---
title: PowerShell을 사용하여 가용성 그룹 만들기
description: SQL Server 2019(15.x)에서 PowerShell cmdlet을 사용하여 Always On 가용성 그룹을 만들고 구성하는 방법을 알아봅니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- Availability Groups [SQL Server], creating
ms.assetid: bc69a7df-20fa-41e1-9301-11317c5270d2
author: cawrites
ms.author: chadam
ms.openlocfilehash: a408ff7289b117a1cdab5abb36be164535feb15c
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584421"
---
# <a name="create-an-always-on-availability-group-using-powershell"></a>PowerShell을 사용하여 Always On 가용성 그룹 만들기
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서 PowerShell cmdlet을 사용하여 Always On 가용성 그룹을 만들고 구성하는 방법에 대해 설명합니다. *가용성 그룹* 은 단일 단위로 장애 조치(Failover)될 사용자 데이터베이스 집합과 장애 조치(Failover)를 지원하는 장애 조치(Failover) 파트너 집합( *가용성 복제본* 이라고 함)을 정의합니다.  
  
> [!NOTE]  
> 가용성 그룹에 대한 개요를 보려면 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  
  
> [!NOTE]  
> PowerShell cmdlet을 사용하는 대신 가용성 그룹 만들기 마법사나 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용할 수도 있습니다. 자세한 내용은 [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md) 또는 [가용성 그룹 만들기&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)에서 PowerShell cmdlet을 사용하여 Always On 가용성 그룹을 만들고 구성하는 방법에 대해 설명합니다.  

## <a name="before-you-begin"></a>시작하기 전에
### <a name="prerequisites-restrictions-and-recommendations"></a><a name="PrerequisitesRestrictions"></a> 필수 구성 요소, 제한 사항 및 권장 사항  

- 가용성 그룹을 만들기 전에 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 호스트 인스턴스가 각각 단일 WSFC 장애 조치(Failover) 클러스터 내의 다른 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 노드에 있는지 확인합니다. 또한 해당 서버 인스턴스가 다른 서버 인스턴스의 사전 요구 사항을 충족하는지와 다른 모든 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 요구 사항을 충족하는지, 그리고 현재 권장 사항을 알고 있는지 확인합니다. 자세한 내용은 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](~/database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  

### <a name="permissions"></a><a name="Permissions"></a> 권한  
 CREATE AVAILABILITY GROUP 서버 권한, ALTER ANY AVAILABILITY GROUP 권한, CONTROL SERVER 권한 중 하나와 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  

## <a name="using-powershell-to-create-and-configure-an-availability-group"></a><a name="PowerShellProcedure"></a> PowerShell을 사용하여 가용성 그룹 만들기 및 구성  
 
다음 표에서는 가용성 그룹을 구성하는 데 필요한 기본 태스크와 PowerShell cmdlet이 지원하는 기능을 보여 줍니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 태스크는 표에 나오는 순서대로 수행해야 합니다.  
  
|Task|PowerShell cmdlet(사용 가능한 경우) 또는 Transact-SQL 문|태스크를 수행할 위치|  
|----------|--------------------------------------------------------------------|---------------------------------|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스당 하나의 데이터베이스 미러링 엔드포인트 만들기|**New-SqlHadrEndPoint**|데이터베이스 미러링 엔드포인트가 없는 각 서버 인스턴스에서 실행합니다.<br /><br />기존 데이터베이스 미러링 엔드포인트를 변경하려면 **Set-SqlHadrEndpoint** 를 사용합니다.|  
|가용성 그룹 만들기|먼저 **New-SqlAvailabilityReplica** cmdlet과 **-AsTemplate** 매개 변수를 사용하여 가용성 그룹에 포함할 두 개의 각 가용성 복제본에 대한 메모리 내 가용성 복제본 개체를 만듭니다.<br /><br /> 그런 다음 **New-SqlAvailabilityGroup** cmdlet을 사용하고 가용성 복제본 개체를 참조하여 가용성 그룹을 만듭니다.|초기 주 복제본을 호스트할 서버 인스턴스에서 실행합니다.|  
|가용성 그룹에 보조 복제본 조인|**Join-SqlAvailabilityGroup**|보조 복제본을 호스트할 각 서버 인스턴스에서 실행합니다.|  
|보조 데이터베이스 준비|**Backup-SqlDatabase** 및 **Restore-SqlDatabase**|주 복제본을 호스트하는 서버 인스턴스에 백업을 만듭니다.<br /><br /> **NoRecovery** 복원 매개 변수를 사용하여 보조 복제본을 호스팅하는 각 서버 인스턴스에 백업을 복원합니다. 또한 주 복제본을 호스팅하는 컴퓨터와 대상 보조 복제본을 호스팅하는 컴퓨터의 파일 경로가 다른 경우 **RelocateFile** 복원 매개 변수를 사용합니다.|  
|가용성 그룹에 각 보조 데이터베이스를 조인하여 데이터 동기화 시작|**Add-SqlAvailabilityDatabase**|보조 복제본을 호스트하는 각 서버 인스턴스에서 실행합니다.|  
  
> [!NOTE]
> 지정된 태스크를 수행하려면 표시된 서버 인스턴스로 디렉터리를 변경(**cd**)합니다.  

## <a name="using-powershell"></a>PowerShell 사용

[SQL Server PowerShell 공급자](../../../powershell/sql-server-powershell-provider.md)를 설정 및 사용합니다. 

> [!NOTE]  
> 특정 cmdlet의 구문 및 예제를 보려면 **PowerShell 환경에서** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)을 참조하세요.  

