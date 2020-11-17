---
title: 가용성 그룹에서 보조 데이터베이스 제거
description: T-SQL(Transact-SQL), PowerShell 또는 SQL Server Management Studio를 사용하여 Always On 가용성 그룹에서 보조 데이터베이스를 제거하는 단계입니다.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroup.unjoindb.f1
helpviewer_keywords:
- secondary databases [SQL Server], in availability group
- Availability Groups [SQL Server], removing
- Availability Groups [SQL Server], databases
ms.assetid: 4e51a570-58d7-4f01-9390-4198f3602576
author: cawrites
ms.author: chadam
ms.openlocfilehash: 60ce75bd240c8658bbf3a8174064c017456f6225
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584017"
---
# <a name="remove-a-secondary-database-from-an-availability-group-sql-server"></a>가용성 그룹에서 보조 데이터베이스 제거(SQL Server)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[tsql](../../../includes/tsql-md.md)], [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]또는 PowerShell을 사용하여 Always On 가용성 그룹에서 보조 데이터베이스를 제거하는 방법을 설명합니다.  
   
  
##  <a name="prerequisites-and-restrictions"></a><a name="Prerequisites"></a> 사전 요구 사항 및 제한 사항  
  
-   이 태스크는 보조 복제본에서만 지원됩니다. 데이터베이스를 제거할 보조 복제본을 호스팅하는 서버 인스턴스에 연결되어 있어야 합니다.  
  
 
##  <a name="permissions"></a><a name="Permissions"></a> 권한  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **가용성 그룹에서 보조 데이터베이스를 제거하려면**  
  
1.  개체 탐색기에서 하나 이상의 보조 데이터베이스를 제거할 보조 복제본을 호스팅하는 서버 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **Always On 고가용성** 노드 및 **가용성 그룹** 노드를 확장합니다.  
  
3.  가용성 그룹을 선택하고 **가용성 데이터베이스** 노드를 확장합니다.  
  
4.  이 단계는 여러 데이터베이스 그룹을 제거할지 아니면 데이터베이스를 하나만 제거할지에 따라 다음과 같이 달라집니다.  
  
    -   여러 데이터베이스를 제거하려면 **개체 탐색기 정보** 창을 사용하여 제거할 모든 데이터베이스를 표시하고 선택합니다. 자세한 내용은 [개체 탐색기 정보를 사용하여 가용성 그룹 모니터링&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-object-explorer-details-to-monitor-availability-groups.md)을 참조하세요.  
  
    -   단일 데이터베이스를 제거하려면 **개체 탐색기** 창 또는 **개체 탐색기 정보** 창에서 데이터베이스를 선택합니다.  
  
5.  선택한 데이터베이스를 마우스 오른쪽 단추로 클릭하고 명령 메뉴에서 **보조 데이터베이스 제거** 를 선택합니다.  
  
6.  **가용성 그룹에서 데이터베이스 제거** 대화 상자에서 나열된 데이터베이스를 모두 제거하려면 **확인** 을 클릭합니다. 나열된 모든 데이터베이스를 제거하지 않으려면 **취소** 를 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 **가용성 그룹에서 보조 데이터베이스를 제거하려면**  
  
1.  보조 복제본을 호스팅하는 서버 인스턴스에 연결합니다.  
  
2.  다음과 같이 [ALTER DATABASE 문의 SET HADR 절](../../../t-sql/statements/alter-database-transact-sql-set-hadr.md) 을 사용합니다.  
  
     ALTER DATABASE *database_name* SET HADR OFF  
  
     여기서 *database_name* 은 해당 데이터베이스가 속한 가용성 그룹에서 제거할 보조 데이터베이스의 이름입니다.  
  
     다음 예에서는 가용성 그룹에서 *MyDb2* 라는 로컬 보조 데이터베이스를 제거합니다.  
  
    ```  
    ALTER DATABASE MyDb2 SET HADR OFF;  
    GO  
    ```  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> PowerShell 사용  
 **가용성 그룹에서 보조 데이터베이스를 제거하려면**  
  
1.  보조 복제본을 호스팅하는 서버 인스턴스로 디렉터리를 변경(**cd**)합니다.  
  
2.  **Remove-SqlAvailabilityDatabase** cmdlet을 사용하여 가용성 그룹에서 제거할 가용성 데이터베이스의 이름을 지정합니다. 보조 복제본을 호스팅하는 서버 인스턴스에 연결된 경우 가용성 그룹에서 로컬 보조 데이터베이스만 제거됩니다.  
  
     예를 들어 다음 명령은 `MyDb8` 서버 인스턴스가 호스팅하는 보조 복제본에서 보조 데이터베이스 `SecondaryComputer\Instance`을 제거합니다. 제거된 보조 데이터베이스에 대한 데이터 동기화가 중단됩니다. 이 명령은 주 데이터베이스 또는 다른 보조 데이터베이스에 영향을 주지 않습니다.  
  
    ```  
    Remove-SqlAvailabilityDatabase `  
    -Path SQLSERVER:\Sql\SecondaryComputer\InstanceName\AvailabilityGroups\MyAg\Databases\MyDb8  
    ```  
  
    > [!NOTE]  
    >  cmdlet의 구문을 보려면 **PowerShell 환경에서** Get-Help [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cmdlet을 사용합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="follow-up-after-removing-a-secondary-database-from-an-availability-group"></a><a name="FollowUp"></a> 후속 작업: 가용성 그룹에서 보조 데이터베이스를 제거한 후  
 보조 데이터베이스가 제거되면 이 보조 데이터베이스는 더 이상 가용성 그룹에 조인되지 않으며 제거된 보조 데이터베이스에 대한 모든 정보가 가용성 그룹에서 삭제됩니다. 제거된 보조 데이터베이스는 RESTORING 상태가 됩니다.  
  
> [!TIP]  
>  보조 데이터베이스를 제거한 후에는 짧은 기간 동안 이를 다시 가용성 그룹에 조인하여 데이터베이스에서 Always On 데이터 동기화를 다시 시작할 수 있습니다. 자세한 내용은 [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)인스턴스에 AlwaysOn 가용성 그룹을 만드는 방법을 설명합니다.  
  
 여기서 제거된 보조 데이터베이스를 다음과 같은 다른 방법으로 처리할 수 있습니다.  
  
-   보조 데이터베이스가 더 이상 필요하지 않은 경우 삭제할 수 있습니다.  
  
     자세한 내용은 [DROP DATABASE&#40;Transact-SQL&#41;](../../../t-sql/statements/drop-database-transact-sql.md) 또는 [데이터베이스 삭제](../../../relational-databases/databases/delete-a-database.md)를 참조하세요.  
  
-   가용성 그룹에서 제거된 보조 데이터베이스에 액세스하려면 데이터베이스를 복구할 수 있습니다. 그러나 제거된 보조 데이터베이스를 복구하면 같은 이름의 독립적인 두 분기 데이터베이스가 온라인 상태가 됩니다. 클라이언트가 현재 주 데이터베이스에만 액세스할 수 있는지 확인해야 합니다.  
  
     자세한 내용은 [데이터를 복원하지 않고 데이터베이스 복구&#40;Transact-SQL&#41;](../../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹에서 주 데이터베이스 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)  
  
