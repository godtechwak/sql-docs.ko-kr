---
description: CREATE PARTITION SCHEME(Transact-SQL)
title: CREATE PARTITION SCHEME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE PARTITION SCHEME
- SCHEME
- PARTITION SCHEME
- CREATE_PARTITION_SCHEME_TSQL
- SCHEME_TSQL
- PARTITION_SCHEME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- partitioned indexes [SQL Server], schemes
- partitioned tables [SQL Server], schemes
- CREATE PARTITION SCHEME statement
- partition schemes [SQL Server], creating
- filegroups [SQL Server], partitions
- partitioned indexes [SQL Server], filegroups
- partitioned tables [SQL Server], filegroups
- mapping partitions [SQL Server]
ms.assetid: 5b21c53a-b4f4-4988-89a2-801f512126e4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ea6018e34db8ddc07a1e30cec6089994e402b9e6
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124039"
---
# <a name="create-partition-scheme-transact-sql"></a>CREATE PARTITION SCHEME(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  현재 데이터베이스에서 분할된 테이블 또는 인덱스의 파티션을 파일 그룹에 매핑하는 구성표를 만듭니다. 분할된 테이블 또는 인덱스의 파티션 수 및 도메인은 파티션 함수에서 결정됩니다. 파티션 구성표를 만들기 전에 [CREATE PARTITION FUNCTION](../../t-sql/statements/create-partition-function-transact-sql.md) 문을 사용해 먼저 파티션 함수를 만들어야 합니다.  

>[!NOTE]
>Azure SQL Database에서는 기본 파일 그룹만 지원됩니다.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
CREATE PARTITION SCHEME partition_scheme_name  
AS PARTITION partition_function_name  
[ ALL ] TO ( { file_group_name | [ PRIMARY ] } [ ,...n ] )  
[ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *partition_scheme_name*  
 파티션 구성표의 이름입니다. 파티션 구성표 이름은 데이터베이스 내에서 고유해야 하며 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다.  
  
 *partition_function_name*  
 파티션 구성표를 사용하는 파티션 함수의 이름입니다. 파티션 함수로 생성한 파티션은 파티션 구성표에서 지정한 파일 그룹으로 매핑됩니다. *partition_function_name* 이 데이터베이스에 이미 있어야 합니다. 단일 파티션에는 FILESTREAM 파일 그룹과 FILESTREAM이 아닌 파일 그룹이 둘 다 포함될 수 없습니다.  
  
 ALL  
 모든 파티션이 *file_group_name* 에서 제공한 파일 그룹에 매핑되거나 또는 **[** PRIMARY **]** 가 지정된 경우 주 파일 그룹에 매핑되도록 지정합니다. ALL을 지정하면 하나의 *file_group_name* 만 지정할 수 있습니다.  
  
 *file_group_name* |  **[** PRIMARY **]** [ **,** _...n_]  
 *partition_function_name* 에 지정된 파티션을 보유할 파일 그룹의 이름을 지정합니다. *file_group_name* 은 데이터베이스에 이미 있어야 합니다.  
  
 **[** PRIMARY **]** 를 지정하면 파티션은 주 파일 그룹에 저장됩니다. ALL을 지정하면 하나의 *file_group_name* 만 지정할 수 있습니다. [ **,** _...n_]에 나열된 파일 그룹의 순서대로 1번 파티션부터 시작하여 파티션을 파일 그룹에 할당합니다. [ **,** _...n_]에서 같은 *file_group_name* 을 두 번 이상 지정할 수 있습니다. *n* 이 *partition_function_name* 에서 지정된 만큼의 파티션 수를 보유하기에 부족한 경우 CREATE PARTITION SCHEME은 오류가 발생하고 실패합니다.  
  
 *partition_function_name* 이 파일 그룹보다 적은 파티션을 생성한 경우 할당되지 않은 첫 번째 파일 그룹이 NEXT USED로 표시되고 정보 메시지가 NEXT USED 파일 그룹에 표시됩니다. ALL을 지정하면 하나의 *file_group_name* 만이 해당 *partition_function_name* 의 NEXT USED 속성을 유지합니다. ALTER PARTITION FUNCTION 문에서 파티션을 생성한 경우 NEXT USED 파일 그룹이 추가 파티션을 받습니다. 할당되지 않은 파일 그룹을 추가로 만들어 새 파티션을 보유하려면 ALTER PARTITION SCHEME을 사용하십시오.  
  
 *file_group_name* [ 1 **,** _...n_]에서 주 파일 그룹을 지정하면 PRIMARY는 키워드이므로 **[** PRIMARY **]** 와 같이 구분해야 합니다.  
  
 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]에는 PRIMARY만 사용할 수 있습니다. 아래 예제 E를 참조하세요. 
  
## <a name="permissions"></a>사용 권한  
 CREATE PARTITION SCHEME을 실행하는 데 필요한 권한은 다음과 같습니다.  
  
-   ALTER ANY DATASPACE 권한. 이 권한은 기본적으로 **sysadmin** 고정 서버 역할 및 **db_owner** 및 **db_ddladmin** 고정 데이터베이스 역할의 멤버에게 부여됩니다.  
  
-   파티션 구성표가 생성된 데이터베이스에 대한 CONTROL 또는 ALTER 권한  
  
-   파티션 구성표가 생성된 데이터베이스의 서버에 대한 CONTROL SERVER 또는 ALTER ANY DATABASE 권한  
  
## <a name="examples"></a>예제  
  
