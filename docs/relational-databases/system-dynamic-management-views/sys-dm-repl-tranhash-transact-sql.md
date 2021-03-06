---
description: sys.dm_repl_tranhash(Transact-SQL)
title: sys. dm_repl_tranhash (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_repl_tranhash
- sys.dm_repl_tranhash_TSQL
- dm_repl_tranhash_TSQL
- dm_repl_tranhash
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_repl_tranhash dynamic management view
ms.assetid: 0cc52338-e805-4ed4-9835-b19bbf72448e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 35bb540ff2b73a44de324a51937552ae7cc3ec56
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536902"
---
# <a name="sysdm_repl_tranhash-transact-sql"></a>sys.dm_repl_tranhash(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  트랜잭션 게시에서 복제되고 있는 트랜잭션에 대한 정보를 반환합니다.  
  
|column_name|data_type|description|  
|------------------|----------------|-----------------|  
|**버킷**|**bigint**|해시 테이블의 버킷 수입니다.|  
|**hashed_trans**|**bigint**|현재 일괄 처리에서 복제된 커밋된 트랜잭션 수입니다.|  
|**completed_trans**|**bigint**|지금까지 완료된 트랜잭션 수입니다.|  
|**compensated_trans**|**bigint**|부분 롤백을 포함하는 트랜잭션 수입니다.|  
|**first_begin_lsn**|**nvarchar (64)**|현재 일괄 처리에서 가장 빠른 시작 LSN(로그 시퀀스 번호)입니다.|  
|**last_commit_lsn**|**nvarchar (64)**|현재 일괄 처리에서 마지막 커밋 LSN입니다.|  
  
## <a name="permissions"></a>사용 권한  
 **Dm_repl_tranhash**를 호출 하려면 게시 데이터베이스에 대 한 VIEW DATABASE STATE 권한이 필요 합니다.  
  
## <a name="remarks"></a>설명  
 현재 복제 아티클 캐시에 로드되어 있는 복제된 데이터베이스 개체에 대한 정보만 반환됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [복제 관련 동적 관리 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)  
  
  
