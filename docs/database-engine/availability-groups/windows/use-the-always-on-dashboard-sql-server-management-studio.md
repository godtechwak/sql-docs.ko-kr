---
title: SSMS에서 가용성 그룹 대시보드 사용
description: Always On 가용성 그룹 대시보드를 사용하여 SSMS(SQL Server Management Studio)에서 가용성 그룹의 상태를 모니터링하는 방법을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 08/09/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
- Availability Groups [SQL Server], dashboard
ms.assetid: c9ba2589-139e-42bc-99e1-94546717c64d
author: cawrites
ms.author: chadam
ms.openlocfilehash: 80b7f3e83af181676f09a6dc38b3652ae6142c89
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583665"
---
# <a name="use-the-always-on-availability-group-dashboard-sql-server-management-studio"></a>Always On 가용성 그룹 대시보드 사용(SQL Server Management Studio)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  데이터베이스 관리자는 Always On 가용성 그룹 대시보드를 사용하여 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 가용성 그룹과 해당 가용성 복제본 및 데이터베이스에 대한 상태를 한 눈에 볼 수 있습니다. 가용성 그룹 대시보드의 일반적인 몇 가지 용도는 다음과 같습니다.  
  
-   수동 장애 조치(failover)를 위한 복제본 선택    
-   장애 조치(failover)를 강제 실행하는 경우의 데이터 손실 예상  
-   데이터 동기화 성능 평가   
-   동기-커밋 보조 복제본의 성능 영향 평가 
  -  대시보드는 주요 가용성 그룹 상태 및 성과 지표를 제공하여 다음과 같은 유형의 정보를 통해 고가용성 작업 결정을 쉽게 내릴 수 있도록 합니다.  
-   복제본 롤업 상태    
-   동기화 모드 및 상태   
-   예상 데이터 손실    
-   예상 복구 시간(catchup 다시 실행)    
-   데이터베이스 복제본 정보    
-   동기화 모드 및 상태    
-   로그 복원 시간  
  
  
## <a name="prerequisites"></a>사전 요구 사항  
 가용성 그룹의 주 복제본 또는 보조 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스(서버 인스턴스)에 연결해야 합니다.  
  
 
### <a name="permissions"></a>사용 권한  
 연결, 서버 상태 보기 및 모든 정의 보기 권한이 필요합니다.  
  
##  <a name="to-start-the-always-on-dashboard"></a>Always On 대시보드를 시작하려면  
  
1.  개체 탐색기에서 Always On 대시보드를 실행할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  **Always On 고가용성** 노드를 확장하고 **가용성 그룹** 노드를 마우스 오른쪽 단추로 클릭한 다음 **대시보드 표시** 를 클릭합니다.  
  
##  <a name="change-always-on-dashboard-options"></a>Always On 대시보드 옵션 변경  
 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]**옵션** 대화 상자를 사용하여 자동 정의된 Always On 정책 자동 새로 고침 및 사용을 위한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Always On 대시보드 동작을 구성할 수 있습니다.  
  
1.  **도구** 메뉴에서 **옵션** 을 클릭합니다.  
  
2.  대시보드를 자동으로 새로 고치려면 **옵션** 대화 상자에서 **자동 새로 고침 설정** 을 선택하고 새로 고침 간격(초)을 입력한 다음 연결을 다시 시도할 횟수를 입력합니다.  
  
3.  사용자 정의 정책을 사용하도록 설정하려면 **사용자 정의 Always On 정책 사용** 을 선택합니다.  
  
##  <a name="availability-group-summary"></a>가용성 그룹 요약  
 가용성 그룹 화면에 연결된 서버 인스턴스가 복제본을 호스팅하는 각 가용성 그룹에 대한 요약 행을 표시합니다. 이 창에는 다음과 같은 열이 표시됩니다.  
  
 **가용성 그룹 이름**  
 연결된 서버 인스턴스에서 복제본을 호스팅하는 가용성 그룹의 이름입니다.  
  
 **주 인스턴스**  
 가용성 그룹의 주 복제본을 호스팅하는 서버 인스턴스의 이름입니다.  
  
 **장애 조치(Failover) 모드**  
 복제본이 구성되는 장애 조치(failover) 모드를 표시합니다. 가능한 장애 조치(failover) 모드 값은 다음과 같습니다.  
  
