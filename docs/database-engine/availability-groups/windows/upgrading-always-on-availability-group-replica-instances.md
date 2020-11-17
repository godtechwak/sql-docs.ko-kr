---
title: 가용성 그룹 복제본 업그레이드
description: 롤링 업그레이드를 수행하여 SQL Server 업그레이드 동안 주 복제본의 가동 중지 시간을 줄이는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 01/10/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: f670af56-dbcc-4309-9119-f919dcad8a65
author: cawrites
ms.author: chadam
ms.openlocfilehash: 6633eae12aa231b4b4a97b1c663d6b2e15339ee2
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583717"
---
# <a name="upgrading-always-on-availability-group-replica-instances"></a>Always On 가용성 그룹 복제본 인스턴스 업그레이드
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

Always On AG(가용성 그룹)를 호스트하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 신규 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 버전, 신규 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 팩 또는 누적 업데이트로 업그레이드하거나 신규 Windows 서비스 팩 또는 누적 업데이트를 설치하려는 경우 롤링 업그레이드를 수행하여 주 복제본을 단일 수동 장애 조치(failover)에만 적용하여 가동 중지 시간을 단축할 수 있습니다(또는 원본 주 복제본이 실패하는 경우 두 개의 수동 장애 조치(failover)). 업그레이드 프로세스 동안 읽기 전용 작업 또는 장애 조치(failover)에서는 보조 복제본을 사용할 수 없고 업그레이드 이후에는 주 복제본 노드에서의 작업 크기에 따라 보조 복제본이 주 복제본 노드를 따라잡기 위해서는 약간의 시간이 걸릴 수 있습니다(이로 인해 높은 네트워크 트래픽이 예상됨). 또한 최신 버전의 SQL Server를 실행하는 보조 복제본에 대한 초기 장애 조치(failover) 이후에, 가용성 그룹의 데이터베이스는 업그레이드 프로세스를 거쳐 최신 버전으로 업데이트됩니다. 이 기간 동안 이러한 데이터베이스에 대해 읽기가 가능한 복제본은 없습니다. 초기 장애 조치(failover) 후 가동 중지 시간은 가용성 그룹의 데이터베이스 수에 따라 달라집니다. 원래 주 데이터베이스로 장애 복구(failback)를 계획하는 경우, 이 단계는 장애 복구 시 반복되지 않습니다.
  
>[!NOTE]  
>이 문서는 SQL Server 업그레이드에 대한 설명으로 제한됩니다. WSFC(Windows Server Failover Cluster) 클러스터를 포함하는 운영 체제 업그레이드를 다루지 않습니다. Windows Server 2012 R2 이전의 운영 체제에서는 장애 조치(Failover) 클러스터를 호스팅하는 Windows 운영 체제 업그레이드가 지원되지 않습니다. Windows Server 2012 R2에서 실행되는 클러스터 노드를 업그레이드하려면 [클러스터 운영 체제 롤링 업그레이드](/windows-server/failover-clustering/cluster-operating-system-rolling-upgrade)를 참조하세요.  
  
## <a name="prerequisites"></a>필수 구성 요소  
시작하기 전에 다음과 같은 중요한 정보를 검토하십시오.  
  
- [지원되는 버전 및 에디션 업그레이드](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md): 사용 중인 Windows 운영 체제 버전 및 SQL Server 버전에서 SQL Server 2016으로 업그레이드할 수 있는지 확인합니다. 예를 들어, SQL Server 2005 인스턴스에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]로 직접 업그레이드할 수 없습니다.  
  
- [데이터베이스 엔진 업그레이드 방법 선택](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md): 올바른 순서로 업그레이드하려면 지원되는 버전 및 에디션 업그레이드에 대한 검토 및 환경에 설치된 기타 구성 요소를 기반으로 적합한 업그레이드 방법 및 단계를 선택합니다.  
  
- [데이터베이스 엔진 업그레이드 계획 및 테스트](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md): 릴리스 정보 및 알려진 업그레이드 문제, 업그레이드 전 검사 목록을 검토한 후 업그레이드 계획을 개발하고 테스트합니다.  
  
