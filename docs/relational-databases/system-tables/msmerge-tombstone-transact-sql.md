---
description: MSmerge_tombstone(Transact-SQL)
title: MSmerge_tombstone (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_tombstone_TSQL
- MSmerge_tombstone
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_tombstone system table
ms.assetid: 8b3fc7bf-729b-40f2-8a26-e7dfbe8ddb38
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dc137583386c4b098960d762484ef526f2f95f14
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545568"
---
# <a name="msmerge_tombstone-transact-sql"></a>MSmerge_tombstone(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSmerge_tombstone** 테이블은 삭제 된 행에 대 한 정보를 포함 하며 삭제는 다른 구독자로 전파할 수 있습니다. 이 테이블은 게시 및 구독 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**rowguid**|**uniqueidentifier**|행 식별자입니다.|  
|**tablenick**|**int**|테이블의 애칭입니다.|  
|**type**|**tinyint**|삭제의 유형입니다.<br /><br /> 1 = 사용자 삭제입니다.<br /><br /> 5 = 행이 더 이상 필터링된 파티션에 속하지 않습니다.<br /><br /> 6 = 시스템 삭제입니다.|  
|**계보**|**varbinary (249)**|삭제된 레코드의 버전과 삭제될 때 알려진 업데이트를 표시합니다. 한 구독자에서 행이 삭제되는 동안 다른 구독자가 해당 행을 업데이트하는 경우 충돌을 일관성 있게 해결하기 위해 필요한 규칙을 허용합니다.|  
|**작성**|**int**|행을 삭제할 때 할당됩니다. 구독자가 세대 N을 요청 하면 생성 >= N 인 삭제 표식만 전송 됩니다.|  
|**logical_record_parent_rowguid**|**uniqueidentifier**|삭제된 행이 속한 논리적 레코드를 식별합니다.|  
|**logical_record_lineage**|**Varbinary (501)**|이 행이 속한 논리적 레코드에 대한 삭제 기록을 유지 관리하기 위해 사용하는 구독자 애칭과 버전 번호 쌍입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