-   **자동**. 하나 이상의 복제본이 자동 장애 조치 모드임을 나타냅니다.  
  
-   **수동**. 자동 장애 조치 모드인 복제본이 없음을 나타냅니다.  
  
 **문제**  
 지정된 문제에 대한 문제 해결 설명서를 열려면 **문제** 링크를 클릭합니다. 모든 Always On 정책 문제 목록은 [Always On 가용성 그룹의 운영 문제에 대한 Always On 정책&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)을 참조하세요.  
  
> [!TIP]  
>  열 머리글을 클릭하여 가용성 그룹, 주 인스턴스, 장애 조치(failover) 모드 또는 문제의 이름을 기준으로 가용성 그룹 정보를 정렬할 수 있습니다.  
  
##  <a name="availability-group-details"></a><a name="AvGroupDetails"></a> 가용성 그룹 정보  
 요약 화면에서 선택하는 가용성 그룹에 대한 다음 정보가 표시됩니다.  
  
 **가용성 그룹 상태**  
 가용성 그룹의 상태를 표시합니다.  
  
 **Primary instance**  
 가용성 그룹의 주 복제본을 호스팅하는 서버 인스턴스의 이름입니다.  
  
 **Failover mode**  
 복제본이 구성되는 장애 조치(failover) 모드를 표시합니다. 가능한 장애 조치(failover) 모드 값은 다음과 같습니다.  
  
-   **자동**. 하나 이상의 복제본이 자동 장애 조치 모드임을 나타냅니다.  
  
-   **수동**. 자동 장애 조치 모드인 복제본이 없음을 나타냅니다.  
  
 **클러스터 상태**  
 연결된 서버의 인스턴스와 가용성 그룹이 구성원 노드인 클러스터의 이름과 상태입니다.  
  
##  <a name="availability-replica-details"></a><a name="AvReplicaDetails"></a> 가용성 복제본 정보  

주 복제본에 연결하는 경우 **가용성 복제본 정보** 는 가용성 그룹에 있는 모든 복제본의 정보를 보여 줍니다. 보조 복제본에 연결되면 화면에는 연결된 복제본의 정보만 표시됩니다.  

**가용성 복제본** 창에 다음 열이 표시됩니다.  
  
 **이름**  
 가용성 복제본을 호스팅하는 서버 인스턴스의 이름입니다. 이 열은 기본적으로 표시됩니다.  
  
 **역할**  
 가용성 복제본의 현재 역할( **주** 또는 **보조**)을 나타냅니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 역할에 대한 자세한 내용은 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)를 참조하세요. 이 열은 기본적으로 표시됩니다.  
  
 **장애 조치(Failover) 모드**  
 복제본이 구성되는 장애 조치(failover) 모드를 표시합니다. 가능한 장애 조치(failover) 모드 값은 다음과 같습니다.  
  
-   **자동**. 하나 이상의 복제본이 자동 장애 조치 모드임을 나타냅니다.  
  
-   **수동**. 자동 장애 조치 모드인 복제본이 없음을 나타냅니다.  
  
 **동기화 상태**  
 보조 복제본이 주 복제본에 현재 동기화되어 있는지 여부를 나타냅니다. 이 열은 기본적으로 표시됩니다. 사용 가능한 값은  
  
-   **동기화되지 않음**. 복제본에 있는 하나 이상의 데이터베이스가 동기화되지 않았거나 가용성 그룹에 아직 조인되지 않았습니다.  
  
-   **동기화 중**. 복제본에 있는 하나 이상의 데이터베이스가 동기화되고 있습니다.  
  
-   **동기화됨**. 보조 복제본에 있는 모든 데이터베이스가 현재 주 복제본 또는 마지막 주 복제본(있는 경우)의 해당 주 데이터베이스와 동기화되어 있습니다.  
  
    > [!NOTE]  
    >  성능 모드에서는 데이터베이스가 절대 Synchronized 상태로 되지 않습니다.  
  