### <a name="a-creating-a-partition-scheme-that-maps-each-partition-to-a-different-filegroup"></a>A. 각 파티션을 다른 파일 그룹에 매핑하는 파티션 구성표 만들기  
 다음 예에서는 테이블이나 인덱스를 4개의 파티션으로 분할하는 파티션 함수를 만듭니다. 4개의 파티션 각각을 보유하도록 파일 그룹을 지정하는 파티션 구성표를 만듭니다. 이 예에서는 데이터베이스에 이미 파일 그룹이 있다고 가정합니다.  
  
```sql  
CREATE PARTITION FUNCTION myRangePF1 (INT)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS1  
AS PARTITION myRangePF1  
TO (test1fg, test2fg, test3fg, test4fg);  
```  
  
 **col1** 분할 열에 `myRangePF1` 파티션 함수를 사용하는 테이블의 파티션은 다음 표와 같이 할당됩니다.  
  
||||||  
|-|-|-|-|-|  
|**파일 그룹**|`test1fg`|`test2fg`|`test3fg`|`test4fg`|  
|**파티션**|1|2|3|4|  
|**값**|**col1** <= `1`|**col1** > `1` AND **col1** <= `100`|**col1** > `100` AND **col1** <= `1000`|**col1** > `1000`|  
  
### <a name="b-creating-a-partition-scheme-that-maps-multiple-partitions-to-the-same-filegroup"></a>B. 여러 파티션을 같은 파일 그룹에 매핑하는 파티션 구성표 만들기  
 모든 파티션을 같은 파일 그룹에 매핑하는 경우 ALL 키워드를 사용하십시오. 그러나 모든 파티션이 아니라 여러 개의 일부 파티션을 같은 파일 그룹에 매핑하는 경우 다음 예와 같이 파일 그룹 이름을 반복해야 합니다.  
  
```sql  
CREATE PARTITION FUNCTION myRangePF2 (INT)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS2  
AS PARTITION myRangePF2  
TO ( test1fg, test1fg, test1fg, test2fg );  
```  
  
 **col1** 분할 열에 `myRangePF2` 파티션 함수를 사용하는 테이블의 파티션은 다음 표와 같이 할당됩니다.  
  
||||||  
|-|-|-|-|-|  
|**파일 그룹**|`test1fg`|`test1fg`|`test1fg`|`test2fg`|  
|**파티션**|1|2|3|4|  
|**값**|**col1** <= `1`|**col1** > 1 AND **col1** <= `100`|**col1** > `100` AND **col1** <= `1000`|**col1** > `1000`|  
  
### <a name="c-creating-a-partition-scheme-that-maps-all-partitions-to-the-same-filegroup"></a>C. 모든 파티션을 같은 파일 그룹에 매핑하는 파티션 구성표 만들기  
 다음 예에서는 앞의 예와 같은 파티션 함수를 만들고 모든 파티션을 같은 파일 그룹에 매핑하는 파티션 구성표를 만드는 방법을 보여 줍니다.  
  
```sql  
CREATE PARTITION FUNCTION myRangePF3 (INT)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS3  
AS PARTITION myRangePF3  
ALL TO ( test1fg );  
```  
  
### <a name="d-creating-a-partition-scheme-that-specifies-a-next-used-filegroup"></a>D. 'NEXT USED' 파일 그룹을 지정하는 파티션 구성표 만들기  
 다음 예에서는 앞의 예와 같은 파티션 함수를 만들고 연관된 파티션 함수가 생성한 파티션보다 많은 파일 그룹을 나열하는 파티션 구성표를 만드는 방법을 보여 줍니다.  
  
```sql  
CREATE PARTITION FUNCTION myRangePF4 (INT)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS4  
AS PARTITION myRangePF4  
TO (test1fg, test2fg, test3fg, test4fg, test5fg)  
```  
  
 문을 실행하면 다음 메시지가 반환됩니다.  
  
파티션 구성표 'myRangePS4'가 작성되었습니다. 파티션 구성표 'myRangePS4'에서 'test5fg'는 다음에 사용되는 파일 그룹으로 표시됩니다.  
  
  
 파티션을 추가하도록 `myRangePF4` 파티션 함수를 변경한 경우 `test5fg` 파일 그룹이 새로 만들어진 파티션을 받습니다.  

### <a name="e-creating-a-partition-scheme-only-on-primary---only-primary-is-supported-for-sqldbesa"></a>E. PRIMARY에서만 파티션 구성표 만들기 - [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]에서는 PRIMARY만 지원됨

 다음 예에서는 테이블이나 인덱스를 4개의 파티션으로 분할하는 파티션 함수를 만듭니다. 그러면 모든 파티션이 PRIMARY 파일 그룹에 만들어지도록 지정하는 파티션 구성표가 만들어집니다.  
  
```sql  
CREATE PARTITION FUNCTION myRangePF1 (INT)  
AS RANGE LEFT FOR VALUES (1, 100, 1000);  
GO  
CREATE PARTITION SCHEME myRangePS1  
AS PARTITION myRangePF1  
ALL TO ( [PRIMARY] );  
```
   
## <a name="see-also"></a>참고 항목  
 [CREATE PARTITION FUNCTION&#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)   
 [ALTER PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/alter-partition-scheme-transact-sql.md)   
 [DROP PARTITION SCHEME&#40;Transact-SQL&#41;](../../t-sql/statements/drop-partition-scheme-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [분할된 테이블 및 인덱스 만들기](../../relational-databases/partitions/create-partitioned-tables-and-indexes.md)   
 [sys.partition_schemes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [sys.data_spaces &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)   
 [sys.destination_data_spaces&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-destination-data-spaces-transact-sql.md)   
 [sys.partitions&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [sys.tables&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)   
 [sys.indexes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