1. 주 복제본을 호스트할 서버 인스턴스로 디렉터리를 변경(**cd**)합니다.  
  
1. 주 복제본에 대한 메모리 내 가용성 복제본 개체를 만듭니다.  
  
1. 각 보조 복제본에 대한 메모리 내 가용성 복제본 개체를 만듭니다.  
  
1. 가용성 그룹을 만듭니다.  
  
    > [!NOTE]  
    > 가용성 그룹 이름의 최대 길이는 128자입니다.  

1. 새 보조 복제본을 가용성 그룹에 조인합니다. [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)을 참조하세요.  
  
1. 가용성 그룹의 각 데이터베이스에 대해 RESTORE WITH NORECOVERY를 사용하여 주 데이터베이스의 최신 백업을 복원하는 방법으로 보조 데이터베이스를 만듭니다.  
  
1. 새 보조 데이터베이스를 가용성 그룹에 모두 조인합니다. [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)을 참조하세요.  
  
1. (옵션) Windows **dir** 명령을 사용하여 새 가용성 그룹의 내용을 확인합니다.  
  
> [!NOTE]  
> 서버 인스턴스의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스 계정이 다른 도메인 사용자 계정으로 실행되는 경우에는 각 서버 인스턴스에서 다른 서버 인스턴스에 대한 로그인을 만들고 로컬 데이터베이스 미러링 엔드포인트에 이 로그인 CONNECT 권한을 부여합니다.  

### <a name="example"></a><a name="ExampleConfigureGroup"></a> 예제
다음 PowerShell 예에서는 가용성 복제본 두 개와 가용성 데이터베이스 한 개가 포함된 `<myAvailabilityGroup>` 라는 단순한 가용성 그룹을 만들고 구성합니다. 예:  

1. `<myDatabase>` 와 해당 트랜잭션 로그를 백업합니다.  

1. `<myDatabase>` -NoRecovery **옵션을 사용하여** 및 해당 트랜잭션 로그를 복원합니다.  

1. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 로컬 인스턴스에 의해 호스트될 주 복제본의 메모리 내 표현을 만듭니다( `PrimaryComputer\Instance`).  

1. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 의해 호스트될 보조 복제본의 메모리 내 표현을 만듭니다( `SecondaryComputer\Instance`).  

1. `<myAvailabilityGroup>`라는 가용성 그룹을 만듭니다.  

1. 보조 복제본을 가용성 그룹에 조인합니다.  

1. 보조 데이터베이스를 가용성 그룹에 조인합니다.  

```powershell
# Backup my database and its log on the primary  
Backup-SqlDatabase `  
    -Database "<myDatabase>" `  
    -BackupFile "\\share\backups\<myDatabase>.bak" `  
    -ServerInstance "PrimaryComputer\Instance"  
  
Backup-SqlDatabase `  
    -Database "<myDatabase>" `  
    -BackupFile "\\share\backups\<myDatabase>.log" `  
    -ServerInstance "PrimaryComputer\Instance" `  
    -BackupAction Log   
  
# Restore the database and log on the secondary (using NO RECOVERY)  
Restore-SqlDatabase `  
    -Database "<myDatabase>" `  
    -BackupFile "\\share\backups\<myDatabase>.bak" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -NoRecovery  
  