-   **NULL**. 알 수 없는 상태입니다. 이 값은 로컬 서버 인스턴스가 WSFC 장애 조치(Failover) 클러스터와 통신할 수 없는 경우(즉, 로컬 노드가 WSFC 쿼럼의 일부가 아닌 경우)에 발생합니다.  
  
 **문제**  
 문제 이름을 나열합니다. 이 값은 기본적으로 표시됩니다. 모든 Always On 정책 문제 목록은 [Always On 가용성 그룹의 운영 문제에 대한 Always On 정책&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)을 참조하세요.  
  
 **가용성 모드**  
 각 가용성 복제본에 대해 별도로 설정한 복제본 속성을 나타냅니다. 이 값은 기본적으로 숨겨집니다. 사용 가능한 값은  
  
-   **비동기**. 보조 복제본이 주 복제본과 동기화되지 않습니다.  
  
-   **Synchronous**: 주 데이터베이스에 catchup할 때 보조 데이터베이스가 이 상태로 전환되고 데이터베이스에 대해 데이터 동기화가 지속되는 동안 catchup 상태를 유지합니다.  
  
 **주 연결 모드**  
 주 복제본에 연결하는 데 사용되는 모드를 나타냅니다.  이 값은 기본적으로 숨겨집니다.  
  
 **보조 연결 모드**  
 보조 복제본에 연결하는 데 사용되는 모드를 나타냅니다.  이 값은 기본적으로 숨겨집니다.  
  
 **연결 상태**  
 보조 복제본이 주 복제본에 현재 연결되어 있는지 여부를 나타냅니다. 이 열은 기본적으로 숨겨집니다. 사용 가능한 값은  
  
-   **연결 끊김**. 원격 가용성 복제본의 경우 로컬 가용성 복제본에서 연결이 끊어져 있는지를 나타냅니다. 연결이 끊긴 상태에 대한 로컬 복제본의 응답은 역할별로 다음과 같이 다릅니다.  
  
    -   주 복제본에서 보조 복제본의 연결이 끊어지면 보조 데이터베이스는 주 복제본에 **동기화되지 않음** 으로 표시되고 주 복제본은 보조 복제본이 다시 연결될 때까지 기다립니다.  
  
    -   보조 복제본에서 보조 복제본의 연결이 끊어지면 보조 복제본은 주 복제본에 다시 연결하려고 시도합니다.  
  
-   **Connected**. 로컬 복제본에 현재 연결되어 있는 원격 가용성 복제본입니다.  
  
 **작동 상태**  
 보조 복제본의 현재 작동 상태를 나타냅니다. 이 값은 기본적으로 숨겨집니다. 사용 가능한 값은  
  
 **0**. 장애 조치(failover) 보류 중    
 **1**. 보류 중    
 **2**. 온라인    
 **3**. 오프라인   
 **4**. 실패    
 **5**. 실패, 쿼럼 없음  
  
 **NULL**. 복제본이 로컬이 아님  
  
 **마지막 연결 오류 번호**  
 마지막 연결 오류의 번호입니다.  이 값은 기본적으로 숨겨집니다.  
  
 **마지막 연결 오류 설명**  
 마지막 연결 오류에 대한 설명입니다.  이 값은 기본적으로 숨겨집니다.  
  
 **마지막 연결 오류 타임스탬프**  
 마지막 연결 오류의 타임스탬프입니다. 이 값은 기본적으로 숨겨집니다.  
  
> [!NOTE]  
>  가용성 복제본의 성능 카운터에 대한 자세한 내용은 [SQL Server, 가용성 복제본](../../../relational-databases/performance-monitor/sql-server-availability-replica.md)을 참조하세요.  
  
##  <a name="group-by-availability-group-information"></a>가용성 그룹 정보에 따른 그룹화  
 정보를 그룹화하려면 **그룹화 방법** 을 클릭하고 다음 중 하나를 선택합니다.  
  
-   **가용성 복제본**    
-   **가용성 데이터베이스** 
-   **Synchronization state**  
-   **장애 조치(Failover) 준비**   
-   **문제**  
  
 그룹화된 정보를 표시하는 창에 다음 열이 표시됩니다.  
  
 **이름**  
 가용성 데이터베이스의 이름입니다. 이 값은 기본적으로 표시됩니다.  
  
 **복제본**  
 가용성 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인스턴스 이름입니다. 이 값은 기본적으로 표시됩니다.  
  
 **동기화 상태**  
 가용성 데이터베이스가 주 복제본에 현재 동기화되어 있는지 여부를 나타냅니다. 이 값은 기본적으로 표시됩니다. 가능한 동기화 상태는 다음과 같습니다.  
  
