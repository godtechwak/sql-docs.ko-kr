---
title: 가용성 그룹에서 가용성 복제본 연결이 해제됨
description: Always On 가용성 그룹 내에서 복제본의 연결이 해제된 이유에 대한 가능한 원인을 식별합니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: troubleshooting
f1_keywords:
- sql13.swb.agdashboard.arp2connected.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: 1a2162d3-54fb-4356-b349-effbdc15a5a4
author: cawrites
ms.author: chadam
ms.openlocfilehash: e06e94693f8f6102962b08893878ba5ac249cb3b
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584633"
---
# <a name="availability-replica-is-disconnected-within-an-always-on-availability-group"></a>Always On 가용성 그룹 내에서 가용성 복제본 연결이 해제됨
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
    
## <a name="introduction"></a>소개  
  
|||  
|-|-|  
|**정책 이름**|가용성 복제본 연결 상태|  
|**문제점**|가용성 복제본의 연결이 끊어짐|  
|**범주**|**심각**|  
|**패싯**|가용성 복제본|  
  
## <a name="description"></a>Description  
 이 정책은 가용성 복제본 간의 연결 상태를 확인합니다. 가용성 복제본의 연결 상태가 DISCONNECTED인 경우 정책은 비정상 상태에 있습니다. 그렇지 않으면 정책은 정상 상태입니다.  
  
> [!NOTE]  
>  이 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]릴리스의 경우 가능한 원인 및 해결 방법에 대한 자세한 내용은 TechNet Wiki의 [가용성 복제본의 연결이 끊어짐](https://go.microsoft.com/fwlink/p/?LinkId=220857) 을 참조하세요.  
  
## <a name="possible-causes"></a>가능한 원인  
 보조 복제본이 주 복제본에 연결되어 있지 않습니다. 연결 상태가 DISCONNECTED입니다. 이 문제는 다음에 의해 발생할 수 있습니다.  
  
-   연결 포트가 다른 애플리케이션과 충돌했을 수 있습니다.  
  
-   암호화 유형 또는 알고리즘이 일치하지 않습니다.  
  
-   연결 엔드포인트가 삭제되었거나 시작되지 않았습니다.  
  
-   전송 연결이 끊어졌습니다.  
  
## <a name="possible-solutions"></a>가능한 해결 방법  
 이 문제에 대한 해결 방법은 다음과 같습니다.  
  
-   주 복제본 및 보조 복제본 인스턴스의 데이터베이스 미러링 엔드포인트 구성을 확인하여 일치하지 않는 구성을 업데이트합니다.  
  
-   포트가 충돌하는 경우 포트 번호를 변경합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
