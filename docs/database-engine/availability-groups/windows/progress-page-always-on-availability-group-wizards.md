---
title: 진행률 페이지(Always On 가용성 그룹 마법사)
description: SQL Server Management Studio 내 Always On 가용성 그룹 마법사의 '진행률 페이지'에 있는 옵션에 대한 설명입니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.failoverwizard.progress.f1
- sql13.swb.adddatabasewizard.progress.f1
- sql13.swb.addreplicawizard.progress.f1
- sql13.swb.newagwizard.progress.f1
ms.assetid: bd3b0306-8384-4120-a1c9-03825f0ae26a
author: cawrites
ms.author: chadam
ms.openlocfilehash: a019b061fb6352e00ab717e70661be260ad879fe
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584077"
---
# <a name="progress-page-always-on-availability-group-wizards"></a>진행률 페이지(Always On 가용성 그룹 마법사)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  이 대화 상자를 사용하여 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 에서 실행 중인 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]마법사의 진행률을 볼 수 있습니다. 진행률 표시줄에는 마법사에서 수행 중인 단계의 상대적 진행률이 표시됩니다.  
  
## <a name="ui-element-list"></a>UI 요소 목록  
 **자세한 정보**  
 아래쪽 화살표를 클릭하여 완료된 단계와 현재 진행 중인 작업을 순서대로 나열하는 진행률 표를 표시합니다. 표에는 다음 열이 있습니다.  
  
 **이름**  
 특정 단계를 설명하는 문구를 표시합니다.  
  
 **상태**  
 완료된 단계의 결과와 현재 단계의 완료 비율을 다음과 같이 나타냅니다.  
  
|결과|Description|  
|------------|-----------------|  
|**오류**|이 단계의 작업에서 오류가 발생했음을 나타냅니다. 오류를 설명하는 메시지 대화 상자를 표시하려면 링크를 클릭합니다.|  
|**진행 중(** ‘완료율’ **)** |작업이 지금 수행되고 있음을 나타내고 이 단계의 완료율을 추정합니다.|  
|**Success**|이 단계에서 완료된 작업을 나타냅니다.|  
  
 **간략 정보**  
 진행률 표를 숨기려면 클릭합니다.  
  
 **취소**  
 나머지 작업을 건너뛰고 마법사를 종료하려면 클릭합니다.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 그룹에 복제본 추가 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [가용성 그룹에 데이터베이스 추가 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
-   [가용성 그룹 장애 조치(Failover) 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-fail-over-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
