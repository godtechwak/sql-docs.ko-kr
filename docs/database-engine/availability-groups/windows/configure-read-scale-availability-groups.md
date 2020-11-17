---
title: 가용성 그룹에 대한 읽기 확장 구성
description: Windows에서 읽기 확장 워크로드에 대한 SQL Server Always On 가용성 그룹을 구성하는 방법을 알아봅니다.
ms.custom: seodec18
author: cawrites
ms.author: chadam
ms.reviewer: ''
ms.date: 05/24/2018
ms.topic: how-to
ms.prod: sql
ms.technology: high-availability
ms.openlocfilehash: c5029f8f6e2200751d193172322d7d84934271ab
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584512"
---
# <a name="configure-read-scale-for-an-always-on-availability-group"></a>Always On 가용성 그룹에 대한 읽기 확장 구성

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

Windows에서 읽기 배율 작업에 대한 SQL Server Always On 가용성 그룹을 구성할 수 있습니다. 가용성 그룹에 대한 아키텍처는 다음과 같은 두 종류가 있습니다.
* 고가용성을 위한 아키텍처는 클러스터 관리자를 사용하여 향상 된 비즈니스 연속성을 제공하고 읽기 가능한 보조 복제본을 포함할 수 있습니다. 이 고가용성 아키텍처를 만들려면 [Windows에서 가용성 그룹의 생성 및 구성](creation-and-configuration-of-availability-groups-sql-server.md)을 참조하세요. 
* 아키텍처는 읽기 배율 작업만을 지원합니다. 

이 문서에서는 읽기 배율 작업에 대한 클러스터 관리자 없이 가용성 그룹을 만드는 방법을 설명합니다. 이 아키텍처는 읽기 배율만을 제공합니다. 고가용성을 제공하지 않습니다.

>[!NOTE]
>`CLUSTER_TYPE = NONE`인 가용성 그룹은 다양한 운영 체제 플랫폼에서 호스팅되는 복제본을 포함할 수 있습니다. 고가용성을 지원할 수 없습니다. Linux 운영 체제는 [Linux에서 읽기 배율에 대한 SQL Server 가용성 그룹 구성](../../../linux/sql-server-linux-availability-group-configure-rs.md)을 참조하세요.

[!INCLUDE [Create prerequisites](../../../includes/ss-availability-group-rs-prereq.md)]

## <a name="create-an-availability-group"></a>가용성 그룹 만들기

가용성 그룹을 만듭니다. `CLUSTER_TYPE = NONE`을 설정합니다. 또한 각 복제본을 `FAILOVER_MODE = NONE`으로 설정합니다. 분석 또는 보고 워크로드를 실행하는 클라이언트 애플리케이션에서 보조 데이터베이스에 직접 연결할 수 있습니다. 읽기 전용 라우팅 목록을 만들 수도 있습니다. 주 복제본에 대한 연결은 읽기 연결 요청을 라운드 로빈 방식으로 라우팅 목록에서 각 보조 복제본으로 전달합니다.

다음 Transact-SQL 스크립트는 `ag1`이라는 가용성 그룹을 만듭니다. 스크립트는 `SEEDING_MODE = AUTOMATIC`으로 가용성 그룹 복제본을 구성합니다. 이렇게 설정하면 SQL Server에서 가용성 그룹에 추가된 후 각 보조 서버에 데이터베이스를 자동으로 만듭니다. 

사용자 환경에 대해 다음 스크립트를 업데이트합니다. `<node1>` 및 `<node2>` 값을 복제본을 호스팅하는 SQL Server 인스턴스의 이름으로 바꿉니다. `<5022>` 값을 엔드포인트에 대해 설정한 포트로 바꿉니다. 주 SQL Server 복제본에서 다음 Transact-SQL 스크립트를 실행합니다.

```sql
CREATE AVAILABILITY GROUP [ag1]
    WITH (CLUSTER_TYPE = NONE)
    FOR REPLICA ON
        N'<node1>' WITH (
            ENDPOINT_URL = N'tcp://<node1>:<5022>',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
                    SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
        N'<node2>' WITH (
            ENDPOINT_URL = N'tcp://<node2>:<5022>',
            AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            FAILOVER_MODE = MANUAL,
            SEEDING_MODE = AUTOMATIC,
            SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            );

ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

### <a name="join-secondary-sql-server-instances-to-the-availability-group"></a>가용성 그룹에 보조 SQL Server 인스턴스 조인

다음 Transact-SQL 스크립트는 `ag1`이라는 가용성 그룹에 서버를 조인합니다. 사용자 환경에 대해 스크립트를 업데이트합니다. 가용성 그룹을 조인하려면 각 보조 SQL Server 복제본에서 다음 Transact-SQL 스크립트를 실행합니다.

```sql
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE);

ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create post](../../../includes/ss-availability-group-rs-postactivity.md)]

이 가용성 그룹은 고가용성 구성이 아닙니다. 고가용성이 필요한 경우 [Linux에서 SQL Server에 대한 Always On 가용성 그룹 구성](../../../linux/sql-server-linux-availability-group-configure-ha.md) 또는 [Windows에서 가용성 그룹의 생성 및 구성](creation-and-configuration-of-availability-groups-sql-server.md)의 지침을 따릅니다.

## <a name="connect-to-read-only-secondary-replicas"></a>읽기 전용 보조 복제본에 연결

두 방법 중 하나를 사용하여 읽기 전용 보조 복제본에 연결할 수 있습니다.
* 애플리케이션은 보조 복제본을 호스팅하는 SQL Server 인스턴스에 직접 연결하고 데이터베이스를 쿼리할 수 있습니다. 자세한 내용은 [읽기 가능한 보조 복제본](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)을 참조합니다.
* 애플리케이션은 수신기가 필요한 읽기 전용 라우팅을 사용할 수도 있습니다. 클러스터 관리자 없이 읽기 확장 시나리오를 배포하는 경우에도 현재 주 복제본의 IP 주소와 SQL Server에서 수신 대기하는 것과 다른 포트를 가리키는 수신기를 만들 수 있습니다. 장애 조치(failover) 후 새로운 주 IP 주소를 가리키도록 수신기를 다시 만들어야 합니다. 자세한 내용은 [읽기 전용 라우팅](listeners-client-connectivity-application-failover.md#ConnectToSecondary)을 참조합니다.

## <a name="fail-over-the-primary-replica-on-a-read-scale-availability-group"></a>읽기 확장 가용성 그룹에서 주 복제본 장애 조치

[!INCLUDE[Force failover](../../../includes/ss-force-failover-read-scale-out.md)]

## <a name="next-steps"></a>다음 단계

* [분산 가용성 그룹 구성](./distributed-availability-groups.md)
* [가용성 그룹에 대한 자세한 정보](overview-of-always-on-availability-groups-sql-server.md)
* [강제 수동 장애 조치(failover) 수행](perform-a-forced-manual-failover-of-an-availability-group-sql-server.md)