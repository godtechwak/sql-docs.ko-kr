---
title: 가용성 그룹에 대해 자동 장애 조치(Failover)가 준비되지 않음
description: Always On 가용성 그룹에 대해 장애 조치(failover)가 준비되지 않은 이유의 가능한 원인을 식별하는 방법을 알아봅니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: end-user-help
f1_keywords:
- sql13.swb.agdashboard.agp3autofailover.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 28261014-342c-442a-bd89-6d04b8d4e8b7
author: cawrites
ms.author: chadam
ms.openlocfilehash: 1a5609955ca61cb1ef2df4a940e749c6cb7c038c
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584747"
---
# <a name="always-on-availability-group-is-not-ready-for-automatic-failover"></a>Always On 가용성 그룹에 대해 자동 장애 조치(Failover)가 준비되지 않았습니다.
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
    
## <a name="introduction"></a>소개  
  
|||  
|-|-|  
|**정책 이름**|가용성 그룹 자동 장애 조치(Failover) 준비|  
|**문제점**|가용성 그룹에 대해 자동 장애 조치(Failover)가 준비되지 않음|  
|**범주**|**심각**|  
|**패싯**|가용성 그룹|  
  
## <a name="description"></a>Description  
 이 정책은 가용성 그룹에 장애 조치(failover)가 준비된 보조 복제본이 하나 이상 있는지 확인합니다. 주 복제본의 장애 조치(Failover) 모드가 자동이지만 가용성 그룹에 장애 조치(Failover)가 준비된 보조 복제본이 하나도 없는 경우 이 정책은 비정상 상태이며 경고가 발생합니다.  
  
 적어도 하나의 보조 복제본이 자동 장애 조치(Failover)가 준비된 상태이면 정책은 정상 상태입니다.  
  
> [!NOTE]  
>  이 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]릴리스의 경우 가능한 원인 및 해결 방법에 대한 자세한 내용은 TechNet Wiki의 [가용성 그룹에 대해 자동 장애 조치(Failover)가 준비되지 않음](https://go.microsoft.com/fwlink/p/?LinkId=220851) 을 참조하세요.  
  
## <a name="possible-causes"></a>가능한 원인  
 가용성 그룹에 대해 자동 장애 조치(Failover)가 준비되지 않았습니다. 주 복제본은 자동 장애 조치(Failover)를 사용하도록 구성되어 있지만 보조 복제본은 자동 장애 조치(Failover)를 사용하도록 구성되어 있지 않습니다. 자동 장애 조치(Failover)를 사용하도록 구성된 보조 복제본을 사용할 수 없거나 해당 데이터 동기화 상태가 현재 SYNCHRONIZED가 아닙니다.  
  
## <a name="possible-solutions"></a>가능한 해결 방법  
 이 문제에 대한 해결 방법은 다음과 같습니다.  
  
-   적어도 하나의 보조 복제본이 자동 장애 조치(Failover)를 사용하도록 구성되어 있는지 확인합니다. 자동 장애 조치(Failover)를 사용하도록 구성되어 있는 보조 복제본이 없으면 동기 커밋을 사용하여 자동 장애 조치(Failover) 대상이 되도록 보조 복제본의 구성을 업데이트합니다.  
  
-   정책을 사용하여 데이터가 동기화 상태에 있는지, 그리고 자동 장애 조치(failover) 대상이 SYNCHRONIZED인지 확인한 다음 가용성 복제본에서 문제를 해결합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
