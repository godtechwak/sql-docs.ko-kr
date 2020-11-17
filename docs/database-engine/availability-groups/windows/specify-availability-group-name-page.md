---
title: '가용성 그룹 마법사: 가용성 그룹 옵션 지정'
description: SQL Server Management Studio 내 가용성 그룹 마법사의 '가용성 그룹 이름 지정' 페이지에 있는 옵션을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.newagwizard.specifyagname.f1
- sql13.swb.adddatabasewizard.specifyagname.f1
ms.assetid: dcb6374d-becb-4c6c-b88c-5a8273f8aa38
author: cawrites
ms.author: chadam
ms.openlocfilehash: 8ca6b683bf1fd51d0942984e2b4fcecd5b7d9a9d
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583904"
---
# <a name="specify-availability-group-options-page-for-an-always-on-availability-group"></a>Always On 가용성 그룹에 대한 가용성 그룹 옵션 지정 페이지
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 **가용성 그룹 이름 지정** 페이지의 옵션에 대해 설명합니다. 이 항목은 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 의 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] 및 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]모두에 사용됩니다.  
  
##  <a name="specify-availability-group-options"></a><a name="PageOptions"></a> 가용성 그룹 옵션 지정  
 **가용성 그룹 이름**  
 가용성 그룹의 이름을 지정합니다. 새 가용성 그룹의 경우 WSFC(Windows Server 장애 조치 클러스터)의 모든 가용성 그룹에서 고유하고 유효한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 식별자를 지정합니다. 가용성 그룹 이름의 최대 길이는 128자입니다.  

 **클러스터 유형** 다음으로 클러스터 유형을 지정합니다. 가능한 클러스터 유형은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전 및 운영 체제에 따라 다릅니다. 다음 목록에서 하나를 선택합니다.

   * **Windows Server 장애 조치(failover) 클러스터링**
   
      고가용성 및 재해 복구를 위해 Windows Server 장애 조치 클러스터에 속한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 가용성 그룹을 호스팅할 때 사용합니다. 지원되는 모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 버전에 적용됩니다. 

   * **외부**
      
      고가용성 및 재해 복구를 위해 외부 클러스터 기술(예: Linux의 Pacemaker)로 관리되는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 가용성 그룹을 호스팅할 때 사용합니다. [!INCLUDE[sssqlv14](../../../includes/sssqlv14-md.md)] 이상에 적용됩니다.

   * **NONE**
      
      읽기-배율 및 부하 분산을 위해 클러스터 기술로 관리되지 않는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 가용성 그룹을 호스팅할 때 사용합니다. [!INCLUDE[sssqlv14](../../../includes/sssqlv14-md.md)] 이상에 적용됩니다. 
 
   **데이터베이스 수준 상태 검색** 이 확인란을 선택하면 가용성 그룹에 대해 데이터베이스 수준 상태 검색(DB_FAILOVER) 옵션을 사용하도록 설정됩니다. 데이터베이스가 더 이상 온라인 상태가 아니거나 문제가 발생하여 가용성 그룹의 자동 장애 조치가 트리거될 때 데이터베이스 상태 검색에서 해당 상태를 알려줍니다. [SQL Server Always On 데이터베이스 상태 검색 장애 조치 옵션](sql-server-always-on-database-health-detection-failover-option.md)을 참조하세요.


Select Databases Page (New Availability Group Wizard and Add Database Wizard)  
  
##  <a name="related-tasks"></a><a name="LaunchWiz"></a> 관련 작업  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 그룹에 데이터베이스 추가 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