Restore-SqlDatabase `  
    -Database "<myDatabase>" `  
    -BackupFile "\\share\backups\<myDatabase>.log" `  
    -ServerInstance "SecondaryComputer\Instance" `  
    -RestoreAction Log `  
    -NoRecovery  
  
# Create an in-memory representation of the primary replica.  
$primaryReplica = New-SqlAvailabilityReplica `  
    -Name "PrimaryComputer\Instance" `  
    -EndpointURL "TCP://PrimaryComputer.domain.com:5022" `  
    -AvailabilityMode "SynchronousCommit" `  
    -FailoverMode "Automatic" `  
    -Version 12 `  
    -AsTemplate  
  
# Create an in-memory representation of the secondary replica.  
$secondaryReplica = New-SqlAvailabilityReplica `  
    -Name "SecondaryComputer\Instance" `  
    -EndpointURL "TCP://SecondaryComputer.domain.com:5022" `  
    -AvailabilityMode "SynchronousCommit" `  
    -FailoverMode "Automatic" `  
    -Version 12 `  
    -AsTemplate  
  
# Create the availability group  
New-SqlAvailabilityGroup `  
    -Name "<myAvailabilityGroup>" `  
    -Path "SQLSERVER:\SQL\PrimaryComputer\Instance" `  
    -AvailabilityReplica @($primaryReplica,$secondaryReplica) `  
    -Database "<myDatabase>"  
  
# Join the secondary replica to the availability group.  
Join-SqlAvailabilityGroup -Path "SQLSERVER:\SQL\SecondaryComputer\Instance" -Name "<myAvailabilityGroup>"  
  
# Join the secondary database to the availability group.  
Add-SqlAvailabilityDatabase -Path "SQLSERVER:\SQL\SecondaryComputer\Instance\AvailabilityGroups\<myAvailabilityGroup>" -Database "<myDatabase>"  
```  
  
## <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
 **Always On 가용성 그룹에 대한 서버 인스턴스를 구성하려면**  
  
- [Always On 가용성 그룹 활성화 및 비활성화&#40;SQL Server&#41;](~/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)  
  
- [Always On 가용성 그룹에 대한 데이터베이스 미러링 엔드포인트 만들기&#40;SQL Server PowerShell&#41;](~/database-engine/availability-groups/windows/database-mirroring-always-on-availability-groups-powershell.md)  
  
 **가용성 그룹 및 복제본 속성을 구성하려면**  
  
- [가용성 복제본의 가용성 모드 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md)  
  
- [가용성 복제본의 장애 조치(failover) 모드 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-failover-mode-of-an-availability-replica-sql-server.md)  
  
- [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
- [유연한 장애 조치(failover) 정책을 구성하여 자동 장애 조치(failover)의 상태 제어&#40;Always On 가용성 그룹&#41;](~/database-engine/availability-groups/windows/configure-flexible-automatic-failover-policy.md)  
  
- [가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
- [가용성 복제본에 백업 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
- [가용성 복제본에 대한 읽기 전용 액세스 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
- [가용성 그룹에 대한 읽기 전용 라우팅 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
- [가용성 복제본에 대한 세션 제한 시간 변경&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **가용성 그룹 구성을 완료하려면**  
  
- [가용성 그룹에 보조 복제본 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
- [가용성 그룹에 대한 보조 데이터베이스 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
- [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
- [가용성 그룹 수신기 만들기 또는 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
 **가용성 그룹을 만드는 다른 방법**  
  
- [가용성 그룹 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)  
  
- [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
- [가용성 그룹 만들기&#40;Transact-SQL&#41;](../../../database-engine/availability-groups/windows/create-an-availability-group-transact-sql.md)  
  
 **Always On 가용성 그룹 구성 문제를 해결하려면**  
  
- [Always On 가용성 그룹 구성 문제 해결&#40;SQL Server&#41;](~/database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
- [실패한 파일 추가 작업 문제 해결&#40;Always On 가용성 그룹&#41;](~/database-engine/availability-groups/windows/troubleshoot-a-failed-add-file-operation-always-on-availability-groups.md)  
  
## <a name="related-content"></a><a name="RelatedContent"></a> 관련 내용  
  
- **블로그:**  
  
     [Always On - HADRON 학습 시리즈: HADRON 지원 데이터베이스에 대한 작업자 풀 사용](/archive/blogs/psssql/alwayson-hadron-learning-series-worker-pool-usage-for-hadron-enabled-databases)  
  
     [SQL Server PowerShell을 사용하여 Always On 구성](/archive/blogs/sqlalwayson/configuring-alwayson-with-sql-server-powershell)  
  
     [SQL Server Always On 팀 블로그: 공식 SQL Server Always On 팀 블로그](/archive/blogs/sqlalwayson/)  
  
     [CSS SQL Server 엔지니어 블로그](/archive/blogs/psssql/)  
  
- **비디오:**  
  
     [Microsoft SQL Server 코드 이름 "Denali" Always On 시리즈, 1부: 차세대 고가용성 솔루션 소개](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server 코드 이름 "Denali" Always On 시리즈, 2부: Always On을 사용하여 중요 업무용 고가용성 솔루션을 구축](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
- **백서:**  
  
     [고가용성 및 재해 복구를 위한 Microsoft SQL Server Always On 솔루션 가이드](/previous-versions/sql/sql-server-2012/hh781257(v=msdn.10))  
  
     [SQL Server 2012에 대한 Microsoft 백서](https://social.technet.microsoft.com/wiki/contents/articles/13146.white-paper-gallery-for-sql-server.aspx#[Category]SQLServer2012)  
  
     [SQL Server 고객 자문 팀 백서](https://techcommunity.microsoft.com/t5/DataCAT/bg-p/DataCAT/)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 엔드포인트&#40;SQL Server&#41;](../../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)