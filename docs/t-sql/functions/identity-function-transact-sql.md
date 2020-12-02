---
description: IDENTITY(함수)(Transact-SQL)
title: IDENTITY (Function) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IDENTITY_TSQL
- IDENTITY
dev_langs:
- TSQL
helpviewer_keywords:
- IDENTITY function
- SELECT statement [SQL Server], IDENTITY function
- inserting identity columns
- columns [SQL Server], creating
- identity columns [SQL Server], IDENTITY function
ms.assetid: ebec77eb-fc02-4feb-b6c5-f0098d43ccb6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 364bcd6eb68ca7c529c56fae70109b79cbc1dc18
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91114734"
---
# <a name="identity-function-transact-sql"></a>IDENTITY(함수)(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ID 열을 새 테이블에 삽입하기 위해 INTO *테이블* 절과 함께 SELECT 문에서만 사용됩니다. IDENTITY 함수는 CREATE TABLE 및 ALTER TABLE과 함께 사용되는 IDENTITY 속성과 비슷하지만 동일하지는 않습니다.  
  
> [!NOTE]  
>  여러 테이블에서 사용할 수 있거나 테이블을 참조하지 않고 애플리케이션에서 호출할 수 있는 자동으로 증가하는 번호를 만들려면 [시퀀스 번호](../../relational-databases/sequence-numbers/sequence-numbers.md)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
IDENTITY (data_type [ , seed , increment ] ) AS column_name  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *data_type*  
 ID 열의 데이터 형식입니다. ID 열의 유효한 데이터 형식은 **bit** 데이터 형식을 제외한 정수 데이터 형식 범주의 모든 데이터 형식 또는 **decimal** 데이터 형식입니다.  
  
 *seed*  
 테이블의 첫 번째 행에 할당되는 정수 값입니다. 후속 행에는 각각 마지막 IDENTITY 값에 *증가* 값을 더한 것과 같은 다음 ID 값이 할당됩니다. *초기값* 및 *증가값* 을 모두 지정하지 않으면 기본값은 모두 1이 됩니다.  
  
 *increment*  
 테이블의 연속된 행에 대해 *초기* 값에 추가되는 정수 값입니다.  
  
 *column_name*  
 새 테이블에 삽입될 열의 이름입니다.  
  
## <a name="return-types"></a>반환 형식  
 *data_type* 과 같은 유형을 반환합니다.  
  
## <a name="remarks"></a>설명  
 이 함수는 테이블에 열을 만들기 때문에 다음 방법 중 하나를 사용하여 선택 목록에서 열 이름을 지정해야 합니다.  
  
```sql  
--(1)  
SELECT IDENTITY(int, 1,1) AS ID_Num  
INTO NewTable  
FROM OldTable;  
  
--(2)  
SELECT ID_Num = IDENTITY(int, 1, 1)  
INTO NewTable  
FROM OldTable;  
```  
  
## <a name="examples"></a>예제  
 다음 예는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 데이터베이스의 `Contact` 테이블에 있는 모든 행을 `NewContact`라는 새 테이블에 삽입합니다. IDENTITY 함수는 `NewContact` 테이블에서 ID를 1 대신 100부터 시작하는 데 사용됩니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID (N'Person.NewContact', N'U') IS NOT NULL  
    DROP TABLE Person.NewContact;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY BULK_LOGGED;  
GO  
SELECT  IDENTITY(smallint, 100, 1) AS ContactNum,  
        FirstName AS First,  
        LastName AS Last  
INTO Person.NewContact  
FROM Person.Person;  
GO  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
GO  
SELECT ContactNum, First, Last FROM Person.NewContact;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE TABLE&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [@@IDENTITY&#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [IDENTITY&#40;속성&#41;&#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql-identity-property.md)   
 [SELECT @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/select-local-variable-transact-sql.md)   
 [DBCC CHECKIDENT&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [sys.identity_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-identity-columns-transact-sql.md)  
  
  
