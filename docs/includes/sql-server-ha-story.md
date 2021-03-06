이 문서에서는 SQL Server의 고가용성 및 재해 복구를 위한 비즈니스 연속성 솔루션에 대한 개요를 제공합니다. 

SQL Server를 배포하는 모든 사람들이 공통적으로 해야 할 작업 중 하나는 모든 중요한 SQL Server 인스턴스와 그 안에 포함된 데이터베이스를 비즈니스 및 최종 사용자가 필요로 할 때(예: 9~5시 사이 또는 24시간 내내) 사용할 수 있도록 하는 것입니다. 목표는 중단을 최소화하거나 중단 없이 비즈니스를 계속 운영하는 것입니다. 이러한 개념은 비즈니스 연속성이라고도 합니다.

SQL Server 2017은 기존 기능에 새롭거나 향상된 기능을 많이 도입했으며 그 중 일부는 가용성을 위한 것입니다. SQL Server 2017에서 가장 크게 추가된 기능은 Linux 배포판에서 SQL Server를 지원하는 것입니다. SQL Server 2017 새로운 기능의 전체 목록은 [SQL Server의 새로운 기능](../sql-server/what-s-new-in-sql-server-2017.md)을 참조하십시오.

이 문서는 SQL Server 2017의 가용성 시나리오와 SQL Server 2017의 새롭고 향상된 가용성 기능을 설명하는 데 중점을 두고 있습니다. 이 시나리오에는 Windows Server 및 Linux에서 SQL Server 배포를 확장할 수 있을 뿐만 아니라 데이터베이스의 읽기 가능한 복사본 수를 늘릴 수 있는 하이브리드 시나리오도 포함됩니다. 이 문서에서는 가상화에서 제공되는 것과 같은 SQL Server 외부의 가용성 옵션에 대해서는 설명하지 않지만, 여기에 언급된 모든 내용은 퍼블릭 클라우드의 게스트 가상 머신이나 온-프레미스 하이퍼바이저 서버가 호스트하는 게스트 가상 머신 내부의 SQL Server 설치에 적용됩니다.

## <a name="sql-server-2017-scenarios-using-the-availability-features"></a>가용성 기능을 사용하는 SQL Server 2017 시나리오

가용성 그룹, FCI 및 로그 전달은 다양한 방법으로 사용할 수 있으며 가용성 목적으로만 사용할 수 있는 것은 아닙니다. 가용성 기능을 사용할 수 있는 주요 방법은 네 가지입니다.

* 고가용성
* 재해 복구
* 마이그레이션 및 업그레이드
* 하나 이상의 데이터베이스에서 읽을 수 있는 복사본 확장

각 섹션에서는 특정 시나리오에 사용할 수 있는 관련 기능에 대해 설명합니다. 다루지 않는 한 가지 기능은 [SQL Server 복제](../relational-databases/replication/sql-server-replication.md)입니다. Always On 내에 가용성 기능으로 공식 지정되지는 않았지만 특정 시나리오에서 데이터 중복을 위해 종종 사용됩니다. 복제는 향후 릴리스에서 Linux의 SQL Server에 추가될 예정입니다.

> [!IMPORTANT] 
> SQL Server 가용성 기능을 사용하더라도 가용성 솔루션의 가장 근본적인 구성 요소인 충분한 테스트를 거친 강력한 백업 및 복원 전략이 꼭 필요합니다.

### <a name="high-availability"></a>고가용성

클라우드 지역의 데이터 센터 또는 단일 지역에 국한된 문제가 발생하는 경우 SQL Server 인스턴스 또는 데이터베이스를 사용할 수 있도록 하는 것이 중요합니다. 이 섹션에서는 SQL Server 가용성 기능이 이러한 작업을 지원하는 방법에 대해 설명합니다. 설명된 모든 기능은 Windows Server뿐 아니라 Linux에서도 사용할 수 있습니다. 

#### <a name="always-on-availability-groups"></a>Always On 가용성 그룹

SQL Server 2012에 도입된 Always On 가용성 그룹(가용성 그룹)은 데이터베이스의 각 트랜잭션을 특수 상태의 해당 데이터베이스 복사본이 포함된 복제본이라고 하는 다른 인스턴스로 보내서 데이터베이스 수준의 보호를 제공합니다. 가용성 그룹은 Standard 또는 Enterprise Edition에 배포할 수 있습니다.  가용성 그룹에 참여하는 인스턴스는 독립 실행형이거나 Always On FCI(Failover Cluster Instance, 다음 섹션 참조)일 수 있습니다. 트랜잭션이 발생하면 복제본으로 전송되기 때문에 복구 지점 및 복구 시간 목표를 낮추기 위한 요구 사항이 있는 경우 가용성 그룹을 사용하는 것이 좋습니다. 복제본 간의 데이터 이동은 동기식 또는 비동기식일 수 있으며 Enterprise Edition에서는 동기식으로 최대 3개의 복제본(기본 포함)이 허용됩니다. 가용성 그룹에는 주 복제본에 있는 데이터베이스의 완전 읽기/쓰기 복사본이 하나 있고 모든 보조 복제본은 최종 사용자 또는 애플리케이션에서 직접 트랜잭션을 수신할 수 없습니다. 

> [!NOTE] 
> Always On은 SQL Server의 가용성 기능에 대한 포괄적인 용어이며 가용성 그룹과 FCI가 포함됩니다. Always On은 가용성 그룹 기능의 이름이 아닙니다.

가용성 그룹은 인스턴스 수준이 아닌 데이터베이스 수준의 보호만 제공하기 때문에 트랜잭션 로그에 캡처되지 않거나 데이터베이스에 구성되지 않은 항목은 각 보조 복제본에 수동으로 동기화되어야 합니다. 수동으로 동기화해야 하는 개체의 예로는 인스턴스 수준의 로그인, 연결된 서버 및 SQL Server 에이전트 작업이 있습니다.

