---
description: DATABASE_PRINCIPAL_ID(Transact-SQL)
title: DATABASE_PRINCIPAL_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATABASE_PRINCIPAL_ID_TSQL
- DATABASE_PRINCIPAL_ID
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], principals
- principal ID numbers [SQL Server]
- DATABASE_PRINCIPAL_ID function
- IDs [SQL Server], principals
ms.assetid: 908c7dd8-c10b-4658-92f6-0224f9835dd9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 95d7bf7ac61ed2b79829a5aeb9d41c7f06485c8d
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96117951"
---
# <a name="database_principal_id-transact-sql"></a>DATABASE_PRINCIPAL_ID(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

이 함수는 현재 데이터베이스의 보안 주체 ID를 반환합니다. 보안 주체에 대한 자세한 내용은 [보안 주체&#40;데이터베이스 엔진#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)를 참조하세요.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```syntaxsql
DATABASE_PRINCIPAL_ID ( 'principal_name' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*principal_name*  
보안 주체를 나타내는 **sysname** 형식의 식입니다. *principal_name* 을 생략하면 `DATABASE_PRINCIPAL_ID`가 현재 사용자의 ID를 반환합니다. `DATABASE_PRINCIPAL_ID`에는 괄호가 필요합니다.
  
## <a name="return-types"></a>반환 형식
**int**  
데이터베이스 보안 주체가 없는 경우 NULL입니다.
  
## <a name="remarks"></a>설명  
`DATABASE_PRINCIPAL_ID`는 선택 목록, WHERE 절 또는 식을 허용하는 모든 위치에서 사용합니다. 자세한 내용은 [식 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)을 참조하세요.
  
## <a name="examples"></a>예제  
  
### <a name="a-retrieving-the-id-of-the-current-user"></a>A. 현재 사용자의 ID 검색  
이 예에서는 현재 사용자의 데이터베이스 보안 주체 ID를 반환합니다.
  
```sql
SELECT DATABASE_PRINCIPAL_ID();  
GO  
```  
  
### <a name="b-retrieving-the-id-of-a-specified-database-principal"></a>B. 지정한 데이터베이스 보안 주체의 ID 검색  
이 예에서는 `db_owner` 데이터베이스 역할에 대한 데이터베이스 보안 주체 ID를 반환합니다.
  
```sql
SELECT DATABASE_PRINCIPAL_ID('db_owner');  
GO  
```  
  
## <a name="see-also"></a>참고 항목
[보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
[사용 권한 계층&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
[sys.database_principals&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)
  
  
