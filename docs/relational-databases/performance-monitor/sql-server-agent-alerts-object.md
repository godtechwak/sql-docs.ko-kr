---
title: SQL Server 에이전트, Alerts 개체 | Microsoft 문서
description: SQL Server 에이전트 경고에 대한 정보를 보고하는 성능 카운터를 포함하는 SQL Server 에이전트 Alerts 성능 개체에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Alerts object
- SQLAgent:Alerts
ms.assetid: e5e37f74-ee88-46d0-ad8f-71fd1b1fa64a
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 180224d5be7a49f031b3ff37741c90a9647fd89b
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505947"
---
# <a name="sql-server-agent-alerts-object"></a>SQL Server 에이전트, Alerts 개체
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  SQL Server 에이전트 **Alerts** 성능 개체는 SQL Server 에이전트 경고에 대한 정보를 보고하는 성능 카운터를 포함합니다. 다음 표에서는 이 개체가 포함하는 카운터를 나열합니다.  
  
 다음 표에서는 **SQLAgent:Alerts** 카운터를 나열합니다.  
  
|Name|Description|  
|----------|-----------------|  
|**Activated alerts**|이 카운터는 SQL Server 에이전트가 마지막으로 다시 시작된 이후 SQL Server 에이전트가 활성화한 총 경고 수를 보고합니다.|  
|**Alerts activated/minute**|이 카운터는 마지막 시간(분) 내에 SQL Server 에이전트가 활성화한 경고의 수를 보고합니다.|  
  
> [!NOTE]  
>  이 SQL Server 에이전트 개체를 사용하려면 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Alerts](../../ssms/agent/alerts.md)   
 [성능 개체 사용](../../ssms/agent/use-performance-objects.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