가용성 그룹에는 수신기라는 또 다른 구성 요소가 있어서 애플리케이션과 최종 사용자가 주 복제본을 호스트하는 SQL Server 인스턴스를 몰라도 연결기 가능하도록 합니다. 각 가용성 그룹에는 자체 수신기가 있습니다. 수신기 구현은 Windows Server와 Linux에서 약간 다르지만 제공하는 기능과 사용하는 방법은 동일합니다. 아래 그림은 WSFC(Windows Server 장애 조치 클러스터)를 사용하는 Windows Server 기반 가용성 그룹을 보여줍니다. OS 계층에 있는 기본 클러스터는 Linux 또는 Windows Server에 상관없이 가용성을 위해 필요합니다. 이 예제는 WSFC가 기본 클러스터인 단순한 두 개의 서버 또는 노드 구성을 보여줍니다. 

![단순한 가용성 그룹](media/sql-server-ha-story/image1.png)
 
Standard 및 Enterprise Edition은 복제본에 대한 최대값이 다릅니다. 기본 가용성 그룹이라고 하는 Standard Edition의 가용성 그룹은 가용성 그룹의 데이터베이스가 하나뿐인 두 개의 복제본(주 복제본과 보조 복제본)을 지원합니다. Enterprise Edition은 하나의 가용성 그룹에 여러 데이터베이스를 구성할 수 있을 뿐 아니라 최대 9개의 복제본(주 1개, 보조 8개)을 가질 수 있습니다. Enterprise Edition은 읽기 가능한 보조 복제본, 보조 복제본에서 백업을 수행하는 기능 등의 다른 선택적 이점도 제공합니다.

>[!NOTE]
> SQL Server 2012에서 더 이상 사용되지 않는 데이터베이스 미러링은 Linux 버전의 SQL Server에서 사용할 수 없으며 추가되지 않습니다. 데이터베이스 미러링을 아직 사용하는 고객은 데이터베이스 미러링을 대체하는 가용성 그룹으로 마이그레이션을 계획해야 합니다.

가용성과 관련하여 가용성 그룹은 자동 또는 수동 장애 조치(failover)를 제공할 수 있습니다. 자동 장애 조치(failover)는 동기 데이터 이동이 구성되어 있고 주 복제본과 보조 복제본의 데이터베이스가 동기화된 상태이면 발생할 수 있습니다. 수신기가 사용되고 애플리케이션에 최신 버전의 .NET(업데이트가 있는 3.5 또는 4.0 이상)이 사용되는 한, 수신기가 사용되는 경우 최종 사용자에게 거의 영향을 미치지 않으면서 장애 조치(failover)가 처리되어야 합니다. 보조 복제본을 새 주 복제본으로 만드는 장애 조치(failover)는 자동 또는 수동으로 구성될 수 있으며 일반적으로 초 단위로 측정됩니다.

아래 목록은 Windows Server와 Linux의 가용성 그룹에 대한 몇 가지 차이점을 보여줍니다.
* Linux와 Windows Server에서 기본 클러스터가 작동하는 방식의 차이로 인해 가용성 그룹의 모든 장애 조치(failover)(수동 또는 자동)는 Linux의 클러스터를 통해 수행됩니다. Windows Server 기반 가용성 그룹 배포에서는 SQL Server를 통해 수동 장애 조치(failover)를 수행해야 합니다. 자동 장애 조치(failover)는 Windows Server와 Linux의 기본 클러스터에서 처리됩니다. 
* SQL Server 2017에서 Linux의 가용성 그룹에 권장되는 구성은 최소 세 개의 복제본입니다. 이것은 기본 클러스터링이 작동하는 방식 때문입니다. 두 개 복제본 구성을 위한 향상된 솔루션이 나중에 릴리즈될 예정입니다.
* Linux에서 각 수신기에서 사용되는 일반 이름은 DNS에 정의되며 Windows Server에서처럼 클러스터에 정의되지 않습니다.

SQL Server 2017에는 가용성 그룹에 대한 몇 가지 새롭고 향상된 기능이 있습니다.

* 클러스터 유형
* REQUIRED_SECONDARIES_TO_COMMIT
* Windows Server 기반 구성에 대해 향상된 Microsoft DTC(Distributor Transaction Coordinator) 지원
* 읽기 전용 데이터베이스에 대한 추가 확장 시나리오 (이 문서 뒷부분 참조)

##### <a name="always-on-availability-group-cluster-types"></a>Always On 가용성 그룹 클러스터 유형

Windows Server에 기본 제공되는 클러스터링의 가용성 형태는 장애 조치(failover) 클러스터링이라는 기능을 통해 활성화됩니다. 이를 통해 가용성 그룹 또는 FCI와 함께 사용되는 WSFC를 만들 수 있습니다. 가용성 그룹 및 FCI에 대한 통합은 SQL Server에 제공되는 클러스터 인식 리소스 DLL에 의해 제공됩니다. 

지원되는 각각의 Linux 배포판에는 자체적인 Pacemaker 클러스터 솔루션 버전이 제공됩니다. Linux의 SQL Server 2017은 Pacemaker 사용을 지원합니다. Pacemaker는 각 배포판을 자체 스택에 통합할 수 있는 개방형 스택 솔루션입니다. 배포판에 Pacemaker가 제공되지만 Windows Server의 장애 조치(failover) 클러스터링 기능만큼 통합되어 있지 않습니다.

WSFC와 Pacemaker는 다르기보다는 유사합니다. 둘 다 개별 서버를 구성으로 결합하여 가용성을 제공하는 방법을 제공하고 리소스, 제약 조건(다르게 구현되는 경우에도), 장애 조치(failover) 등의 개념을 제공합니다. 가용성 그룹과 자동 장애 조치(failover)와 같은 FCI 구성 양쪽 모두에 대해 Pacemaker를 지원하기 위해 Microsoft는 mssql-server-ha 패키지를 제공합니다. 이것은 Pacemaker용 WSFC의 리소스 DLL과 유사하지만 완전히 동일하지는 않습니다. WSFC와 Pacemaker의 차이 중 하나는 Pacemaker에 네트워크 이름 리소스가 없다는 것입니다. Pacemaker는 WSFC에서 수신기 이름(또는 FCI 이름)을 추상화하는 데 도움이 되는 구성 요소입니다. DNS는 Linux에서 해당 이름 확인을 제공합니다.

