---
description: DROP AGGREGATE(Transact-SQL)
title: DROP AGGREGATE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_AGGREGATE_TSQL
- DROP AGGREGATE
dev_langs:
- TSQL
helpviewer_keywords:
- aggregate functions [SQL Server], removing
- removing user-defined functions
- dropping user-defined functions
- user-defined functions [CLR integration]
- deleting user-defined functions
- DROP AGGREGATE statement
ms.assetid: 84ffc4e7-c451-4f1f-9a67-7fc3a120e53f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b0ff8af0373d733cd24c507a544694849b849027
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96131326"
---
# <a name="drop-aggregate-transact-sql"></a>DROP AGGREGATE(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스에서 사용자 정의 집계 함수를 제거합니다. 사용자 정의 집계 함수는 [CREATE AGGREGATE](../../t-sql/statements/create-aggregate-transact-sql.md)를 사용하여 만듭니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
DROP AGGREGATE [ IF EXISTS ] [ schema_name . ] aggregate_name  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *IF EXISTS*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 이미 있는 경우에만 집계를 조건부로 삭제합니다.  
  
 *schema_name*  
 사용자 정의 집계 함수가 속한 스키마의 이름입니다.  
  
 *aggregate_name*  
 삭제할 사용자 정의 집계 함수의 이름입니다.  
  
## <a name="remarks"></a>설명  
 DROP AGGREGATE는 삭제할 사용자 정의 집계 함수를 참조하는 스키마 바인딩으로 생성된 뷰, 함수 또는 저장 프로시저가 있는 경우에는 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 DROP AGGREGATE를 실행하려면 최소한 사용자 정의 집계가 속한 스키마에 대한 ALTER 권한이나 집계에 대한 CONTROL 권한이 있어야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 집계 `Concatenate`를 삭제합니다.  
  
```sql  
DROP AGGREGATE dbo.Concatenate;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE AGGREGATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-aggregate-transact-sql.md)   
 [사용자 정의 집계 만들기](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)  
  
  