-   **비동기화 중**:  
-   
    -   주 역할의 경우 데이터베이스에서 트랜잭션 로그를 해당 보조 데이터베이스와 동기화할 준비가 되지 않았음을 나타냅니다.   
    -   보조 데이터베이스의 경우 데이터베이스에서 연결 문제로 인해 로그 동기화를 시작하지 않았거나 데이터베이스가 일시 중지되었거나, 시작 중에 전환 상태를 진행하고 있거나 역할 전환 중임을 나타냅니다.  
  
-   **동기화 중**:
- 주 복제본에서:   
    - 주 데이터베이스에서 이 데이터베이스가 보조 데이터베이스의 검색 요청을 받을 준비가 되었음을 나타냅니다.  
    - 보조 복제본에서 해당 보조 데이터베이스에 대해 진행 중인 활성 데이터 이동이 있음을 나타냅니다. 
  
  
-   **동기화됨**: 
  
    - 주 데이터베이스의 경우 하나 이상의 보조 데이터베이스가 동기화되었음을 나타냅니다.
    - 보조 데이터베이스의 경우 데이터베이스가 해당 주 데이터베이스와 동기화되었음을 나타냅니다.  
  
-   **되돌리는 중**.  
  
     보조 데이터베이스가 주 데이터베이스에서 페이지 가져오기를 현재 진행 중인 경우의 실행 취소 프로세스의 단계를 나타냅니다.  
  
    > [!CAUTION]  
    >  데이터베이스가 REVERTING 상태일 때 보조 복제본에 대한 장애 조치를 강제로 실행하면 해당 데이터베이스가 시작할 수 없는 상태로 될 수 있습니다.  
  
-   **초기화 중**.  
  
     보조 데이터베이스에서 실행 취소 LSN을 catch하는 데 필요한 트랜잭션 로그가 보조 복제본에서 제공되고 확정 중인 경우의 실행 취소 단계를 나타냅니다.  
  
    > [!CAUTION]  
    >  데이터베이스가 INITIALIZING 상태일 때 보조 복제본에 대한 장애 조치를 강제로 실행하면 해당 데이터베이스가 시작할 수 없는 상태로 될 수 있습니다.  
  
 **장애 조치(Failover) 준비**  
 잠재적인 데이터 손실을 발생 또는 발생하지 않고 장애 조치할 수 있는 가용성 복제본을 나타냅니다. 이 열은 기본적으로 표시됩니다. 사용 가능한 값은  
  
-   **데이터 손실**   
-   **데이터 손실 없음**  
  
 **문제**  
 문제 이름을 나열합니다. 이 열은 기본적으로 표시됩니다. 사용 가능한 값은  
  
