---
title: 가용성 그룹 장애 조치(failover)
description: SQL Server Management Studio, Transact-SQL 또는 SQL PowerShell을 사용하여 Always On 가용성 그룹의 계획된 장애 조치(failover)/강제 수동 장애 조치(failover)를 수행하는 방법을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.failoverwizard.connecttoreplicas.f1
- sql13.swb.failoverwizard.progress.f1
- sql13.swb.failoverwizard.selectnewprimary.f1
- sql13.swb.failoverwizard.f1
- sql13.swb.failoverwizard.confirmdataloss.f1
helpviewer_keywords:
- failover [SQL Server], failover
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], configuring
ms.assetid: 4a602584-63e4-4322-aafc-5d715b82b834
author: cawrites
ms.author: chadam
ms.openlocfilehash: a64554a84bc8e238a48058e3d9c925a5c2809057
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583517"
---
# <a name="use-the-fail-over-availability-group-wizard-sql-server-management-studio"></a>가용성 그룹 장애 조치(Failover) 마법사 사용(SQL Server Management Studio)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[tsql](../../../includes/tsql-md.md)], [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]또는 PowerShell을 사용하여 AlwaysOn 가용성 그룹에 대해 계획된 수동 장애 조치(failover) 또는 강제 수동 장애 조치(강제 장애 조치)를 수행하는 방법을 설명합니다. 가용성 그룹은 가용성 복제본의 수준에서 장애 조치(Failover)됩니다. SYNCHRONIZED 상태의 보조 복제본으로 장애 조치하는 경우 마법사는 계획된 수동 장애 조치(데이터가 손실되지 않음)를 수행합니다. UNSYNCHRONIZED 또는 NOT SYNCHRONIZING 상태의 보조 복제본으로 장애 조치하는 경우 마법사는 *강제 장애 조치*(데이터가 손실될 수 있음)로 강제 수동 장애 조치를 수행합니다. 두 형태의 수동 장애 조치는 현재 연결되어 있는 보조 복제본을 주 역할로 전환합니다. 계획된 수동 장애 조치는 이전의 주 복제본을 보조 역할로 전환합니다. 강제 장애 조치가 끝난 후 이전의 주 복제본은 온라인 상태가 되면 보조 역할로 전환됩니다.  

##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
 첫 번째 계획된 수동 장애 조치를 시작하기 전에 [가용성 그룹의 계획된 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)또는 PowerShell을 사용하여 AlwaysOn 가용성 그룹에 대해 계획된 수동 장애 조치(failover) 또는 강제 수동 장애 조치(강제 장애 조치)를 수행하는 방법을 설명합니다.  
  
 첫 번째 강제 장애 조치(failover)를 시작하기 전에 "시작하기 전 주의 사항" 및 "후속 작업: [가용성 그룹의 강제 수동 장애 조치(failover) 수행&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)의 강제 장애 조치(failover) 후의 필수 작업" 세션을 참조하세요.  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   장애 조치 명령은 대상 복제본에서 명령을 수락하는 즉시 반환하지만 데이터베이스 복구는 가용성 그룹의 장애 조치가 끝난 후 비동기로 수행됩니다.  
    
###  <a name="prerequisites-for-using-the-failover-availability-group-wizard"></a><a name="Prerequisites"></a> 가용성 그룹 장애 조치 마법사를 사용하기 위한 사전 요구 사항  
  
-   현재 사용할 수 있는 가용성 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 가용성 그룹에 대한 ALTER AVAILABILITY GROUP 권한, CONTROL AVAILABILITY GROUP 권한, ALTER ANY AVAILABILITY GROUP 권한 또는 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 그룹 장애 조치 마법사를 사용하려면**  
  
1.  개체 탐색기에서 장애 조치해야 할 가용성 그룹의 보조 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  가용성 그룹 장애 조치 마법사를 시작하려면 장애 조치할 가용성 그룹을 마우스 오른쪽 단추로 클릭하고 **장애 조치(Failover)** 를 선택합니다.  
  
4.  **소개** 페이지에 제공되는 정보는 보조 복제본에 대해 계획된 장애 조치를 수행할 수 있는지 여부에 따라 달라집니다. 페이지에 "**이 가용성 그룹에 대해 계획된 장애 조치(Failover)를 수행합니다.** "라고 표시되면 데이터 손실 없이 가용성 그룹을 장애 조치할 수 있습니다.  
  
