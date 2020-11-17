---
title: 가용성 그룹 내의 복제본에 대한 클라이언트 연결 유형
description: 클라이언트가 SQL Server 내의 Always On 가용성 그룹의 주 복제본 또는 보조 복제본으로 만들 수 있는 다양한 유형의 연결에 대해 알아봅니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], client connectivity
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 29027e46-43e4-4b45-b650-c4cdeacdf552
author: cawrites
ms.author: chadam
ms.openlocfilehash: 12d7db7b49c15954240843b13d750ea1d64503f3
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584920"
---
# <a name="types-of-client-connections-to-replicas-within-an-always-on-availability-group"></a>Always On 가용성 그룹 내의 복제본에 대한 클라이언트 연결 유형
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Always On 가용성 그룹에서 보조 역할 즉, 보조 복제본으로 실행되는 동안 읽기 전용 연결을 허용하도록 하나 이상의 가용성 복제본을 구성할 수 있습니다. 주 역할 즉, 주 복제본으로 실행되는 동안 읽기 전용 연결을 허용하거나 제외하도록 각 가용성 복제본을 구성할 수도 있습니다.  
  
 지정된 가용성 그룹의 주 또는 보조 데이터베이스에 클라이언트가 쉽게 액세스할 수 있도록 하려면 가용성 그룹 수신기를 정의해야 합니다. 기본적으로 가용성 그룹 수신기는 들어오는 연결을 주 복제본으로 전달합니다. 그러나 읽기 전용 라우팅만 지원하도록 가용성 그룹을 구성할 수 있습니다. 그러면 가용성 그룹 수신기가 읽기 전용 애플리케이션의 연결 요청을 읽기 가능한 보조 복제본으로 리디렉션합니다. 자세한 내용은 이 항목 뒷부분에 있는 [가용성 그룹에 대한 읽기 전용 라우팅 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)와 같은 시스템 데이터베이스, 사용자 데이터베이스를 비롯하여 보조 복제본을 호스트하는 서버 인스턴스의 읽기/쓰기 데이터베이스에는 데이터를 쓸 수 있습니다.  
  
 장애 조치(failover) 중에 보조 복제본은 주 역할로 전환되고 이전의 주 복제본은 보조 역할로 전환됩니다. 장애 조치(failover) 프로세스 동안 주 복제본 및 보조 복제본에 대한 모든 클라이언트 연결은 종료됩니다. 장애 조치(failover) 후 클라이언트가 가용성 그룹 수신기에 다시 연결할 때 수신기는 읽기 전용 연결 요청을 제외하고 새로운 주 복제본에 클라이언트를 다시 연결합니다. 새로운 주 복제본을 호스팅하는 클라이언트 및 서버 인스턴스와 최소 하나 이상의 읽기 가능한 보조 복제본에서 읽기 전용 라우팅이 구성되어 있는 경우 읽기 전용 연결 요청은 클라이언트에 필요한 연결 액세스 유형을 지원하는 보조 복제본으로 다시 라우팅됩니다. 장애 조치(failover) 후 정상적인 클라이언트 환경을 위해 모든 가용성 복제본의 보조 역할 및 주 역할에 대해 연결 액세스를 구성해야 합니다.  
  
> [!NOTE]  
>  클라이언트 연결 요청을 처리하는 가용성 그룹 수신기에 대한 자세한 내용은 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)을 참조하세요.  
  
##  <a name="types-of-connection-access-supported-by-the-secondary-role"></a><a name="ConnectAccessForSecondary"></a> 보조 역할에서 지원되는 연결 액세스의 유형  
 보조 역할은 클라이언트 연결에 대해 다음과 같은 세 가지 대체 방법을 지원합니다.  
  
 연결 없음  
 사용자 연결이 허용되지 않습니다. 보조 데이터베이스를 읽기 액세스에 사용할 수 없습니다. 이 항목은 보조 역할의 기본 동작입니다.  
  
 읽기 전용 연결만  
 **애플리케이션 의도** 연결 속성이 **ReadOnly** (*읽기 전용 연결*)로 설정된 연결에만 보조 데이터베이스를 사용할 수 있습니다.  
  
 이 연결 속성에 대한 자세한 내용은 [고가용성 재해 복구를 위한 SQL Server Native Client 지원](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)을 참조하세요.  
  
 읽기 전용 연결 허용  
 모든 보조 데이터베이스는 읽기 액세스 연결에 사용할 수 있습니다. 이 옵션을 선택하면 낮은 버전의 클라이언트가 연결할 수 있습니다.  
  
 자세한 내용은 [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)가 있어야 합니다.  
  
##  <a name="types-of-connection-access-supported-by-the-primary-role"></a><a name="ConnectAccessForPrimary"></a> 주 역할에서 지원되는 연결 액세스의 유형  
 주 역할은 클라이언트 연결에 대해 다음과 같은 두 가지 대체 방법을 지원합니다.  
  
 모든 연결이 허용됩니다.  
 주 데이터베이스에 읽기/쓰기 및 읽기 전용 연결이 모두 허용됩니다. 이 항목은 주 역할의 기본 동작입니다.  
  
 읽기/쓰기 연결만 허용  
 **애플리케이션 의도** 연결 속성을 설정하지 않거나 **ReadWrite** 로 설정하면 연결이 허용됩니다. **Application Intent** 연결 문자열 키워드를 **ReadOnly** 로 설정하는 연결은 허용되지 않습니다. 읽기/쓰기 연결을 허용하면 고객이 읽기 전용 작업 로드를 주 복제본에 실수로 연결하지 않도록 할 수 있습니다.  
  
 이 연결 속성에 대한 자세한 내용은 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하세요.  
  
 자세한 내용은 [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)가 있어야 합니다.  
  
