---
title: T-SQL 문
description: PDW (병렬 데이터 웨어하우스)를 SQL Server 하는 APS (분석 플랫폼 시스템)에 대 한 t-sql 문.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 078c0364e64ddca8974544734e8e5a45950e14e0
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778402"
---
# <a name="t-sql-statements-for-parallel-data-warehouse"></a>병렬 데이터 웨어하우스의 t-sql 문
PDW (병렬 데이터 웨어하우스)를 SQL Server 하는 APS (분석 플랫폼 시스템)에 대 한 transact-sql (T-sql) 문

## <a name="data-definition-language-ddl-statements"></a>데이터 정의 언어(DDL) 문
* [ALTER DATABASE](../t-sql/statements/alter-database-transact-sql.md?view=aps-pdw-2016)
* [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md)
* [ALTER PROCEDURE](../t-sql/statements/alter-procedure-transact-sql.md)
* [ALTER SCHEMA](../t-sql/statements/alter-schema-transact-sql.md)
* [ALTER TABLE](../t-sql/statements/alter-table-transact-sql.md)
* [CREATE COLUMNSTORE INDEX](../t-sql/statements/create-columnstore-index-transact-sql.md)
* [CREATE DATABASE](../t-sql/statements/create-database-transact-sql.md?view=aps-pdw-2016)
* [CREATE DATABASE SCOPED CREDENTIAL](../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [CREATE EXTERNAL DATA SOURCE](../t-sql/statements/create-external-data-source-transact-sql.md)
* [CREATE EXTERNAL FILE FORMAT](../t-sql/statements/create-external-file-format-transact-sql.md)
* [CREATE EXTERNAL TABLE](../t-sql/statements/create-external-table-transact-sql.md)
* [CREATE FUNCTION](../t-sql/statements/create-function-sql-data-warehouse.md)
* [CREATE  INDEX](../t-sql/statements/create-index-transact-sql.md)
* [CREATE PROCEDURE](../t-sql/statements/create-procedure-transact-sql.md)
* [CREATE SCHEMA](../t-sql/statements/create-schema-transact-sql.md)
* [CREATE STATISTICS](../t-sql/statements/create-statistics-transact-sql.md)
* [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md)
* [CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)
* [CREATE VIEW](../t-sql/statements/create-view-transact-sql.md)
* [DROP EXTERNAL DATA SOURCE](../t-sql/statements/drop-external-data-source-transact-sql.md)
* [DROP EXTERNAL FILE FORMAT](../t-sql/statements/drop-external-file-format-transact-sql.md)
* [DROP EXTERNAL TABLE](../t-sql/statements/drop-external-table-transact-sql.md)
* [DROP  INDEX](../t-sql/statements/drop-index-transact-sql.md)
* [DROP PROCEDURE](../t-sql/statements/drop-procedure-transact-sql.md)
* [DROP STATISTICS](../t-sql/statements/drop-statistics-transact-sql.md)
* [DROP TABLE](../t-sql/statements/drop-table-transact-sql.md)
* [DROP SCHEMA](../t-sql/statements/drop-schema-transact-sql.md)
* [DROP VIEW](../t-sql/statements/drop-view-transact-sql.md)
* [바꾸면](../t-sql/statements/rename-transact-sql.md)
* [TRUNCATE TABLE](../t-sql/statements/truncate-table-transact-sql.md)
* [UPDATE STATISTICS](../t-sql/statements/update-statistics-transact-sql.md)

## <a name="data-manipulation-language-dml-statements"></a>데이터 조작 언어(DML) 문
* [DELETE](../t-sql/statements/delete-transact-sql.md)
* [INSERT](../t-sql/statements/insert-transact-sql.md)
* [UPDATE](../t-sql/queries/update-transact-sql.md)

## <a name="database-console-commands"></a>데이터베이스 콘솔 명령
* [DBCC DROPCLEANBUFFERS](../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)
* [DBCC FREEPROCCACHE](/previous-versions/sql/sql-server-2016/mt204018(v=sql.130))
* [DBCC SHRINKLOG](../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md?view=aps-pdw-2016-au7)
* [DBCC PDW_SHOWEXECUTIONPLAN](../t-sql/database-console-commands/dbcc-pdw-showexecutionplan-transact-sql.md?view=aps-pdw-2016-au7)
* [DBCC PDW_SHOWPARTITIONSTATS](../t-sql/database-console-commands/dbcc-pdw-showpartitionstats-transact-sql.md?view=aps-pdw-2016-au7)
* [DBCC PDW_SHOWSPACEUSED](../t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql.md)
* [DBCC SHOW_STATISTICS](../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md?view=sql-server-ver15)

## <a name="query-statements"></a>쿼리 문
* [SELECT](../t-sql/queries/select-transact-sql.md)
* [WITH common_table_expression](../t-sql/queries/with-common-table-expression-transact-sql.md)
* [EXCEPT 및 INTERSECT](../t-sql/language-elements/set-operators-except-and-intersect-transact-sql.md)
* [하겠습니다](../t-sql/queries/explain-transact-sql.md)
* [FROM](../t-sql/queries/from-transact-sql.md)
* [PIVOT 및 UNPIVOT 사용](../t-sql/queries/from-using-pivot-and-unpivot.md)
* [GROUP BY](../t-sql/queries/select-group-by-transact-sql.md)
* [HAVING](../t-sql/queries/select-having-transact-sql.md)
* [ORDER BY](../t-sql/queries/select-order-by-clause-transact-sql.md)
* [OPTION](../t-sql/queries/option-clause-transact-sql.md)
* [UNION](../t-sql/language-elements/set-operators-union-transact-sql.md)
* [WHERE](../t-sql/queries/where-transact-sql.md)
* [맨 위로 이동](../t-sql/queries/top-transact-sql.md)
* [별칭 지정](../t-sql/queries/aliasing-azure-sql-data-warehouse-parallel-data-warehouse.md)
* [검색 조건](../t-sql/queries/search-condition-transact-sql.md)
* [하위 쿼리](../t-sql/queries/subqueries-azure-sql-data-warehouse-parallel-data-warehouse.md)

## <a name="security-statements"></a>보안 문
* 사용 권한: [GRANT](../t-sql/statements/grant-transact-sql.md), [DENY](../t-sql/statements/deny-transact-sql.md), [REVOKE](../t-sql/statements/revoke-transact-sql.md)
* [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md)
* [ALTER CERTIFICATE](../t-sql/statements/alter-certificate-transact-sql.md)
* [ALTER DATABASE ENCRYPTION KEY](../t-sql/statements/alter-database-encryption-key-transact-sql.md)
* [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)
* [ALTER MASTER KEY](../t-sql/statements/alter-master-key-transact-sql.md)
* [ALTER ROLE](../t-sql/statements/alter-role-transact-sql.md)
* [ALTER USER](../t-sql/statements/alter-user-transact-sql.md)
* [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
* [CLOSE MASTER KEY](../t-sql/statements/close-master-key-transact-sql.md)
* [CREATE CERTIFICATE](../t-sql/statements/create-certificate-transact-sql.md)
* [CREATE DATABASE ENCRYPTION KEY](../t-sql/statements/create-database-encryption-key-transact-sql.md)
* [CREATE LOGIN](../t-sql/statements/create-login-transact-sql.md)
* [CREATE MASTER KEY](../t-sql/statements/create-master-key-transact-sql.md)
* [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md)
* [CREATE USER](../t-sql/statements/create-user-transact-sql.md)
* [DROP CERTIFICATE](../t-sql/statements/drop-certificate-transact-sql.md)
* [DROP DATABASE ENCRYPTION KEY](../t-sql/statements/drop-database-encryption-key-transact-sql.md)
* [DROP LOGIN](../t-sql/statements/drop-login-transact-sql.md)
* [DROP MASTER KEY](../t-sql/statements/drop-master-key-transact-sql.md)
* [DROP ROLE](../t-sql/statements/drop-role-transact-sql.md)
* [DROP USER](../t-sql/statements/drop-user-transact-sql.md)
* [OPEN MASTER KEY](../t-sql/statements/open-master-key-transact-sql.md)

## <a name="next-steps"></a>다음 단계
자세한 참조 정보는 [t-sql 언어 요소](tsql-language-elements.md) 및 [t-sql 시스템 뷰](tsql-system-views.md)를 참조 하세요.

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
