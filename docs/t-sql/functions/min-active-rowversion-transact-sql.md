---
description: MIN_ACTIVE_ROWVERSION(Transact-SQL)
title: MIN_ACTIVE_ROWVERSION(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- MIN_ACTIVE_ROWVERSION
- MIN_ACTIVE_ROWVERSION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MIN_ACTIVE_ROWVERSION function [Transact-SQL]
ms.assetid: 87c89547-8ea1-4820-b75e-36be683e4e10
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 61304621317ee302585102acdd82198fd90baedd
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91115971"
---
# <a name="min_active_rowversion-transact-sql"></a>MIN_ACTIVE_ROWVERSION(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  현재 데이터베이스의 비활성 **rowversion** 값을 반환합니다. **rowversion** 값이 아직 커밋되지 않은 트랜잭션에서 사용되는 경우에는 활성 상태입니다. 자세한 내용은 [rowversion &#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)을 참조하세요.  
  
> [!NOTE]  
>  **rowversion** 데이터 형식은 **timestamp** 라고도 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
MIN_ACTIVE_ROWVERSION ( ) 
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 **binary(8)** 값을 반환합니다.  
  
## <a name="remarks"></a>설명  
 MIN_ACTIVE_ROWVERSION은 현재 데이터베이스의 가장 낮은 활성 **rowversion** 값을 반환하는 비결정적 함수입니다. 새로운 **rowversion** 값은 일반적으로 **rowversion** 형식의 열이 포함된 테이블에 삽입 또는 업데이트가 수행될 때 생성됩니다. 데이터베이스에 활성 값이 없는 경우 MIN_ACTIVE_ROWVERSION은 @@DBTS + 1과 같은 값을 반환합니다.  
  
 MIN_ACTIVE_ROWVERSION은 **rowversion** 값을 사용하여 변경 내용 집합을 그룹화하는 데이터 동기화와 같은 시나리오에 유용합니다. 애플리케이션이 MIN_ACTIVE_ROWVERSION이 아닌 @@DBTS를 사용하면 동기화가 일어날 때 활성 상태인 변경 내용을 놓칠 수 있습니다.  
  
 MIN_ACTIVE_ROWVERSION 함수는 트랜잭션 격리 수준에 있는 변경 내용의 영향을 받지 않습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `MIN_ACTIVE_ROWVERSION` 및 `@@DBTS`를 사용하여 **rowversion** 값을 반환합니다. 데이터베이스에 활성 트랜잭션이 없으면 값이 달라집니다.  
  
```sql  
-- Create a table that has a ROWVERSION column in it.  
CREATE TABLE RowVersionTestTable (rv ROWVERSION)  
GO  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()   
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E2  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E3  
  
-- Insert a row.  
INSERT INTO RowVersionTestTable VALUES (DEFAULT)  
SELECT * FROM RowVersionTestTable  
GO  
---------------- Results ----------------  
--rv  
--0x00000000000007E3  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()  
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E3  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E4  
  
-- Insert a new row inside a transaction but do not commit.  
BEGIN TRAN  
INSERT INTO RowVersionTestTable VALUES (DEFAULT)  
SELECT * FROM RowVersionTestTable  
GO  
---------------- Results ----------------  
--rv  
--0x00000000000007E3  
--0x00000000000007E4  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()   
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E4  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E4  
  
-- Commit the transaction.  
COMMIT  
GO  
  
-- Print the current values for the database.  
PRINT ''  
PRINT 'DBTS'  
PRINT @@DBTS  
PRINT 'MIN_ACTIVE_ROWVERSION'  
PRINT MIN_ACTIVE_ROWVERSION()  
GO  
---------------- Results ----------------  
--DBTS  
--0x00000000000007E4  
--MIN_ACTIVE_ROWVERSION  
--0x00000000000007E5  
```  
  
## <a name="see-also"></a>참고 항목  
 [@@DBTS&#40;Transact-SQL&#41;](../../t-sql/functions/dbts-transact-sql.md)   
 [rowversion&#40;Transact-SQL&#41;](../../t-sql/data-types/rowversion-transact-sql.md)  
  
  
