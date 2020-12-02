---
description: DROP FULLTEXT CATALOG(Transact-SQL)
title: DROP FULLTEXT CATALOG(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_FULLTEXT_CATALOG_TSQL
- DROP FULLTEXT CATALOG
dev_langs:
- TSQL
helpviewer_keywords:
- dropping full-text catalogs
- removing full-text catalogs
- full-text catalogs [SQL Server], removing
- deleting full-text catalogs
- DROP FULLTEXT CATALOG statement
ms.assetid: b54efb0b-400b-49ce-923b-ce20a2a12255
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 71061c8265ccd7ca2b1d8ed060843b06db621b0e
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127431"
---
# <a name="drop-fulltext-catalog-transact-sql"></a>DROP FULLTEXT CATALOG(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  데이터베이스에서 전체 텍스트 카탈로그를 제거합니다. 카탈로그를 삭제하기 전에 카탈로그와 연관된 모든 전체 텍스트 인덱스를 삭제해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
DROP FULLTEXT CATALOG catalog_name  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *catalog_name*  
 제거할 카탈로그의 이름입니다. *catalog_name* 이 없는 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 오류를 반환하고 DROP 작업을 수행하지 않습니다. 명령을 제대로 수행하려면 전체 텍스트 카탈로그의 파일 그룹에 OFFLINE 또는 READONLY가 표시되지 않아야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 전체 텍스트 카탈로그에 대해 DROP 사용 권한이 있거나 **db_owner** 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sys.fulltext_catalogs&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [ALTER FULLTEXT CATALOG&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT CATALOG&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [전체 텍스트 검색](../../relational-databases/search/full-text-search.md)  
  
  
