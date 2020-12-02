---
description: APPLOCK_MODE(Transact-SQL)
title: APPLOCK_MODE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- APPLOCK_MODE_TSQL
- APPLOCK_MODE
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], applications
- applications [SQL Server], locks
- sessions [SQL Server], application locks
- APPLOCK_MODE function
ms.assetid: e43d4917-77f1-45cc-b231-68ba7fee3385
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 40e578837b86b75538e678711293e4adc6b1ac14
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96119536"
---
# <a name="applock_mode-transact-sql"></a>APPLOCK_MODE(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

이 기능은 특정 애플리케이션 리소스에 대해 잠금 소유자가 보유한 잠금 모드를 반환합니다. 애플리케이션 잠금 함수로 APPLOCK_MODE는 현재 데이터베이스에서 작동합니다. 데이터베이스는 애플리케이션 잠금의 범위입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
APPLOCK_MODE( 'database_principal' , 'resource_name' , 'lock_owner' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
'*database_principal*'  
데이터베이스의 개체에 대한 사용 권한이 부여될 수 있는 사용자, 역할 또는 애플리케이션 역할입니다. 함수를 성공적으로 호출하려면 함수 호출자가 *database_principal*, dbo 또는 db_owner 고정 데이터베이스 역할의 멤버여야 합니다.
  
'*resource_name*'  
클라이언트 애플리케이션이 지정한 잠금 리소스의 이름입니다. 애플리케이션은 고유한 리소스 이름인지 확인해야 합니다. 지정된 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 잠금 관리자가 내부적으로 저장할 수 있는 값으로 내부적으로 해시됩니다. *resource_name* 은 **nvarchar(255)** 이며 기본값은 없습니다. *resource_name* 은 이진 비교되며 현재 데이터베이스의 데이터 정렬 설정에 관계없이 대/소문자를 구분합니다.
  
'*lock_owner*'  
잠금의 소유자이며 잠금이 요청되었을 때의 *lock_owner* 값입니다. *lock_owner* 는 **nvarchar (32)** 이고 값은 **Transaction**(기본값) 또는 **Session** 이 될 수 있습니다.
  
## <a name="return-types"></a>반환 형식
**nvarchar(32)**
  
## <a name="return-value"></a>반환 값
특정 애플리케이션 리소스에 대해 잠금 소유자가 보유한 잠금 모드를 반환합니다. 잠금 모드는 다음 값 중 하나일 수 있습니다.
  
||||  
|-|-|-|  
|**NoLock**|**Update**|**\*SharedIntentExclusive**|  
|**IntentShared**|**IntentExclusive**|**\*UpdateIntentExclusive**|  
|**공유**|**전용**||  
  
*이 잠금 모드는 다른 잠금 모드의 조합이며 sp_getapplock은 명시적으로 설정할 수 없습니다.
  
## <a name="function-properties"></a>함수 속성
**비결정적**
  
**Nonindexable**
  
**Nonparallelizable**
  
## <a name="examples"></a>예제  
별도의 세션을 갖는 두 명의 사용자(사용자 A와 사용자 B)가 다음의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령문 시퀀스를 실행합니다.
  
사용자 A는 다음을 실행합니다.
  
```sql
USE AdventureWorks2012;  
GO  
BEGIN TRAN;  
DECLARE @result INT;  
EXEC @result=sp_getapplock  
    @DbPrincipal='public',  
    @Resource='Form1',  
    @LockMode='Shared',  
    @LockOwner='Transaction';  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
GO  
```  
  
그런 다음 사용자 B는 다음을 실행합니다.
  
```sql
Use AdventureWorks2012;  
GO  
BEGIN TRAN;  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
--Result set: NoLock  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Shared', 'Transaction');  
--Result set: 1 (Lock is grantable.)  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: 0 (Lock is not grantable.)  
GO  
```  
  
사용자 A는 다음을 실행합니다.
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
그런 다음 사용자 B는 다음을 실행합니다.
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
사용자 A와 사용자 B가 다음을 실행합니다.
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>참고 항목
[APPLOCK_TEST&#40;Transact-SQL&#41;](../../t-sql/functions/applock-test-transact-sql.md)  
[sp_getapplock&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  