클러스터 스택의 차이로 인해, SQL Server는 WSFC에서 기본적으로 처리하는 일부 메타 데이터를 처리해야 하기 때문에 가용성 그룹에 대한 일부 변경이 필요했습니다. 가장 [!IMPORTANT]한 변경 사항은 가용성 그룹에 대한 클러스터 유형의 도입입니다. 이것은 cluster_type 및 cluster_type_desc 열의 sys.availability_groups에 저장됩니다. 클러스터 유형은 세 가지입니다.

* WSFC 
* 외부
* None

가용성이 필요한 모든 가용성 그룹은 기본 클러스터를 사용해야 합니다. SQL Server 2017의 경우 WSFC 또는 Pacemaker가 여기에 해당됩니다. 기본 WSFC를 사용하는 Windows Server 기반 가용성 그룹의 경우 기본 클러스터 유형은 WSFC이며 설정이 필요 없습니다. Linux 기반 가용성 그룹의 경우 가용성 그룹을 만들 때 클러스터 유형을 외부로 설정해야 합니다. Pacemaker와의 통합은 가용성 그룹이 만들어진 후에 구성되는 반면 WSFC의 경우 생성시 완료됩니다.

없음이라는 클러스터 유형은 Windows Server 및 Linux 가용성 그룹 모두에서 사용할 수 있습니다. 클러스터 유형을 없음으로 설정하면 가용성 그룹에 기본 클러스터가 필요하지 않다는 의미입니다. 즉, SQL Server 2017은 클러스터 없이 가용성 그룹을 지원하는 첫 번째 SQL Server 버전이지만 이 구성은 고가용성 솔루션으로 지원되지 않습니다. 

> [!IMPORTANT] 
> SQL Server 2017에서는 가용성 그룹을 만든 후 가용성 그룹의 클러스터 유형을 변경할 수 없습니다. 즉, 가용성 그룹을 없음에서 외부 또는 WSFC로 또는 그 반대로 전환할 수 없습니다. 

