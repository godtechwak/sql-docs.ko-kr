---
title: SQL Server, Cursor Manager by Type 개체 | Microsoft 문서
description: 커서 모니터링에 사용되는 카운터를 유형별로 그룹화하여 제공하는 SQLServer:Cursor Manager by Type 개체에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Cursor Manager by Type object
- SQLServer:Cursor Manager by Type
ms.assetid: d67fbd8a-7554-4a16-96f1-d9ee857a95e3
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 95f88849070d95703b611a00c5c1e5abef94fffb
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505795"
---
# <a name="sql-server-cursor-manager-by-type-object"></a>SQL Server, Cursor Manager by Type 개체
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **SQLServer:Cursor Manager by Type** 개체는 커서 모니터링에 사용되는 카운터를 유형별로 그룹화하여 제공합니다.  
  
 다음 표에서는 SQL Server **Cursor Manager by Type** 카운터에 대해 설명합니다.  
  
|Cursor Manager by Type 카운터|Description|  
|-------------------------------------|-----------------|  
|**Active cursors**|활성 커서 수입니다.|  
|**Cache Hit Ratio**|캐시 적중 횟수와 조회 간 비율입니다.|  
|**Cache Hit Ratio**|내부 전용입니다.| 
|**Cached Cursor Counts**|캐시에 있는 특정 유형의 커서 수입니다.|  
|**Cursor Cache Use Count/sec**|각 유형의 캐시된 커서가 사용된 시간입니다.|  
|**Cursor memory usage**|커서가 사용한 메모리 양입니다(KB).|  
|**Cursor Requests/sec**|서버에서 받은 SQL 커서 요청 수입니다.|  
|**Cursor worktable usage**|커서에 사용되는 작업 테이블 수입니다.|  
|**Number of active cursor plans**|커서 계획 수입니다.|  
  
 개체의 각 카운터는 다음 인스턴스를 포함합니다.  
  
|Cursor Manager 인스턴스|Description|  
|-----------------------------|-----------------|  
|**_Total**|모든 커서에 대한 정보입니다.|  
|**API Cursor**|API 커서 정보만 해당됩니다.|  
|**TSQL Global Cursor**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 전역 커서 정보만 해당됩니다.|  
|**TSQL Local Cursor**|[!INCLUDE[tsql](../../includes/tsql-md.md)] 로컬 커서 정보만 해당됩니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
