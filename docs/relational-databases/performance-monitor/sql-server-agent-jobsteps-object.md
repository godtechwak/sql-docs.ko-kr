---
title: SQL Server 에이전트, JobSteps 개체 | Microsoft 문서
description: SQL Server 에이전트 작업 단계에 관한 정보를 보고하는 성능 카운터를 포함하는 SQL Server 에이전트 JobSteps 성능 개체에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- JobSteps object
- SQLAgent:JobSteps
ms.assetid: 44f9983c-1753-4fe0-8475-973aa2460b3a
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 18c4c7db9fcd23581162eb4da4d763bfc1efbb3c
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505944"
---
# <a name="sql-server-agent-jobsteps-object"></a>SQL Server 에이전트, JobSteps 개체
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 **JobSteps** 성능 개체에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 단계에 대한 정보를 보고하는 성능 카운터가 포함되어 있습니다. 다음 표에서는 이 개체가 포함하는 카운터를 나열합니다.  
  
 아래 표에는 **SQLAgent:JobSteps** 카운터가 있습니다.  
  
|Name|Description|  
|----------|-----------------|  
|**Active steps**|이 카운터는 현재 실행 중인 작업 단계 수를 보고합니다.|  
|**Queued steps**|이 카운터는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 실행될 준비가 되어 있지만 아직 실행이 시작되지 않은 작업 단계 수를 보고합니다.|  
|**Total step retries**|이 카운터는 마지막 서버 다시 시작 이후에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 작업 단계를 다시 시도한 총횟수를 보고합니다.|  
  
 개체의 각 카운터는 다음 인스턴스를 포함합니다.  
  
|인스턴스|Description|  
|--------------|-----------------|  
|**_Total**|모든 작업 단계에 대한 정보입니다.|  
|**ActiveScripting**|**ActiveScripting** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**ANALYSISCOMMAND**|ANALYSISCOMMAND 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**ANALYSISQUERY**|ANALYSISQUERY 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**CmdExec**|**CmdExec** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**배포**|**Distribution** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**Dts**|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**LogReader**|**LogReader** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**병합**|**Merge** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**PowerShell**|**PowerShell** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**QueueReader**|**QueueReader** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**스냅샷**|**Snapshot** 하위 시스템을 사용하는 작업 단계에 대한 정보입니다.|  
|**TSQL**|[!INCLUDE[tsql](../../includes/tsql-md.md)]을 실행하는 작업 단계에 대한 정보입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [작업 단계 관리](../../ssms/agent/manage-job-steps.md)   
 [성능 개체 사용](../../ssms/agent/use-performance-objects.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
