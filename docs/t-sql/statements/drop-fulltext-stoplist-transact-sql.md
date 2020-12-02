---
description: DROP FULLTEXT STOPLIST(Transact-SQL)
title: DROP FULLTEXT STOPLIST(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_FULLTEXT_STOPLIST_TSQL
- DROP FULLTEXT STOPLIST
dev_langs:
- TSQL
helpviewer_keywords:
- DROP FULLTEXT STOPLIST statement
- stoplists [full-text search]
- full-text search [SQL Server], stoplists
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 3ee2a2bb-1dfb-4e7c-90e9-9d917cd84a15
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e82a6c699aa31b58e5bdd79d122754cabf728941
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96131227"
---
# <a name="drop-fulltext-stoplist-transact-sql"></a>DROP FULLTEXT STOPLIST(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 데이터베이스에서 전체 텍스트 중지 목록을 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!IMPORTANT]  
>  CREATE FULLTEXT STOPLIST는 호환성 수준 100 이상에만 지원됩니다. 호환성 수준 80 및 90의 경우 시스템 중지 목록이 항상 데이터베이스에 할당됩니다.  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
DROP FULLTEXT STOPLIST stoplist_name  
;  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *stoplist_name*  
 데이터베이스에서 삭제할 전체 텍스트 중지 목록의 이름입니다.  
  
## <a name="remarks"></a>설명  
 삭제 중인 전체 텍스트 중지 목록을 참조하는 전체 텍스트 인덱스가 있는 경우 DROP FULLTEXT STOPLIST가 실패합니다.  
  
## <a name="permissions"></a>사용 권한  
 중지 목록을 삭제하려면 중지 목록에 대한 DROP 권한이 있거나 **db_owner** 또는 **db_ddladmin** 고정 데이터베이스 역할의 멤버 자격이 있어야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `myStoplist`라는 전체 텍스트 중지 목록을 삭제합니다.  
  
```sql 
DROP FULLTEXT STOPLIST myStoplist;  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-stoplist-transact-sql.md)   
 [CREATE FULLTEXT STOPLIST&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)   
 [sys.fulltext_stopwords &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql.md)  
  
  