데이터베이스의 읽기 전용 복사본만 추가하려는 경우 또는 가용성 그룹이 마이그레이션/업그레이드에 제공하는 기능은 필요하지만 기본 클러스터나 복제의 추가 복잡성에 관여하지 않으려는 경우에는 클러스터 유형이 없음인 가용성 그룹이 완벽한 솔루션이 될 수 있습니다. 자세한 내용은 [마이그레이션 및 업그레이드](#Migrations)와 [읽기 확장](#ReadScaleOut)을 참조하세요. 

아래 스크린샷은 SSMS의 여러 종류의 클러스터 유형에 대한 지원을 보여줍니다. 버전 17.1 이상을 실행해야 합니다. 아래 스크린샷은 버전 17.2입니다.

![SSMS AG 옵션](media/sql-server-ha-story/image2.png)
 
##### <a name="required_synchronized_secondaries_to_commit"></a>REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT

SQL Server 2016은 Enterprise Edition에서 동기 복제본 수에 대한 지원을 2에서 3으로 증가 시켰습니다. 하지만 하나의 보조 복제본이 동기화되었지만 다른 복제본에 문제가 있다면 오작동하는 복제본을 기다리거나 그대로 진행하도록 기본 복제본에 알리는 동작을 제어할 방법이 없습니다. 즉 보조 복제본이 동기화된 상태가 아니라도 다시 말해 보조 복제본에 데이터 손실이 발생하더라도 주 복제본은 어느 시점에 쓰기 트래픽을 계속 받게 됩니다.
SQL Server 2017에는 동기 복제본이 있을 때 발생하는 동작을 제어할 수 있는 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT라는 옵션이 있습니다. 이 옵션은 다음과 같이 작동합니다.
* 가능한 값은 0, 1 및 2입니다.
* 이 값은 동기화해야 하는 보조 복제본의 수이며 데이터 손실, 가용성 그룹 가용성 및 장애 조치(failover)에 영향을 미칩니다.
* WSFC 및 클러스터 유형이 없음인 경우 기본값은 0이며 수동으로 1 또는 2로 설정할 수 있습니다.
* 클러스터 유형이 외부인 경우 기본적으로 클러스터 메커니즘에 의해 이 값이 설정되며 수동으로 재정의할 수 있습니다. 동기 복제본이 3개인 경우, 기본값은 1입니다.
Linux에서 REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT 값은 클러스터의 가용성 그룹 리소스에 구성됩니다. Windows에서는 Transact-SQL을 통해 설정됩니다.

필요한 수의 보조 복제본이 없으면 이것이 해결될 때가지 주 복제본을 사용할 수 없기 때문에 값이 0보다 높으면 데이터 보호 수준이 높아집니다. REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT는 장애 조치(failover) 동작에도 영향을 주는데 이것은 필요한 수의 보조 복제본이 적절한 상태가 아니면 자동 장애 조치가 발생할 수 없기 때문입니다. Linux에서 값이 0이면 자동 장애 조치(failover)를 허용하지 않으므로 Linux에서 자동 장애 조치(failover)와 함께 동기를 사용할 경우 자동 장애 조치를 수행하려면 값을 0보다 높게 설정해야 합니다. Windows Server에서 값이 0이면 SQL Server 2016 및 이전 동작입니다.

##### <a name="enhanced-microsoft-distributed-transaction-coordinator-support"></a>향상된 Microsoft DTC(Distributed Transaction Coordinator) 지원

SQL Server 2016 이전에는 DTC를 사용하는 분산 트랜잭션이 필요한 애플리케이션에 대해 SQL Server에서 가용성을 얻는 유일한 방법은 FCI를 배포하는 것이었습니다. 분산 트랜잭션은 다음 두 가지 방법 중 하나로 수행할 수 있습니다.
* 동일한 SQL Server 인스턴스에서 둘 이상의 데이터베이스에 걸쳐있는 트랜잭션
* 둘 이상의 SQL Server 인스턴스에 걸쳐 있거나 SQL Server 이외의 데이터 원본과 관련된 트랜잭션

SQL Server 2016에서는 후자의 시나리오를 처리하는 가용성 그룹을 사용하여 DTC를 부분적으로 지원합니다. SQL Server 2017은 DTC를 사용하여 두 시나리오를 모두 지원함으로써 기능 완수합니다.

가용성 그룹에 대한 DTC 지원의 또 다른 개선 사항은 SQL Server 2016에서 가용성 그룹에 대한 DTC 지원은 가용성 그룹이 만들어 질 때만 설정할 수 있으며 나중에 추가할 수 없습니다. SQL Server 2017에서는 가용성 그룹을 만든 후에도 DTC 지원이 추가될 수 있습니다.

>[!NOTE]
> DTC 지원은 Windows Server 기반 SQL Server 인스턴스의 데이터베이스에 대해서만 구성할 수 있습니다. DTC가 애플리케이션의 요구 사항인 경우 SQL Server 배포를 위해 Windows Server를 OS로 사용해야 하며 Linux는 사용할 수 없습니다. 

#### <a name="always-on-failover-cluster-instances"></a>Always On 장애 조치(failover) 클러스터 인스턴스
클러스터형 설치는 버전 6.5부터 SQL Server의 기능입니다. FCI는 SQL Server의 전체 설치에 대해 가용성을 제공하는 입증된 방법이며 인스턴스로 알려져 있습니다. 즉, 기본 서버에 문제가 발생할 경우 데이터베이스, SQL Server 에이전트 작업, 연결된 서버 등 인스턴스 내부의 모든 항목이 다른 서버로 이동됩니다. 모든 FCI는 네트워킹을 통해 제공되는 경우에도 일종의 공유 스토리지가 필요합니다. FCI의 리소스는 주어진 시간에 한 노드에서만 실행하고 소유할 수 있습니다. 아래 그림에서 클러스터의 첫 번째 노드는 FCI를 소유하며 이는 스토리지에 실선으로 표시된 공유 스토리지 리소스를 소유하는 것을 의미합니다.

![장애 조치(Failover) 클러스터 인스턴스](media/sql-server-ha-story/image3.png)
 
장애 조치(failover) 후에는 아래 그림과 같이 소유권이 변경됩니다.

![사후 장애 조치(Failover)](media/sql-server-ha-story/image4.png)
 
FCI에서는 데이터 손실이 거의 없지만 데이터 복사본이 하나이기 때문에 기본 공유 스토리지는 단일 실패 지점입니다. FCI는 중복 데이터베이스 복사본을 확보하기 위해 종종 가용성 그룹이나 로그 전달과 같은 다른 가용성 방법과 결합됩니다. 추가로 배포된 방법은 FCI와 물리적으로 분리된 스토리지를 사용해야 합니다. FCI가 다른 노드로 장애 조치(failover)되면 노드를 중지하고 다른 노드에서 시작하기 때문에 서버의 전원을 껐다 켜는 것과는 다릅니다. FCI는 정상 복구 프로세스를 거칩니다. 즉 롤포워드가 필요한 트랜잭션은 롤포워드가 수행되며 불완전한 트랜잭션은 롤백됩니다. 따라서 데이터베이스는 장애 또는 수동 장애 조치(failover) 시간의 데이터 지점과 일관성을 유지하기 때문에 데이터 손실이 없습니다. 데이터베이스는 복구가 완료된 후에만 사용할 수 있으며 복구 시간은 다양한 요인에 따라 달라지며 일반적으로 가용성 그룹의 장애 조치(failover) 시간보다 길어집니다. 가용성 그룹을 장애 조치(failover)하면 데이터베이스를 사용할 수 있도록 만드는 데 필요한 추가 작업(예: SQL Server 에이전트 작업을 활성화하는 것)이 있을 수 있습니다.

가용성 그룹과 마찬가지로 FCI는 기본 클러스터의 어느 노드에서 호스트 하는지를 추상화합니다. FCI는 항상 같은 이름을 유지합니다. 애플리케이션과 최종 사용자는 노드에 절대 연결하지 않으며 FCI에 할당된 고유한 이름이 사용됩니다. FCI는 주 또는 보조 복제본을 호스트하는 인스턴스 중 하나로 가용성 그룹에 참여할 수 있습니다.

아래 목록은 Windows Server와 Linux에서 FCI의 몇 가지 차이점을 보여줍니다.

* Windows Server에서 FCI는 설치 프로세스의 일부입니다. Linux의 FCI는 SQL Server를 설치한 후에 구성됩니다.
* Linux에서는 호스트당 SQL Server를 하나만 설치할 수 있으므로 모든 FCI가 기본 인스턴스가 됩니다. Windows Server는 WSFC당 최대 25개의 FCI를 지원합니다.
* Linux에서 FCI가 사용하는 일반 이름은 DNS에 정의되어 있으며 FCI용으로 생성된 리소스와 동일해야 합니다.

#### <a name="log-shipping"></a>로그 전달
복구 시점 및 복구 시간 목표가보다 유연하거나 데이터베이스가 업무상 중요하지 않은 경우에는 로그 전달이 SQL Server의 입증된 또 다른 가용성 기능이 될 수 있습니다. SQL Server의 기본 백업을 기반으로 로그 전달 프로세스는 트랜잭션 로그 백업을 자동으로 생성하고, 이것을 웜 대기라는 하나 이상의 인스턴스에 복사하고, 트랜잭션 로그 백업을 해당 대기 항목에 자동으로 적용합니다. 로그 전달은 SQL Server 에이전트 작업을 사용하여 트랜잭션 로그 백업을 백업, 복사 및 적용하는 프로세스를 자동화합니다.

![로그 전달](media/sql-server-ha-story/image5.png)
 
일부 용량에서 로그 전달을 사용하는 가장 큰 이점은 사람의 실수를 처리하는 것입니다. 트랜잭션 로그 적용은 지연될 수 있습니다. 따라서 누군가 WHERE 절 없이 UPDATE 등의 명령을 보내면 대기에 변경 사항이 전달되지 않아서 주 시스템을 복구하는 동안 대기로 전환될 수 있습니다. 로그 전달은 구성하기 쉽지만 기본 대기에서 웜 대기로 전환하는 것(역할 변경이라고 함)은 항상 수동입니다. 역할 변경은 Transact-SQL을 통해 시작되며 가용성 그룹과 마찬가지로 트랜잭션 로그에 캡처되지 않은 모든 개체는 수동으로 동기화해야 합니다. 단일 가용성 그룹에는 여러 데이터베이스가 포함될 수 있지만 로그 전달은 데이터베이스별로 구성해야 합니다. 가용성 그룹 또는 FCI와 달리 로그 전달에는 역할 변경에 대한 추상화가 없습니다. 애플리케이션에서 이 문제를 처리할 수 있어야 합니다. DNS 별칭(CNAME)과 같은 기술을 사용할 수 있지만 전환 후 DNS를 새로 고치는 데 걸리는 시간과 같은 장단점이 있습니다.

## <a name="disaster-recovery"></a>재해 복구

주 가용성 위치에 지진이나 홍수와 같은 치명적인 재해가 발생하는 경우, 자사 시스템이 다른 곳에서 온라인 상태가 되도록 준비해 두어야 합니다. 이 섹션에서는 SQL Server 가용성 기능이 비즈니스 연속성을 어떻게 지원할 수 있는지에 대해 설명합니다.

### <a name="always-on-availability-groups"></a>Always On 가용성 그룹

가용성 그룹의 장점 중 하나는 단일 기능을 사용하여 고가용성 및 재해 복구를 구성할 수 있다는 점입니다. 공유 스토리지의 고가용성을 보장하지 않고도 각각 별개의 스토리지를 사용하여 고가용성을 위해 하나의 데이터 센터에 로컬인 복제본을 확보하고 재해 복구를 위해 다른 데이터 센터에 원격 복제본을 확보하는 것이 훨씬 쉽습니다. 데이터베이스의 추가 복사본을 확보하는 것은 중복성을 보장하기 위한 절충안입니다. 여러 데이터 센터에 걸쳐있는 가용성 그룹의 예는 아래와 같습니다. 하나의 주 복제본은 모든 보조 복제본을 동기화된 상태로 유지할 책임이 있습니다.

![가용성 그룹](media/sql-server-ha-story/image6.png)
 
클러스터 유형이 없음인 가용성 그룹 외부에서 가용성 그룹은 모든 복제본이 동일한 기본 클러스터(WSFC 또는 Pacemaker)의 일부가 될 것을 요구합니다. 즉, 위의 그림에서 WSFC는 두 개의 서로 다른 데이터 센터에서 작동하도록 확장되어 복잡성이 추가됩니다. 플랫폼(Windows Server 또는 Linux)과 관계없이 적용됩니다. 멀리 떨어져있는 클러스터를 스트레치하면 복잡성이 추가됩니다. SQL Server 2016에 도입된 분산형 가용성 그룹을 사용하면 가용성 그룹을 여러 클러스터에 구성된 가용성 그룹으로 확장할 수 있습니다. 이렇게 하면 모든 노드가 동일한 클러스터에 참여해야 하는 요구 사항이 완화되므로 재난 복구가 훨씬 쉬워집니다. 분산형 가용성 그룹에 대한 자세한 내용은 [분산형 가용성 그룹](../database-engine/availability-groups/windows/distributed-availability-groups.md)을 참조하세요.

![분산형 가용성 그룹 다이어그램](media/sql-server-ha-story/image11.png)
 
### <a name="always-on-failover-cluster-instances"></a>Always On 장애 조치(failover) 클러스터 인스턴스

FCI는 재해 복구에 사용될 수 있습니다. 일반 가용성 그룹과 마찬가지로 기본 클러스터 메커니즘도 모든 위치로 확장해야 하기 때문에 복잡성이 추가됩니다. FCI에는 공유 스토리지라는 추가 고려 사항이 있습니다. 기본 및 보조 사이트에서 동일한 디스크를 사용할 수 있어야 하기 때문에 FCI에서 사용하는 디스크가 다른 곳에 있도록 하려면 하드웨어 계층에서 스토리지 공급 업체가 제공하는 기능 또는 Windows Server의 스토리지 복제본 사용과 같은 외적인 방법이 필요합니다. 

![Always On FCI](media/sql-server-ha-story/image8.png)
 
### <a name="log-shipping"></a>로그 전달
로그 전달은 SQL Server 데이터베이스에 재해 복구를 제공하는 가장 오래된 방법 중 하나입니다. 로그 전달은 가용성 그룹 및 FCI와 함께 사용되어 비용 효율적이고 간단한 재해 복구를 제공합니다. 다른 옵션은 환경, 관리 기술 또는 예산으로 인해 어려울 수 있습니다. 로그 전달에 대한 고가용성 시나리오와 마찬가지로, 많은 환경에서 사람의 실수를 처리하기 위해 트랜잭션 로그의 로드를 지연시킵니다.

## <a name="migrations-and-upgrades"></a><a name = "Migrations"></a> 마이그레이션 및 업그레이드

새 인스턴스를 배포하거나 기존 인스턴스를 업그레이드할 때 업무를 오래 중단하는 것이 여의치 않습니다. 이 섹션에서는 SQL Server의 가용성 기능을 사용하여 계획된 아키텍처 변경, 서버 전환, 플랫폼 변경(예: Windows Server에서 Linux로 또는 그 반대로) 또는 패치 적용으로 인한 가동 중지 시간을 최소화하는 방법에 대해 설명합니다.

> [!NOTE]
> 백업을 사용하고 다른 곳으로 복원하는 등의 다른 방법을 마이그레이션 및 업그레이드에 사용할 수도 있습니다. 이 내용은 문서에 포함되지 않습니다. 

### <a name="always-on-availability-groups"></a>Always On 가용성 그룹

하나 이상의 가용성 그룹을 포함하는 기존 인스턴스를 SQL Server 2017로 업그레이드할 수 있습니다. 적절한 계획을 세우면 가동 중지 시간이 다소 필요하지만 최소화할 수 있습니다. 

새로운 서버로 마이그레이션하면서 구성(운영 체제 또는 SQL Server 버전 포함)은 변경하지 않는 것이 목표인 경우 해당 서버를 기존의 기본 클러스터에 노드로 추가하고 가용성 그룹에 추가할 수 있습니다. 복제본이 올바른 상태가 되면 새 서버에 수동 장애 조치를 수행할 수 있으며 이전 서버는 가용성 그룹에서 제거하고 최후에는 서비스를 해제할 수 있습니다. 

분산형 AG는 새로운 구성으로 마이그레이션하거나 SQL Server를 업그레이드하는 또 다른 방법입니다. 예를 들어 분산형 AG는 서로 다른 아키텍처에서 서로 다른 기본 AG를 지원하기 때문에 Windows Server 2012 R2에서 실행되는 SQL Server 2016을 Windows Server 2016에서 실행되는 SQL Server 2017로 변경할 수 있습니다. 

![분산형 AG](media/sql-server-ha-story/image10.png)

마지막으로 클러스터 유형이 없음인 가용성 그룹을 마이그레이션이나 업그레이드에 사용할 수도 있습니다. 일반적인 가용성 그룹 구성에서 클러스터 유형을 짜맞출 수 없으므로 모든 복제본의 유형이 없음이어야 합니다. 분산형 가용성 그룹을 사용하여 서로 다른 클러스터 유형으로 구성된 가용성 그룹을 확장할 수 있습니다. 이 방법은 서로 다른 OS 플랫폼에서도 지원됩니다.

마이그레이션 및 업그레이드를 위한 가용성 그룹의 모든 변형은 작업 중 가장 시간을 많이 소비하는 부분(데이터 동기화)을 시간에 따라 수행하도록 허용합니다. 새로운 구성으로 전환을 시작하는 경우 컷오버는 일시적인 중단 대 데이터 동기화를 비롯한 모든 작업을 완료해야 하는 오랜 가동 중지 시간입니다. 

가용성 그룹은 패치 적용이 완료되는 동안 주 복제본을 보조 복제본으로 수동 장애 조치(failover)하여 기본 OS의 패치 적용으로 인한 가동 중지 시간을 최소화할 수 있습니다. 운영 체제 측면에서 볼 때 이렇게 하는 것이 Windows Server에서 더 일반적일 수 있습니다. 그 이유는 자주는 아니지만 종종 기본 OS를 서비스하는 경우 재부팅이 필요하기 때문입니다. Linux에 패치를 적용할 때 가끔 재부팅이 필요하지만 드물게 발생할 수 있습니다. 

[가용성 그룹에 참여하는 SQL Server 인스턴스에 패치를 적용하면](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md) 가용성 그룹 아키텍처의 복잡성에 따라 가동 중지 시간을 최소화할 수 있습니다. 가용성 그룹에 참여하는 서버에 패치를 적용하려면 보조 복제본에 패치가 먼저 적용됩니다. 적절한 수의 복제본에 패치가 적용되면 주 복제본을 다른 노드로 수동으로 장애 조치(failover)하여 업그레이드를 수행합니다. 그 시점에 남아있는 보조 복제본도 업그레이드할 수 있습니다. 

### <a name="always-on-failover-cluster-instances"></a>Always On 장애 조치(failover) 클러스터 인스턴스

FCI는 자체적으로 기존 마이그레이션 또는 업그레이드를 지원할 수 없습니다. 가용성 그룹 또는 로그 전달은 FCI의 데이터베이스와 다른 모든 개체가 처리될 수 있도록 구성되어야 합니다. 그러나 Windows Server 기반 FCI는 기본 Windows Server에 패치를 적용해야 하는 경우 여전히 많이 사용되는 옵션입니다. 수동 장애 조치를 시작할 수 있습니다. 즉, Windows Server에 패치가 적용되는 동안 인스턴스를 완전히 사용할 수 없게 되는 대신 일시적인 중단을 할 수 있습니다.
FCI를 SQL Server 2017로 업그레이드할 수 있습니다. 자세한 내용은 [SQL Server 장애 조치(failover) 클러스터 인스턴스 업그레이드](../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance.md)를 참조하세요.

### <a name="log-shipping"></a>로그 전달

로그 전달은 마이그레이션 및 업그레이드 데이터베이스 모두에서 여전히 많이 사용되는 옵션입니다. 가용성 그룹과 비슷하지만 이번에는 트랜잭션 로그를 동기화 방법으로 사용하기 때문에 서버를 전환하기 훨씬 전에 데이터 전달을 시작할 수 있습니다. 전환 시 원본에서 모든 트래픽이 중지되면 최종 트랜잭션 로그를 가져와서 복사하고 새 구성에 적용합니다. 이 시점에서 데이터베이스를 온라인 상태로 만들 수 있습니다. 로그 전달은 종종 느린 네트워크를 허용하며, 가용성 그룹 또는 분산형 가용성 그룹을 사용하여 수행하는 것보다 전환 시간이 약간 더 걸릴 수 있지만 보통 시간, 일 또는 주가 아닌 분 단위로 측정됩니다.

가용성 그룹과 마찬가지로 로그 전달은 패치 적용 시 다른 서버로 전환할 수 있는 방법을 제공합니다.

### <a name="other-sql-server-deployment-methods-and-availability"></a>기타 SQL Server 배포 방법 및 가용성

Linux에서 SQL Server에 대한 다른 두 가지 배포 방법은 컨테이너 및 Azure(또는 다른 퍼블릭 클라우드 공급자)를 사용하는 것입니다. 이 문서에 제시된 가용성에 대한 일반적인 필요성은 SQL Server 배포 방법에 관계없이 존재합니다. 이 두 가지 방법은 SQL Server의 가용성을 높이는 데 있어 특별한 고려 사항이 있습니다.

[Docker를 사용하는 컨테이너](../linux/quickstart-install-connect-docker.md)는 Windows Server 또는 Linux용 SQL Server를 배포하는 새로운 방법입니다. 컨테이너는 실행 준비가 되어 있는 SQL Server의 전체 이미지입니다. 그러나 클러스터링에 대한 기본 지원이 없으므로 직접적인 고가용성 또는 재해 복구는 없습니다. 현재 컨테이너를 사용하여 SQL Server 데이터베이스를 사용할 수 있도록 만드는 옵션은 로그 전달 및 백업 및 복원입니다. 클러스터 유형이 없음인 가용성 그룹을 구성할 수 있지만 앞에서 설명한 것처럼 실제 가용성 구성으로 간주되지는 않습니다. Microsoft는 컨테이너를 사용하여 가용성 그룹 또는 FCI를 사용하도록 설정하는 방법을 모색하고 있습니다. 

현재 컨테이너를 사용하는 경우 컨테이너가 손실되면 컨테이너 플랫폼에 따라 다시 배포하고 사용했던 공유 스토리지에 연결할 수 있습니다. 이 메커니즘 중 일부는 컨테이너 조정자가 제공합니다. 이 기능은 약간의 복원력을 제공하지만 데이터베이스 복구와 관련된 가동 중지 시간이 있을 수 있으며 가용성 그룹 또는 FCI를 사용하는 경우처럼 실제로 가용성이 높지는 않습니다. 

Azure를 사용하여 SQL Server를 설치하면 Linux IaaS 가상 컴퓨터를 배포할 수 있습니다. 온-프레미스 기반 설치에서와 마찬가지로 지원되는 설치에서는 Pacemaker 외부에 있는 STONITH(헤드에 있는 다른 노드 맞추기)를 사용해야 합니다. STONITH는 펜싱 가용성 에이전트를 통해 제공됩니다. 일부 배포는 플랫폼의 일부로 제공되고 나머지 배포는 외부 하드웨어 및 소프트웨어 공급 업체에 의존합니다. 원하는 Linux 배포판을 확인하여 지원되는 솔루션을 퍼블릭 클라우드에 배포할 수 있도록 어떤 형태의 STONITH가 제공되는지 확인하십시오.

## <a name="cross-platform-and-linux-distribution-interoperability"></a>플랫폼 간 및 Linux 배포 상호 운용성

이 섹션에서는 Windows Server와 Linux 모두에서 지원되는 SQL Server를 사용하여 다른 용도 외에 가용성을 위해 함께 작동할 수 있는 방법은 물론 둘 이상의 Linux 배포를 통합하는 솔루션에 대한 시나리오를 설명합니다.

플랫폼 간 시나리오 및 상호 운용성 시나리오를 언급하기 전에 두 가지 사실을 명시해야 합니다.

* WSFC 기반 FCI 또는 가용성 그룹이 Linux 기반 FCI 또는 가용성 그룹과 직접 작동하는 시나리오는 없습니다. WSFC는 Pacemaker 노드에 의해 확장될 수 없으며 그 반대의 경우도 마찬가지 입니다. 
* FCI 또는 클러스터 유형이 외부인 가용성 그룹에서는 Linux 배포판 혼합을 지원하지 않습니다. 해당 시나리오의 모든 가용성 그룹 복제본은 동일한 Linux 배포판뿐만 아니라 동일한 버전으로 구성되어야 합니다. SQL Server를 두 개의 플랫폼 또는 Linux의 여러 배포판에서 작동할 수 있도록 지원되는 두 가지 방법은 가용성 그룹과 로그 전달입니다.

## <a name="distributed-availability-groups"></a>분산 가용성 그룹 

분산형 가용성 그룹은 가용성 그룹 하에 있는 두 개의 기본 클러스터가 두 개의 서로 다른 WSFC이거나, Linux 배포판이거나, 또는 하나가 WSFC이고 나머지가 Linux이든 상관없이 가용성 그룹 구성을 확장하도록 설계되었습니다. 분산형 가용성 그룹은 플랫폼 간 솔루션을 확보하는 기본 방법입니다. 분산형 가용성 그룹은 Windows Server 기반 SQL Server 인프라를 Linux 기반의 인프라로 변환하는 등 회사에 필요한 마이그레이션을 위한 기본 솔루션이기도 합니다. 위에서 언급했듯이 가용성 그룹, 특히 분산형 가용성 그룹은 애플리케이션을 사용할 수 없게 되는 시간을 최소화합니다. 다음은 WSFC와 Pacemaker에 걸친 분산형 가용성 그룹의 예입니다.

![WSFC와 Pacemaker에 걸친 분산형 가용성 그룹 다이어그램](media/sql-server-ha-story/image9.png)
 
가용성 그룹의 클러스터 유형이 없음으로 구성되어 있으면 Windows Server 및 Linux뿐만 아니라 여러 Linux 배포판에 걸쳐 있을 수 있습니다. 이것은 실제 고가용성 구성이 아니기 때문에 업무상 중요한 배포에는 사용하지 말고 읽기 규모 조정 또는 마이그레이션/업그레이드 시나리오에 사용해야 합니다.

## <a name="log-shipping"></a>로그 전달

로그 전달은 백업 및 복원만을 기반으로 하기 때문에 Windows Server의 SQL Server와 Linux의 SQL Server에 대한 데이터베이스, 파일 구조 등에 차이가 없습니다. 즉, 로그 전달은 Windows Server 기반 SQL Server 설치와 Linux 배포 사이 및 Linux 배포간에 구성될 수 있습니다. 나머지는 모두 동일하게 유지됩니다. 유일한 주의 사항은 가용성 그룹과 마찬가지로 로그 전달은 대상이 SQL Server 하위 버전에 있고 원본이 SQL Server 상위 버전에 있는 경우에 작동할 수 없다는 점입니다. 

## <a name="read-scale"></a><a name = "ReadScaleOut"></a> 읽기 확장

SQL Server 2012에서 도입된 이후, 보조 복제본은 읽기 전용 쿼리에 사용될 수 있습니다. 가용성 그룹으로 작업을 수행할 수 있는 방법은 두 가지 입니다. 보조 복제본에 직접 액세스를 허용하는 방법과 [읽기 전용 라우팅을 구성](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)하는 방법입니다. 후자 경우 수신기를 사용해야 합니다.  SQL Server 2016에는 읽기 가능한 모든 복제본에 읽기 전용 요청을 분산할 수 있는 라운드 로빈 알고리즘을 사용하여 수신기를 통해 읽기 전용 연결의 부하를 분산할 수 있는 기능이 도입되었습니다. 

> [!NOTE]
> 읽기 가능한 보조 복제본은 Enterprise Edition에만 포함되는 기능이며 읽기 가능한 복제본을 호스트하는 각 인스턴스에는 SQL Server 라이선스가 필요합니다.

가용성 그룹을 통해 데이터베이스의 읽기 가능한 복사본을 확장하는 것은 SQL Server 2016의 분산형 가용성 그룹에서 처음 도입되었습니다. 이를 통해 기업들은 최소한의 구성으로 로컬뿐만 아니라 지역적으로, 전 세계적으로 데이터베이스의 읽기 전용 복사본을 확보할 수 있고 로컬에서 쿼리를 실행하여 네트워크 트래픽 및 대기 시간을 줄일 수 있습니다. 가용성 그룹에 있는 각각의 주 복제본은 완전한 읽기/쓰기 복사본이 아니더라도 두 개의 다른 가용성 그룹을 시드할 수 있기 때문에 분산형 가용성 그룹마다 읽기 가능한 데이터의 복사본을 최대 27개까지 지원할 수 있습니다. 

![읽기 확장과 관련된 분산형 가용성 그룹 다이어그램](media/sql-server-ha-story/image11.png)

SQL Server 2017부터 클러스터 유형이 없음으로 구성된 가용성 그룹을 사용하여 거의 실시간에 가까운 읽기 전용 솔루션을 만들 수 있습니다. 가용성을 위해서가 아니라 읽기 가능 보조 복제본을 위해 가용성 그룹을 사용하는 것이 목표인 경우에는 이렇게 하면 WSFC 또는 Pacemaker를 사용하는 복잡성이 없어지고 비교적 단순한 배포 방법으로 가용성 그룹의 읽기 편익을 확보할 수 있습니다. 

유일한 주의 사항은 클러스터 유형이 없음인 경우 기본 클러스터가 없으므로 읽기 전용 라우팅을 구성하는 것이 약간 다르다는 것입니다. SQL Server 측면에서 볼 때 클러스터가 없더라도 요청을 라우팅하려면 수신가 여전히 필요합니다. 기존 수신기를 구성하는 대신 주 복제본의 IP 주소 또는 이름이 사용됩니다. 그런 다음 주 복제본을 사용하여 읽기 전용 요청을 라우팅합니다.

로그 전달 웜 대기는 데이터베이스를 대기 상태로 복원하여 기술적으로 읽을 수 있는 용도로 구성할 수 있습니다. 하지만 트랜잭션 로그는 복원을 위해 데이터베이스를 독점적으로 사용해야 하므로 복원을 수행하는 동안은 사용자가 데이터베이스에 액세스할 수 없습니다. 이런 이유로 특히 거의 실시간으로 데이터가 필요한 경우에는 로그 전달이 이상적인 솔루션은 아닙니다. 

가용성 그룹을 사용한 모든 읽기 확장 시나리오에서 주목해야 하는 한 가지 사항은 모든 데이터가 실제로 존재하는 트랜잭션 복제를 사용하는 것과 달리 각각의 보조 복제본은 고유 인덱스를 적용할 수 있는 상태가 아니며 복제본은 주 복제본의 정확한 복사본이라는 점입니다. 즉, 보고를 위해 인덱스가 필요하거나 데이터를 조작해야 하는 경우 주 복제본의 데이터베이스에서 수행해야 합니다. 이러한 유연성이 필요한 경우 복제는 읽기 가능한 데이터를 위한 더 좋은 솔루션입니다.

## <a name="summary"></a>요약

SQL Server 2017의 인스턴스 및 데이터베이스는 Windows Server와 Linux에서 동일한 기능을 사용하여 가용성을 높일 수 있습니다. 로컬 고가용성 및 재해 복구에 대한 표준 가용성 시나리오 외에 업그레이드 및 마이그레이션과 관련된 가동 중지 시간도 SQL Server의 가용성 기능을 사용하면 최소화할 수 있습니다. 가용성 그룹은 읽기 가능 복사본을 확장하기 위해 동일한 아키텍처의 일부로 데이터베이스의 추가 복사본을 제공할 수도 있습니다. SQL Server 2017을 사용하여 새 솔루션을 배포하든 업그레이드를 고려하든 관계없이 SQL Server 2017는 필요한 가용성과 안정성을 제공합니다.
 
[SimpleAG]:media\sql-server-ha-story\image1.png
[SSMSAGOptions]:media\sql-server-ha-story\image2.png
[BasicFCI]:media\sql-server-ha-story\image3.png
[PostFailoverFCI]:media\sql-server-ha-story\image4.png
[LogShipping]:media\sql-server-ha-story\image5.png
[AG]:media\sql-server-ha-story\image6.png
[DAG]:media\sql-server-ha-story\image7.png
[AlwaysOnFCI]:media\sql-server-ha-story\image8.png
[BasicDAG]:media\sql-server-ha-story\image9.png
[image10]:media\sql-server-ha-story\image10.png
[DAG]:media\sql-server-ha-story\image11.png