- [SQL Server 설치를 위한 하드웨어 및 소프트웨어 요구 사항](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md):  [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 설치를 위한 소프트웨어 요구 사항을 검토합니다. 추가 소프트웨어가 필요한 경우 가동 중지 시간을 최소화하기 위해 업그레이드 프로세스를 시작하기 전에 각 노드에 설치하십시오.  

- [변경 데이터 캡처 또는 복제가 AG 데이터베이스에 사용되는지 확인](#special-steps-for-change-data-capture-or-replication): CDC(변경 데이터 캡처)를 위해 AG의 데이터베이스가 활성화되어 있는 경우, 다음 [지침](#special-steps-for-change-data-capture-or-replication)을 완료합니다.

>[!NOTE]  
>동일한 AG의 SQL Server 인스턴스 혼합 버전은 롤링 업그레이드 외부에서 지원되지 않으며, 업그레이드가 신속하게 이루어져야 하므로 장기간 해당 상태로 있어서는 안됩니다. SQL Server 2016을 업그레이드하기 위한 다른 옵션은 분산 가용성 그룹을 사용하는 것입니다.

## <a name="rolling-upgrade-basics-for-always-on-ags"></a>Always On AG의 롤링 업그레이드 기본 사항  
서버 업그레이드 또는 업데이트를 수행할 때 AG의 가동 중단 시간 및 데이터 손실을 최소화하려면 다음과 같은 지침을 따르세요.  
  
- 롤링 업그레이드를 시작하기 전에  
  
    - 동기-커밋 복제본 인스턴스 중 하나 이상에서 수동 장애 조치(Failover)를 연습해 봅니다.  
  
    - 모든 가용성 데이터베이스에 대해 전체 데이터베이스 백업을 수행하여 데이터를 보호합니다.  
  
    - 모든 가용성 데이터베이스에서 DBCC CHECKDB를 실행합니다.  
  
-   항상 원격 보조 복제본을 먼저 업그레이드한 후 로컬 보조 복제본 인스턴스와 주 복제본 인스턴스 순으로 업그레이드합니다.  
  
-   업그레이드되고 있는 데이터베이스에 대한 백업은 발생할 수 없습니다.  보조 복제본을 업그레이드하기 전에 주 복제본에 대해서만 백업을 실행하도록 자동화된 백업 기본 설정을 구성합니다.  버전을 업그레이드하는 동안 백업을 위해 복제본을 읽거나 사용할 수 없습니다. 비-버전 업그레이드 동안 자동화 업데이트가 보조 복제본에서 실행되도록 구성한 후 주 복제본을 업그레이드할 수 있습니다.  
  
-   버전 업그레이드 동안 읽기 가능 보조 복제본은 읽기 가능 보조 복제본을 업그레이드한 후 및 주 복제본이 업그레이드된 보조 복제본으로 장애 조치(Failover)되거나 주 복제본이 업그레이드되기 이전에 읽을 수 없습니다.  
  
-   업그레이드 프로세스 동안 AG에서 의도하지 않은 장애 조치(failover)를 수행하지 않도록 시작하기 전에 모든 동기-커밋에서 가용성 장애 조치(failover)를 제거하세요.  
  
-   AG를 보조 복제본이 포함된 업그레이드된 인스턴스로 장애 조치(failover)하기 전에 주 복제본 인스턴스를 업그레이드해서는 안 됩니다. 그렇지 않으면 주 복제본 인스턴스에서 업그레이드를 진행하는 동안 클라이언트 애플리케이션의 작동 중단 시간이 길어질 수 있습니다.  
  
-   항상 AG를 동기-커밋 보조 복제본 인스턴스로 장애 조치(failover)합니다. 비동기-커밋 보조 복제본 인스턴스로 장애 조치(failover)하는 경우 데이터베이스가 데이터 손실에 취약해지고, 데이터 이동을 수동으로 다시 시작할 때까지 데이터 이동이 자동으로 중지됩니다.  
  
-   다른 보조 복제본 노드를 업그레이드하기 전에 주 복제본 인스턴스를 업그레이드해서는 안 됩니다. 업그레이드된 주 복제본은 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 인스턴스가 아직 같은 버전으로 업그레이드되지 않은 보조 복제본에 로그를 더 이상 전달할 수 없습니다. 보조 복제본으로 데이터 이동이 일시 중지된 경우 해당 복제본에 대한 자동 장애 조치(failover)를 수행할 수 없고 가용성 데이터베이스의 데이터가 손실될 수 있습니다. 이는 이전 주 복제본에서 새 주 복제본으로 수동으로 장애 조치하는 롤링 업그레이드 중에도 적용됩니다. 따라서 이전 주 복제본을 업그레이드한 후 동기화를 다시 시작해야 할 수 있습니다.
  
-   AG를 장애 조치(failover)하기 전에 장애 조치(failover) 대상의 동기화 상태가 SYNCHRONIZED인지 확인하세요.  

  > [!WARNING]
  > 이전 버전의 SQL Server가 설치된 서버에 새 인스턴스 또는 새 버전의 SQL Server를 설치하면 실수로 **이전 버전의 SQL Server에서 호스트되는 모든 가용성 그룹에 대한 가동 중단을 일으킬 수 있습니다.** 이는 SQL Server의 인스턴스나 버전을 설치하는 동안 SQL Server 고가용성 모듈(RHS.EXE)이 업그레이드되기 때문입니다. 이로 인해 서버의 주 역할에서 기존 가용성 그룹이 일시적으로 중단됩니다. 따라서 가용성 그룹이 있는 SQL Server의 이전 버전을 이미 호스팅하고 있는 시스템에 최신 버전의 SQL Server를 설치하는 경우 다음 중 하나를 수행하는 것이 좋습니다.
  > - 유지 관리 기간 동안 새 버전의 SQL Server를 설치합니다. 
  > - 가용성 그룹을 보조 복제본으로 장애 조치(failover)하므로 새 SQL Server 인스턴스를 설치하는 동안 기본 그룹이 아닙니다. 
  
## <a name="rolling-upgrade-process"></a>롤링 업그레이드 프로세스  
 실제로 정확한 프로세스는 AG의 배포 토폴로지 및 각 복제본의 커밋 모드와 같은 요소에 따라 달라집니다. 가장 간단한 시나리오는 다음 단계가 포함된 가장 간단한 형식의 다단계 프로세스로 롤링 업그레이드를 수행하는 것입니다.  
  
 ![HADR 시나리오의 AG 업그레이드](../../../database-engine/availability-groups/windows/media/alwaysonupgrade-ag-hadr.gif "HADR 시나리오의 AG 업그레이드")  
  
1.  모든 동기-커밋 복제본에서 자동 장애 조치(failover)를 제거합니다.  
  
2.  모든 비동기-커밋 보조 복제본 인스턴스를 업그레이드합니다. 
  
3.  모든 원격 비동기-커밋 보조 복제본 인스턴스를 업그레이드합니다. 

4.  모든 로컬 비동기-커밋 보조 복제본 인스턴스를 업그레이드합니다. 
  
4.  수동으로 AG를 새로 업그레이드된 로컬 동기-커밋 보조 복제본으로 장애 조치(failover)합니다.  
  
5.  이전에 주 복제본을 호스팅한 로컬 복제본 인스턴스를 업그레이드 또는 업데이트합니다.  
  
6.  자동 장애 조치(Failover) 파트너를 원하는 대로 구성합니다.
  
 필요한 경우 추가 수동 장애 조치(failover)를 수행하여 AG를 원래 구성으로 되돌릴 수 있습니다.  
 
   > [!NOTE]
   > - 동기-커밋 복제본을 업그레이드하고 오프라인으로 전환해도 주 복제본의 트랜잭션이 지연되지 않습니다. 보조 복제본의 연결이 해제되면 보조 복제본에서 로그가 강화될 때까지 기다리지 않고 트랜잭션이 복제복에서 커밋됩니다. 
   > - `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT`이 `1` 또는 `2`로 설정되면 업데이트 프로세스 중에 해당하는 수의 동기화 보조 복제복을 사용할 수 없는 경우 기본 복제본을 읽기/쓰기에 사용 못할 수도 있습니다. 
  
## <a name="ag-with-one-remote-secondary-replica"></a>원격 보조 복제본 하나가 포함된 AG  
 재해 복구용으로만 AG를 배포한 경우 AG를 비동기-커밋 보조 복제본으로 장애 조치(failover)해야 할 수 있습니다. 다음 그림에서는 이 구성을 보여 줍니다.  
  
 ![DR 시나리오의 AG 업그레이드](../../../database-engine/availability-groups/windows/media/agupgrade-ag-dr.gif "DR 시나리오의 AG 업그레이드")  
  
 이 경우 롤링 업그레이드 동안 AG를 비동기-커밋 보조 복제본으로 장애 조치(failover)해야 합니다. 데이터 손실을 방지하려면 AG를 장애 조치(failover)하기 전에 커밋 모드를 동기 커밋으로 변경하고 보조 복제본이 동기화될 때까지 기다리세요. 즉, 롤링 업그레이드 프로세스는 다음과 같습니다.  
  
1.  원격 사이트에서 보조 복제본 인스턴스 업그레이드  
  
2.  커밋 모드를 동기 커밋으로 변경  
  
3.  동기화 상태가 SYNCHRONIZED가 될 때까지 대기  
  
4.  AG를 원격 사이트의 보조 복제본으로 장애 조치(failover)  
  
5.  로컬 (주 사이트) 복제본 인스턴스 업그레이드 또는 업데이트  
  
6.  AG를 주 사이트로 다시 장애 조치(failover)  
  
7.  커밋 모드를 비동기 커밋으로 변경  
  
 동기-커밋 모드는 원격 사이트로 데이터 동기화에 권장되는 설정이 아니므로 설정 변경 후 클라이언트 애플리케이션에서 데이터베이스 대기 시간이 증가됨을 즉각적으로 알릴 수 있습니다. 또한 장애 조치(failover)를 수행하면 승인되지 않은 모든 로그 메시지가 삭제됩니다. 두 사이트 간 긴 네트워크 지연 시간으로 인해 삭제된 로그 메시지 수가 상당히 많아질 수 있고 이에 따라 방대한 양의 트랜잭션이 실패할 수 있습니다. 다음 작업을 수행하여 클라이언트 애플리케이션에 대한 영향을 최소화할 수 있습니다.  
  
-   클라이언트 트래픽이 낮을 때 유지 관리 기간을 신중하게 선택합니다.  
  
-   주 사이트에서 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 을(를) 업그레이드 또는 업데이트하는 동안 가용성 모드를 비동기 커밋으로 변경한 다음 주 사이트에 대한 장애 조치(failover)를 수행할 준비가 되면 동기 커밋으로 되돌립니다.  
  
## <a name="ag-with-failover-cluster-instance-nodes"></a>장애 조치(failover) 클러스터 인스턴스 노드가 포함된 AG  
 AG에 FCI(장애 조치(failover) 클러스터 인스턴스) 노드가 포함된 경우 활성 노드를 업그레이드하기 전에 비활성 노드를 업그레이드해야 합니다. 다음 그림에서는 로컬 고가용성을 위한 FCI 및 원격 재해 복구용 FCI 간 비동기 커밋과 함께 일반적인 AG 시나리오와 업그레이드 시퀀스를 설명합니다.  
  
 ![FCI를 사용하여 AG 업그레이드](../../../database-engine/availability-groups/windows/media/agupgrade-ag-fci-dr.gif "FCI를 사용하여 AG 업그레이드")  
  
1.  REMOTE2 업그레이드 또는 업데이트  
  
2.  FCI2를 REMOTE2로 장애 조치(Failover)  
  
3.  REMOTE1 업그레이드 또는 업데이트  
  
4.  PRIMARY2 업그레이드 또는 업데이트  
  
5.  FCI1을 PRIMARY2로 장애 조치(Failover)  
  
6.  PRIMARY1 업그레이드 또는 업데이트  
  
## <a name="upgrade-or-update-sql-server-instances-with-multiple-ags"></a>여러 AG가 있는 SQL Server 인스턴스 업그레이드 또는 업데이트  
 별도의 서버 노드(활성/비활성 구성)에서 주 복제본이 있는 여러 AG를 실행 중인 경우 프로세스 중에 고가용성을 유지하기 위해 업그레이드 경로에 더 많은 장애 조치(failover) 단계가 포함됩니다. 다음 표와 같이 3개의 서버 노드에서 3개의 AG를 실행하고 모든 복제본이 동기 커밋 모드에서 실행 중이라고 가정합니다.  
  
|AG|Node1|Node2|Node3|  
|------------------------|-----------|-----------|-----------|  
|AG1|주|||  
|AG2||주||  
|AG3|||주|  
  
 다음 시퀀스에서 부하 분산 롤링 업그레이드를 실행하기 위한 상황에 적합할 수 있습니다.  
  
1.  AG2를 Node3으로 장애 조치(Failover)(Node2를 확보하기 위함)  
  
2.  Node2 업그레이드 또는 업데이트  
  
3.  AG1을 Node2로 장애 조치(Failover)(Node1을 확보하기 위함)  
  
4.  Node1 업그레이드 또는 업데이트  
  
5.  AG2 및 AG3을 Node1로 장애 조치(Failover)(Node3을 확보하기 위함)  
  
6.  Node3 업그레이드 또는 업데이트  
  
7.  AG3을 Node3으로 장애 조치(Failover)  
  
 이 업그레이드 시퀀스에는 AG당 2번의 장애 조치(Failover)보다 적은 평균적인 작동 중단 시간이 발생합니다. 결과적인 구성이 아래 표에 표시됩니다.  
  
|AG|Node1|Node2|Node3|  
|------------------------|-----------|-----------|-----------|  
|AG1||주||  
|AG2|주|||  
|AG3|||주|  
  
 특정 구현에 따라 업그레이드 경로가 달라질 수 있으며 클라이언트 애플리케이션에 발생하는 작동 중지 시간도 달라질 수 있습니다.  
  
> [!NOTE]  
>  대부분의 경우에서 롤링 업그레이드가 완료된 후 원래 주 복제본에 대한 장애 복구가 수행됩니다. 

## <a name="rolling-upgrade-of-a-distributed-availability-group"></a>분산 가용성 그룹의 롤링 업그레이드
분산 가용성 그룹의 롤링 업그레이드를 수행하려면 먼저 모든 보조 복제본을 업그레이드합니다. 다음으로, 전달자를 장애 조치하고 두 번째 가용성 그룹의 마지막 남은 인스턴스를 업그레이드합니다. 다른 모든 복제본을 업그레이드하면 글로벌 주 복제본을 장애 조치하고, 첫 번째 가용성 그룹의 마지막 남은 인스턴스를 업그레이드합니다. 아래 단계에서 자세한 다이어그램이 제공됩니다. 

 특정 구현에 따라 업그레이드 경로가 달라질 수 있으며 클라이언트 애플리케이션에 발생하는 작동 중지 시간도 달라질 수 있습니다.  
  
> [!NOTE]  
>  대부분의 경우에서 롤링 업그레이드가 완료된 후에 원래 주 복제본에 대한 장애 복구가 수행됩니다. 

### <a name="general-steps-to-upgrade-a-distributed-availability-group"></a>분산 가용성 그룹을 업그레이드하는 일반적인 단계
1. 시스템 데이터베이스와 가용성 그룹에 참여한 데이터베이스를 포함한 모든 데이터베이스를 백업합니다. 
2. 두 번째 가용성 그룹(다운스트림)의 모든 보조 복제본을 업그레이드하고 다시 시작합니다. 
3. 첫 번째 가용성 그룹(업스트림)의 모든 보조 복제본을 업그레이드하고 다시 시작합니다. 
4. 보조 가용성 그룹의 업그레이드된 보조 복제본에 주 전달자를 장애 조치합니다.
5. 데이터 동기화가 될 때까지 기다립니다. 데이터베이스는 모든 동기-커밋 복제본에서 동기화된 것으로 표시되어야 하고 글로벌 주 복제본은 전달자와 동기화되어야 합니다.  
6. 보조 가용성 그룹의 마지막 남은 인스턴스를 업그레이드하고 다시 시작합니다. 
7. 첫 번째 가용성 그룹의 업그레이드된 보조 복제본에 글로벌 주 복제본을 장애 조치합니다.  
8. 주 가용성 그룹의 마지막 남은 인스턴스를 업그레이드합니다.
9. 새로 업그레이드된 서버를 다시 시작합니다. 
10. (선택 사항) 두 가용성 그룹을 다시 원래 주 복제본에 장애 복구합니다.  

>[!IMPORTANT]
>- 모든 단계 간의 동기화를 확인합니다. 다음 단계를 계속하기 전에 동기-커밋 복제본이 가용성 그룹 내에서 동기화되고 분산된 AG에서 전달자와 글로벌 주 복제본이 동기화되었는지를 확인합니다. 
>- **권장 사항**: 동기화를 확인할 때마다 SQL Server Management Studio에서 데이터베이스 노드 및 분산된 AG 노드를 모두 새로 고칩니다. 모든 항목이 동기화된 후에 각 복제본의 상태 스크린샷을 저장합니다. 그러면 수행 중인 단계를 추적하고, 다음 단계 전에 모든 항목이 제대로 작동한다는 증명을 제공하고, 문제가 발생하는 경우 문제를 해결하는 데 도움이 됩니다. 


### <a name="diagram-example-for-a-rolling-upgrade-of-a-distributed-availability-group"></a>분산 가용성 그룹의 롤링 업그레이드에 대한 다이어그램 예제

| 가용성 그룹 | 주 복제본 | 보조 복제본|
| :------ | :----------------------------- |  :------ |
| AG1 | NODE1\SQLAG | NODE2\SQLAG|
| AG2 | NODE3\SQLAG | NODE4\SQLAG|
| Distributedag| AG1(글로벌) | AG2(전달자) |
| &nbsp; | &nbsp; | &nbsp; |

![분산된 AG에 대한 예제 다이어그램](media/upgrading-always-on-availability-group-replica-instances/rolling-upgrade-dag-diagram.png)


이 다이어그램에서 인스턴스를 업그레이드하는 단계: 

1. 시스템 데이터베이스와 가용성 그룹에 참여한 데이터베이스를 포함한 모든 데이터베이스를 백업합니다. 
2. NODE4\SQLAG(AG2의 보조)를 업그레이드하고 서버를 다시 시작합니다. 
3. NODE2\SQLAG(AG1의 보조)를 업그레이드하고 서버를 다시 시작합니다. 
4. AG2를 NODE3\SQLAG에서 NODE4\SQLAG로 장애 조치합니다. 
5. NODE3\SQLAG를 업그레이드하고 서버를 다시 시작합니다. 
6. AG1을 NODE1\SQLAG에서 NODE2\SQLAG로 장애 조치합니다. 
7. NODE1\SQLAG를 업그레이드하고 서버를 다시 시작합니다. 
8. (선택 사항) 원래 주 복제본으로 장애 복구합니다.
    1. AG2를 NODE4\SQLAG에서 NODE3\SQLAG로 다시 장애 조치합니다.  
    2. AG1을 NODE2\SQLAG에서 NODE1\SQLAG로 다시 장애 조치합니다. 

세 번째 복제본이 각 가용성 그룹에 존재하는 경우 NODE3\SQLAG 및 NODE1\SQLAG 전에 업그레이드할 수 있습니다. 

>[!IMPORTANT]
>- 모든 단계 간의 동기화를 확인합니다. 다음 단계를 계속하기 전에 동기-커밋 복제본이 가용성 그룹 내에서 동기화되고 분산된 AG에서 전달자와 글로벌 주 복제본이 동기화되었는지를 확인합니다. 
>- 권장 사항: 동기화를 확인할 때마다 SQL Server Management Studio에서 데이터베이스 노드 및 분산된 AG 노드를 모두 새로 고칩니다. 모든 항목을 동기화하는 경우 스크린샷을 찍어 저장합니다. 그러면 수행 중인 단계를 추적하고, 다음 단계 전에 모든 항목이 제대로 작동한다는 증명을 제공하고, 문제가 발생하는 경우 문제를 해결하는 데 도움이 됩니다. 


## <a name="special-steps-for-change-data-capture-or-replication"></a>변경 데이터 캡처 또는 복제를 위한 특별한 단계

적용하는 업데이트에 따라 변경 데이터 캡처 또는 복제가 활성화된 AG 복제본 데이터베이스에 추가 단계가 필요할 수 있습니다. 업데이트에 대한 릴리스 정보를 참조하여 다음 단계가 필요한지 확인하세요.

1. 각 보조 복제본을 업그레이드합니다.

1. 모든 보조 복제본이 업그레이드된 후 AG를 업그레이드된 인스턴스로 장애 조치(failover)합니다. 

1. 주 복제본을 호스트하는 인스턴스에서 다음 Transact-SQL을 실행합니다.

   ```sql
   EXECUTE [master].[sys].[sp_vupgrade_replication];
   ```

   >[!NOTE]
   >이 명령을 실행하는 데 몇 분 정도 걸릴 수 있습니다. 

1. 원래 주 복제본이었던 인스턴스를 업그레이드합니다.

자세한 내용은 [최신 CU로 업그레이드한 후 CDC 기능이 중단될 수 있음](/archive/blogs/sql_server_team/cdc-functionality-may-break-after-upgrading-to-the-latest-cu-for-sql-server-2012-2014-and-2016)을 참조하세요.

  
## <a name="see-also"></a>참고 항목  
 [설치 마법사를 사용하여 SQL Server 2016으로 업그레이드&#40;설치 프로그램&#41;](../../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   

 [명령 프롬프트에서 SQL Server 2016 설치](../../install-windows/install-sql-server-from-the-command-prompt.md)  
  