-   **경고**. 임계값 및 경고 문제를 표시하려면 클릭합니다.   
-   **심각**. 심각한 문제를 표시하려면 클릭합니다.  
  
 모든 Always On 정책 문제 목록은 [Always On 가용성 그룹의 운영 문제에 대한 Always On 정책&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-policies-for-operational-issues-always-on-availability.md)을 참조하세요.  
  
 **일시 중지됨**  
 데이터베이스가 **일시 중지됨** 상태인지 아니면 **재개됨** 상태인지 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **일시 중지 원인**  
 일시 중지됨 상태에 대한 이유를 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **예상 데이터 손실(초)**  
 주 복제본과 보조 복제본에서 마지막 트랜잭션 로그 레코드의 시간 차이를 나타냅니다. 주 복제본이 실패하는 경우 시간 창 내의 모든 트랜잭션 로그 레코드가 손실됩니다. 이 값은 기본적으로 숨겨집니다.  
  
 **예상 복구 시간(초)**  
 catchup 시간을 다시 실행하는 데 걸리는 시간(초)을 나타냅니다. *catch-up 시간* 은 보조 복제본이 주 복제본을 따라잡기 위해 걸리는 시간입니다. 이 값은 기본적으로 숨겨집니다.  
  
 **동기화 성능(초)**  
 주 복제본과 보조 복제본을 동기화하는 데 걸리는 시간(초)을 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **로그 전송 큐 크기(KB)**  
 보조 복제본으로 전송되지 않은 주 데이터베이스의 로그 파일에 있는 로그 레코드 수를 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **로그 전송 속도(KB/초)**  
 로그 레코드를 보조 복제본으로 전송하는 속도(KB/초)를 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **Redo Queue 크기(KB)**  
 아직 다시 실행되지 않은 보조 복제본의 로그 파일에 있는 로그 레코드 수를 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **다시 실행 속도(KB/초)**  
 로그 레코드를 다시 실행하는 속도(KB/초)를 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **파일 스트림 전송 속도(KB/초)**  
 트랜잭션을 복제본으로 전송 중인 파일 스트림의 속도(KB/초)를 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **로그 LSN의 끝**  
 주 복제본과 보조 복제본의 로그 캐시에 있는 마지막 로그 레코드에 해당하는 실제 LSN(로그 시퀀스 번호)을 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **복구 LSN**  
 복제본이 주 복제본에서 복구 또는 장애 조치(failover) 후 새 로그 레코드를 쓰기 전의 트랜잭션 로그 끝을 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **잘림 LSN**  
 주 복제본에 대한 최소 로그 잘림 값을 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **마지막 커밋 LSN**  
 트랜잭션 로그의 마지막 커밋 레코드에 해당하는 실제 LSN을 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **마지막 커밋 시간**  
 마지막 커밋 레코드에 해당하는 시간을 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **마지막 전송 LSN**  
 모든 로그 블록이 주 복제본에 의해 전송된 지점을 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **마지막 전송 시간**  
 마지막 로그 블록이 전송된 시간을 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **마지막으로 받은 LSN**  
 보조 데이터베이스를 호스팅하는 보조 복제본이 모든 로그 블록을 받은 지점을 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **마지막으로 받은 시간**  
 보조 복제본에서 마지막으로 받은 메시지의 로그 블록 식별자를 읽은 시간을 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **마지막으로 확정된 LSN**  
 모든 로그 블록이 보조 복제본의 디스크에 플러시된 지점을 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **마지막으로 확정된 시간**  
 보조 복제본에서 마지막으로 확정된 LSN에 대한 로그 블록 식별자를 수신한 시간을 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **마지막으로 다시 실행된 LSN**  
 보조 복제본에서 마지막으로 다시 실행된 로그 레코드의 실제 LSN을 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
  
 **마지막으로 다시 실행된 시간**  
 보조 데이터베이스에서 마지막 로그 레코드가 다시 실행된 시간을 나타냅니다. 이 값은 기본적으로 숨겨집니다.  
 

   > [!NOTE]  
   >  대부분의 데이터는 sys.dm_hadr_database_replica_states를 기반으로 하므로 일부 제한 사항이 적용될 수 있습니다. 자세한 내용은 [sys.dm_hadr_database_replica_states(Transact-SQL)](../../../relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)를 참조하세요.


## <a name="always-on-availability-group-latency-reports"></a>Always On 가용성 그룹 대기 시간 보고서
가용성 그룹 대기 시간 보고서는 가용성 그룹 대시보드에 기본 제공되는 보고 도구이며 [SQL Server Management Studio 17.4](../../../ssms/download-sql-server-management-studio-ssms.md) 릴리스에서 사용할 수 있습니다. 이 기능은 로그 전송 프로세스의 다양한 단계에서 소요된 시간을 자세히 설명하는 이해하기 쉬운 보고서를 제공합니다. 이를 통해 동기화 프로세스 중 대기 시간의 잠재적 원인을 줄이는 방법을 제공합니다. 

SQL 에이전트는 데이터 수집을 실행하고 주 복제본과 보조 복제본 중 하나 이상에서 사용할 수 있어야 합니다. SQL Server Management Studio의 **개체 탐색기** 에서 가용성 그룹 > 보고서 > 표준 보고서를 마우스 오른쪽 단추로 클릭하여 보고서를 봅니다.  

자세한 내용은 [Always On 가용성 그룹 대기 시간 보고서](/archive/blogs/sql_server_team/new-in-ssms-always-on-availability-group-latency-reports)를 참조하세요.

## <a name="related-tasks"></a>관련 작업  
  
-   [Always On 정책을 사용하여 가용성 그룹의 상태 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/use-always-on-policies-to-view-the-health-of-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [sys.dm_os_performance_counters&#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)   
 [가용성 그룹 모니터링&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/monitoring-of-availability-groups-sql-server.md)  
  