##  <a name="how-the-connection-access-configuration-affects-client-connectivity"></a><a name="HowConnectionAccessAffectsConnectivity"></a> 연결 액세스 구성이 클라이언트 연결에 미치는 영향  
 복제본의 연결 액세스 설정에 따라 연결 시도가 실패하는지 또는 성공하는지가 결정됩니다. 다음 표에는 지정된 연결 시도의 각 연결 액세스 설정에 대한 성공 여부가 요약되어 있습니다.  
  
|복제본 역할|복제본에서 지원되는 연결 액세스|연결 의도|연결 시도 결과|  
|------------------|--------------------------------------------|-----------------------|--------------------------------|  
|보조|모두|읽기 전용, 읽기/쓰기 또는 연결 의도가 지정되지 않음|Success|  
|보조|없음(기본 보조 동작)|읽기 전용, 읽기/쓰기 또는 연결 의도가 지정되지 않음|실패|  
|보조|읽기 전용만|읽기 전용|Success|  
|보조|읽기 전용만|읽기/쓰기 또는 연결 의도가 지정되지 않음|실패|  
|주|모두(기본 주 동작)|읽기 전용, 읽기/쓰기, 또는 연결 의도가 지정되지 않음|Success|  
|주|읽기/쓰기|읽기 전용만|실패|  
|주|읽기/쓰기|읽기/쓰기 또는 연결 의도가 지정되지 않음|Success|  
  
 해당 복제본에 대한 클라이언트 연결을 허용하도록 가용성 그룹을 구성하는 방법은 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)을 참조하세요.  
  
### <a name="example-connection-access-configuration"></a>연결 액세스 구성의 예  
 구성 액세스에 대해 가용성 복제본을 구성하는 방법에 따라 가용성 그룹이 장애 조치된 후 클라이언트 연결에 대한 지원이 변경될 수 있습니다. 예를 들어 원격 비동기 커밋 보조 복제본에서 보고가 수행되는 가용성 그룹의 경우, 모든 읽기 전용 연결이 읽기 전용 연결이 되도록 이 가용성 그룹의 데이터베이스에 대한 모든 읽기 전용 애플리케이션은 **애플리케이션 의도** 연결 속성을 **ReadOnly** 로 설정합니다.  
  
 이 예에서 가용성 그룹은 메인 컴퓨팅 센터에 두 개의 동기-커밋 복제본이 있고 위성 사이트에 두 개의 비동기-커밋 복제본이 있습니다. 주 역할에 대해 모든 복제본은 읽기/쓰기 액세스용으로 구성되므로 모든 상황에서 주 복제본에 대한 읽기 전용 연결은 수행할 수 없습니다. 동기 커밋 보조 역할은 기본 연결 액세스 구성("없음")을 사용하므로 보조 역할로는 모든 클라이언트 연결을 수행할 수 없습니다.  반대로 비동기 커밋 복제본은 보조 역할에서 읽기 전용 연결을 허용하도록 구성됩니다. 다음 표에는 이러한 구성 예가 요약되어 있습니다.  
  
|복제본|커밋 모드|초기 역할|보조 역할에 대한 연결 액세스|주 역할에 대한 연결 액세스|  
|-------------|-----------------|------------------|------------------------------------------|----------------------------------------|  
|Replica1|동기|주|None|읽기/쓰기|  
|Replica2|동기|보조|None|읽기/쓰기|  
|Replica3|비동기|보조|읽기 전용만|읽기/쓰기|  
|Replica4|비동기|보조|읽기 전용만|읽기/쓰기|  
  
 일반적으로 이 시나리오 예에서는 동기-커밋 복제본 사이에서만 장애 조치(failover)가 수행되며 장애 조치(failover) 후 즉시 읽기 전용 애플리케이션이 비동기-커밋 보조 복제본 중 하나에 다시 연결할 수 있습니다. 그러나 메인 컴퓨팅 센터에 재해가 발생할 경우 동기-커밋 복제본은 모두 손실됩니다. 위성 사이트의 데이터베이스 관리자는 비동기-커밋 보조 복제본에 강제 수동 장애 조치(failover)를 수행하여 응답합니다. 나머지 보조 복제본의 보조 데이터베이스는 강제 장애 조치(failover)에 따라 일시 중지되므로 읽기 전용 작업 로드에 사용할 수 없습니다. 읽기/쓰기 연결용으로 구성된 새로운 주 복제본에서는 읽기 전용 작업 로드가 읽기/쓰기 작업 로드와 경쟁할 수 없습니다. 따라서 데이터베이스 관리자가 나머지 비동기-커밋 보조 복제본에서 보조 데이터베이스를 재개할 때까지 읽기 전용 클라이언트는 가용성 복제본에 연결할 수 없습니다.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [가용성 그룹에 대한 읽기 전용 라우팅 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
-   [가용성 그룹 모니터링&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)  
  
-   [가용성 복제본 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-replica-properties-sql-server.md)  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 관련 내용  
  
-   [고가용성 및 재해 복구를 위한 Microsoft SQL Server Always On 솔루션 가이드](/previous-versions/sql/sql-server-2012/hh781257(v=msdn.10))  
  
-   [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](/archive/blogs/sqlalwayson/)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)   
 [통계](../../../relational-databases/statistics/statistics.md)  
  