5.  새로운 주 복제본( **장애 조치 대상** )이 될 보조 복제본을 선택하기 전에 *새로운 주 복제본 선택* 페이지에서 현재 주 복제본의 상태와 WSFC 쿼럼의 상태를 볼 수 있습니다. 계획된 수동 장애 조치를 수행할 경우 **장애 조치(Failover) 준비** 값이 "**데이터 손실 없음**"인 보조 복제본을 선택해야 합니다. 강제 장애 조치의 경우 가능한 모든 장애 조치 대상에 대해 이 값이 "**데이터 손실, 경고(** _#_ **)** "로 표시되며 여기서 *#* 는 지정된 보조 복제본에 대한 경고 수를 나타냅니다. 지정된 장애 조치 대상에 대한 경고를 보려면 해당 "장애 조치(Failover) 준비" 값을 클릭합니다.  
  
     자세한 내용은 이 항목의 뒷부분에 나오는 [새로운 주 복제본 선택 페이지](#SelectNewPrimaryReplica)를 참조하세요.  
  
6.  **복제본에 연결** 페이지에서 장애 조치 대상에 연결합니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [복제본에 연결 페이지](#ConnectToReplica)를 참조하세요.  
  
7.  강제 장애 조치를 수행하는 경우 **잠재적인 데이터 손실 확인** 페이지가 표시됩니다. 장애 조치를 계속하려면 **데이터가 손실될 가능성이 있는 장애 조치(Failover)를 확인하려면 여기를 클릭하세요.** 를 선택해야 합니다. 자세한 내용은 이 항목의 뒷부분에 나오는[잠재적인 데이터 손실 확인 페이지](#ConfirmPotentialDataLoss)를 참조하세요.  
  
8.  **요약** 페이지에서, 선택한 보조 복제본으로 장애 조치할 경우 발생할 영향을 검토합니다.  
  
     선택이 완료되었으면 필요에 따라 **스크립트** 를 클릭하여 마법사에서 실행할 단계에 대한 스크립트를 만들 수 있습니다. 그런 다음 가용성 그룹을 선택한 보조 복제본으로 장애 조치하려면 **마침** 을 클릭합니다.  
  
9. **진행률** 페이지에 가용성 그룹 장애 조치 진행률이 표시됩니다.  
  
10. 장애 조치 작업이 끝나면 **결과** 페이지에 결과가 표시됩니다. 마법사가 완료되면 **닫기** 를 클릭하여 종료합니다.  
  
     자세한 내용은 [결과 페이지&#40;Always On 가용성 그룹 마법사&#41;](../../../database-engine/availability-groups/windows/results-page-always-on-availability-group-wizards.md)또는 PowerShell을 사용하여 AlwaysOn 가용성 그룹에 대해 계획된 수동 장애 조치(failover) 또는 강제 수동 장애 조치(강제 장애 조치)를 수행하는 방법을 설명합니다.  
  
11. 강제 장애 조치(failover) 작업이 끝나면 "후속 작업: [가용성 그룹의 강제 수동 장애 조치(failover) 수행&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)의 강제 장애 조치(failover) 후의 필수 작업" 세션을 참조하세요.  
  
## <a name="help-for-pages-that-are-exclusive-to-this-wizard"></a>이 마법사에만 있는 페이지에 대한 도움말  
 이 섹션에서는 [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]에만 있는 페이지에 대해 설명합니다.  
  
 **섹션 내용**  
  
-   [새로운 주 복제본 선택 페이지](#SelectNewPrimaryReplica)  
  
-   [복제본에 연결 페이지](#ConnectToReplica)  
  
-   [잠재적인 데이터 손실 확인 페이지](#ConfirmPotentialDataLoss)  
  
 이외 이 마법사의 나머지 페이지는 하나 이상의 다른 Always On 가용성 그룹 마법사와 도움말을 공유하며 별도의 F1 도움말 항목에 문서화되어 있습니다.  
  
###  <a name="select-new-primary-replica-page"></a><a name="SelectNewPrimaryReplica"></a> Select New Primary Replica Page  
 이 섹션에서는 **새로운 주 복제본 선택** 페이지의 옵션에 대해 설명합니다. 이 페이지에서 가용성 그룹을 장애 조치할 대상 보조 복제본(장애 조치 대상)을 선택할 수 있습니다. 이 복제본은 새로운 주 복제본이 됩니다.  
  
#### <a name="page-options"></a>페이지 옵션  
 **현재 주 복제본**  
 현재 주 복제본의 이름을 표시합니다(복제본이 온라인 상태인 경우).  
  
 **주 복제본 상태**  
 현재 주 복제본의 상태를 표시합니다(복제본이 온라인 상태인 경우).  
  
 **쿼럼 상태**  
 'WSFC' 클러스터 유형의 경우 다음 중 하나의 가용성 복제본 쿼럼 상태를 표시합니다.  
  
   |값|Description|  
   |-----------|-----------------|  
   |**일반 쿼럼**|클러스터가 일반 쿼럼으로 시작했습니다.|  
   |**강제 쿼럼**|클러스터가 강제 쿼럼으로 시작했습니다.|  
   |**알 수 없는 쿼럼 상태**|클러스터 쿼럼 상태를 알 수 없습니다.|  
   |**해당 사항 없음**|가용성 복제본을 호스팅하는 노드에 쿼럼이 없습니다.|  
  
 자세한 내용은 [WSFC 쿼럼 모드 및 투표 구성&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-quorum-modes-and-voting-configuration-sql-server.md)을 참조하세요.  

 '없음' 클러스터 유형의 경우 쿼럼 상태가 적용되지 않습니다.

 '외부' 클러스터 유형의 경우 쿼럼 상태는 클러스터 관리자가 관리하며 SQL Server에는 표시되지 않습니다.
  
 **새로운 주 복제본 선택**  
 이 표에서 새로운 주 복제본으로 설정할 보조 복제본을 선택할 수 있습니다. 이 표의 열은 다음과 같습니다.  
  
 **서버 인스턴스**  
 보조 복제본을 호스팅하는 서버 인스턴스의 이름을 표시합니다.  
  
 **가용성 모드**  
 서버 인스턴스의 가용성 모드를 표시하며 다음 중 하나입니다.  
  
|값|Description|  
|-----------|-----------------|  
|**동기 커밋**|동기-커밋 모드에서는 동기-커밋 주 복제본이 트랜잭션을 커밋하기 전에 동기-커밋 보조 복제본이 로그 확정을 완료했음을 확인할 때까지 기다립니다. 동기-커밋 모드에서는 지정된 보조 데이터베이스가 주 데이터베이스와 동기화되고 나면 커밋된 트랜잭션이 완전히 보호됩니다.|  
|**비동기 커밋**|비동기-커밋 모드에서는 주 복제본이 비동기-커밋 보조 복제본이 로그를 확정할 때까지 기다리지 않고 트랜잭션을 커밋합니다. 비동기-커밋 모드에서는 보조 데이터베이스의 트랜잭션 대기 시간이 최소화되지만 보조 데이터베이스가 주 데이터베이스보다 뒤쳐질 수 있어 일부 데이터가 손실될 수 있습니다.|  
  
 자세한 내용은 [가용성 모드&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)라는 프로세스에서 서로 바꿀 수 있습니다.  
  
 **장애 조치(Failover) 모드**  
 서버 인스턴스의 장애 조치(failover) 모드를 표시하며 다음 중 하나입니다.  
  
|값|Description|  
|-----------|-----------------|  
|**자동**|자동 장애 조치(Failover)를 사용하도록 구성된 보조 복제본은 주 복제본과 동기활 때마다 계획된 수동 장애 조치도 지원합니다.|  
|**수동**|수동 장애 조치에는 계획된 장애 조치(데이터가 손실되지 않음)와 강제 장애 조치(데이터가 손실될 수 있음)의 두 가지 유형이 있습니다. 가용성 모드 및 동기-커밋 모드의 경우 보조 복제본의 동기화 상태에 따라 지정된 보조 복제본에 대해 이 두 가지 중 하나만 지원됩니다. 지정된 보조 복제본에 현재 지원되는 수동 장애 조치 형태를 확인하려면 이 표에서 **장애 조치(Failover) 준비** 열을 참조하세요.|  
  
 자세한 내용은 이 항목의 뒷부분에 나오는 [장애 조치(Failover) 및 장애 조치(Failover) 모드&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)를 참조하세요.  
  
 **장애 조치(Failover) 준비**  
 보조 복제본의 장애 조치 준비를 표시하며 다음 중 하나입니다.  
  
|값|Description|  
|-----------|-----------------|  
|**데이터 손실 없음**|이 보조 복제본이 현재 계획된 장애 조치를 지원합니다. 이 값은 동기-커밋 모드 보조 복제본이 현재 주 복제본과 동기화된 경우에만 표시됩니다.|  
|**데이터 손실, 경고(** _#_ **)**|이 보조 복제본이 현재 강제 장애 조치(데이터가 손실될 수 있음)를 지원합니다. 이 값은 보조 복제본이 주 복제본과 동기화되지 않은 상태일 때마다 표시됩니다. 가능한 데이터 손실에 대한 자세한 내용을 보려면 데이터 손실 경고 링크를 클릭하세요.|  
  
 **새로 고침**  
 표를 업데이트하려면 클릭합니다.  
  
 **취소**  
 마법사를 취소하려면 클릭합니다. **새로운 주 복제본 선택** 페이지에서 마법사를 취소하면 동작이 수행되지 않고 마법사가 종료됩니다.  
  
###  <a name="confirm-potential-data-loss-page"></a><a name="ConfirmPotentialDataLoss"></a> Confirm Potential Data Loss Page  
 이 섹션에서는 강제 장애 조치를 수행하는 경우에만 표시되는 **잠재적인 데이터 손실 확인** 페이지의 옵션에 대해 설명합니다. 이 항목은 [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]에만 사용됩니다. 이 페이지에서 데이터 손실의 위험을 감수하고 가용성 그룹을 강제 장애 조치할지 여부를 지정할 수 있습니다.  
  
#### <a name="confirm-potential-data-loss-options"></a>잠재적인 데이터 손실 확인 옵션  
 선택한 보조 복제본이 주 복제본과 동기화되어 있지 않은 경우 마법사는 이 보조 복제본으로 장애 조치할 경우 하나 이상의 데이터베이스에서 데이터가 손실될 수 있다는 경고를 표시합니다.  
  
 **데이터가 손실될 가능성이 있는 장애 조치(Failover)를 확인하려면 여기를 클릭하세요.**  
 데이터 손실의 위험을 감수하고 이 가용성 그룹의 데이터베이스를 사용하려면 이 확인란을 클릭합니다. 데이터가 손실되지 않도록 하려면 **이전** 을 클릭하여 **새로운 주 복제본 선택** 페이지로 돌아가거나 **취소** 를 클릭하여 가용성 그룹을 장애 조치하지 않고 마법사를 종료합니다.  
  
 **취소**  
 마법사를 취소하려면 클릭합니다. **잠재적인 데이터 손실 확인** 페이지에서 마법사를 취소하면 동작이 수행되지 않고 마법사가 종료됩니다.  
  
###  <a name="connect-to-replica-page"></a><a name="ConnectToReplica"></a> Connect to Replica Page  
 이 섹션에서는 **의** 복제본에 연결 [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]페이지에 있는 옵션에 대해 설명합니다. 이 페이지는 대상 보조 복제본에 연결되어 있지 않은 경우에만 표시됩니다. 이 페이지에서 새로운 주 복제본으로 선택한 보조 복제본에 연결할 수 있습니다.  
  
#### <a name="page-options"></a>페이지 옵션  
 **표 열:**  
 **서버 인스턴스**  
 가용성 복제본을 호스팅할 서버 인스턴스의 이름을 표시합니다.  
  
 **다음 계정으로 연결**  
 연결이 설정된 후에 서버 인스턴스에 연결되는 계정을 표시합니다. 이 열이 지정된 서버 인스턴스에 대해 "**연결되지 않음**"으로 표시되면 **연결** 단추를 클릭해야 합니다.  
  
 **연결**  
 이 서버 인스턴스가 연결해야 하는 다른 서버 인스턴스와 다른 계정으로 실행 중인 경우 클릭합니다.  
  
 **취소**  
 마법사를 취소하려면 클릭합니다. **복제본에 연결** 페이지에서 마법사를 취소하면 동작이 수행되지 않고 마법사가 종료됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 모드&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)   
 [장애 조치 및 장애 조치 모드&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md)   
 [가용성 그룹의 계획된 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)   
 [가용성 그룹의 강제 수동 장애 조치(Failover) 수행&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)   
 [강제 쿼럼을 통해 WSFC 재해 복구&#40;SQL Server&#41;](../../../sql-server/failover-clusters/windows/wsfc-disaster-recovery-through-forced-quorum-sql-server.md)  
  
