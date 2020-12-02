---
title: max worker threads 서버 구성 옵션 구성 | Microsoft Docs
description: 최대 작업자 스레드 옵션을 사용하여 SQL Server에서 특정 요청을 처리하는 데 사용할 수 있는 작업자 스레드 수를 구성하는 방법을 알아봅니다.
ms.custom: contperfq4
ms.date: 04/14/2020
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- worker threads [SQL Server]
- max worker threads option
ms.assetid: abeadfa4-a14d-469a-bacf-75812e48fac1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e1f2398e59fb7a0fee48f2d4c4e4a171c6044ca7
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127422"
---
# <a name="configure-the-max-worker-threads-server-configuration-option"></a>max worker threads 서버 구성 옵션 구성
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 항목에서는 **또는** 을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]max worker threads[!INCLUDE[tsql](../../includes/tsql-md.md)] 서버 구성 옵션을 구성하는 방법에 대해 설명합니다. **최대 작업자 스레드** 옵션은 쿼리 요청, 로그인, 로그아웃 및 유사한 애플리케이션 요청을 처리하는 데 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전체에 사용할 수 있는 작업자 스레드 수를 구성합니다.


[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 운영 체제의 네이티브 스레드 서비스를 사용하여 다음 조건을 확인합니다.

- 하나 이상의 스레드는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 지원하는 각 네트워크를 동시에 지원합니다.

- 하나의 스레드가 데이터베이스 검사점을 처리합니다.

- 스레드 풀은 모든 사용자를 처리합니다.

**max worker threads** 의 기본값은 0입니다. 이 값을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 시작할 때 작업자 스레드 수가 자동으로 구성됩니다. 기본 설정은 대부분의 시스템에 적합합니다. 그러나 시스템 구성에 따라 **max worker threads** 를 특정 값으로 설정하면 성능이 향상되기도 합니다.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   실제 쿼리 요청 수는 **최대 작업자 스레드** 에 설정된 값을 초과할 수 있으며, 이 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 다음에 사용할 수 있는 작업자 스레드가 요청을 처리할 수 있도록 작업자 스레드를 풀링합니다. 작업자 스레드는 활성 요청에만 할당되며 요청이 처리되면 해제됩니다. 이는 요청이 수행된 사용자 세션/연결이 열린 상태로 유지되는 경우에도 마찬가지입니다. 

-   **최대 작업자 스레드** 서버 구성 옵션은 엔진 안에서 생성될 수 있는 모든 스레드를 제한하는 것은 아닙니다. LazyWriter, 검사점, 로그 기록기, Service Broker, 잠금 관리자 등은 이 제한에서 벗어나 생성됩니다. 가용성 그룹은 **최대 작업자 스레드 한도** 내에서 일부 작업자 스레드를 사용하지만 시스템 스레드도 사용합니다([가용성 그룹별 스레드 사용량](../availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md#ThreadUsage) 참조). 구성된 스레드 수가 초과되면 다음 쿼리는 추가 스레드를 생성한 시스템 작업에 대한 정보를 제공합니다.  
  
 ```sql  
 SELECT  s.session_id, r.command, r.status,  
    r.wait_type, r.scheduler_id, w.worker_address,  
    w.is_preemptive, w.state, t.task_state,  
    t.session_id, t.exec_context_id, t.request_id  
 FROM sys.dm_exec_sessions AS s  
 INNER JOIN sys.dm_exec_requests AS r  
    ON s.session_id = r.session_id  
 INNER JOIN sys.dm_os_tasks AS t  
    ON r.task_address = t.task_address  
 INNER JOIN sys.dm_os_workers AS w  
    ON t.worker_address = w.worker_address  
 WHERE s.is_user_process = 0;  
 ```  
  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   이 옵션은 고급 옵션으로, 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 전문가만이 변경해야 합니다. 성능 문제가 의심되는 경우 작업자 스레드 가용성 문제는 아닙니다. 작업자 스레드를 점유하고 해제하지 않는 활동과 관련된 원인일 가능성이 높습니다. 이러한 예로는 장기 대기 쿼리를 야기하는 시스템의 장기 실행 쿼리 또는 병목 현상(I/O, 차단, 래치 대기, 네트워크 대기)이 있습니다. 최대 작업자 스레드 설정이 변경하기 전에 성능 문제의 근본 원인을 찾는 것이 가장 좋습니다. 성능 평가에 대한 자세한 내용은 [성능 모니터링 및 조정](../../relational-databases/performance/monitor-and-tune-for-performance.md)을 참조하세요.
  
-   스레드 풀링은 서버에 연결된 클라이언트가 많은 경우 성능 최적화에 도움이 됩니다. 보통 각 쿼리 요청마다 별도의 운영 체제 스레드가 생성됩니다. 그러나 서버에 대한 연결 수가 수백 개인 경우 쿼리 요청별로 스레드를 하나씩 사용하면 시스템 리소스를 상당히 많이 소비하게 될 수 있습니다. **max worker threads** 옵션을 사용하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 작업자 스레드 풀을 만들어 많은 쿼리 요청을 처리할 수 있으므로 성능이 향상됩니다.  
  
-   다음 표에서는 **_기본 최대 작업자_ + ((* 논리 CPU* - 4) * *CPU당 작업자*)**와 같은 수식을 사용하여 CPU, 컴퓨터 아키텍처 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 다양한 조합에 대해 자동으로 구성된 최대 작업자 스레드 수(값이 0으로 설정된 경우)를 보여 줍니다.  
  
    |CPU 수|32비트 컴퓨터(최대 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)])|64비트 컴퓨터(최대 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1)|64비트 컴퓨터([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터)|   
    |------------|------------|------------|------------|  
    |\< = 4|256|512|512|   
    |8|288|576|576|   
    |16|352|704|704|   
    |32|480|960|960|   
    |64|736|1472|1472|   
    |128|1248|2496|4480|   
    |256|2272|4544|8576|   
    
    최대 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1에서 *CPU당 작업자* 는 다음 아키텍처(32비트 또는 64비트)에 따라서만 달라집니다.
    
    |CPU 수|32비트 컴퓨터 <sup>1</sup>|64비트 컴퓨터|   
    |------------|------------|------------|   
    |\< = 4|256|512|   
    |\> 4|256 + ((논리 CPU 수 - 4) * 8)|512 <sup>2</sup> + ((논리 CPU 수 - 4) * 16)|   
    
    [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 *CPU당 작업자* 는 다음 프로세스의 아키텍처 및 수(4와 64 간 또는 64 초과)에 따라 달라집니다.
    
    |CPU 수|32비트 컴퓨터 <sup>1</sup>|64비트 컴퓨터|   
    |------------|------------|------------|   
    |\< = 4|256|512|   
    |\> 4 및 \< = 64|256 + ((논리 CPU 수 - 4) * 8)|512 <sup>2</sup> + ((논리 CPU 수 - 4) * 16)|   
    |\> 64|256 + ((논리 CPU 수 - 4) * 32)|512 <sup>2</sup> + ((논리 CPU 수 - 4) * 32)|   
  
    <sup>1</sup> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 32비트 운영 체제에 더 이상 설치할 수 없습니다. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 및 이전 버전을 실행하는 고객을 돕기 위해 32비트 컴퓨터 값을 나열합니다. 32비트 컴퓨터에서 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 최대 작업자 스레드 수는 1,024로 설정하는 것이 좋습니다.
    
    <sup>2</sup> [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]부터 2GB 미만의 메모리를 사용하는 컴퓨터에 대해 *기본 최대 작업자* 값이 2로 나뉩니다.
  
    > [!TIP]  
    > 64개가 넘는 CPU 사용에 대한 권장 사항은 [64개를 초과하는 CPU가 있는 컴퓨터에서 SQL Server를 실행하기 위한 최선의 방법](../../relational-databases/thread-and-task-architecture-guide.md#best-practices-for-running-sql-server-on-computers-that-have-more-than-64-cpus)을 참조하세요.  
  
-   장기 실행 쿼리의 모든 작업자 스레드가 활성 상태이면 작업자 스레드가 완료되어 사용 가능 상태가 되기 전에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 응답하지 않을 수 있습니다. 이는 오류는 아니지만 바람직한 상태는 아닙니다. 프로세스가 응답할 수 없고 새 쿼리를 처리할 수 없으면 DAC(관리자 전용 연결)를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결한 다음 해당 프로세스를 중지합니다. 이를 방지하려면 max worker threads 수를 증가시킵니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 매개 변수 없이 또는 첫 번째 매개 변수만 사용하여 **sp_configure** 를 실행할 수 있는 권한은 기본적으로 모든 사용자에게 부여됩니다. 구성 옵션을 변경하거나 `RECONFIGURE` 문을 실행하는 두 매개 변수를 사용하여 **sp_configure** 를 실행하려면 사용자에게 `ALTER SETTINGS` 서버 수준 권한이 있어야 합니다. **sysadmin** 및 **serveradmin** 고정 서버 역할은 `ALTER SETTINGS` 권한을 암시적으로 보유하고 있습니다.  
  
##  <a name="using-ssmanstudiofull"></a><a name="SSMSProcedure"></a> 사용 중 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>최대 작업자 스레드 수 옵션을 구성하려면  
  
1.  개체 탐색기에서 서버를 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택합니다.  
  
2.  **프로세서** 노드를 클릭합니다.  
  
3.  **max worker threads** 입력란에 128~32,767 범위의 값을 입력하거나 선택합니다.  
  
> [!TIP]
> **max worker threads** 옵션을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 프로세스에 사용할 수 있는 작업자 스레드 수를 구성할 수 있습니다. 대부분의 시스템에는 **max worker threads** 의 기본 설정을 사용하는 것이 최상의 방법입니다. 그러나 시스템 구성에 따라 **max worker threads** 를 더 작은 값으로 설정하면 성능이 향상되기도 합니다.
> 자세한 내용은 이 페이지의 [권장 사항](#Recommendations)을 참조하세요.
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-configure-the-max-worker-threads-option"></a>최대 작업자 스레드 수 옵션을 구성하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다. 이 예제에서는 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) 를 사용하여 `max worker threads` 옵션을 `900`으로 구성하는 방법을 보여 줍니다.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'max worker threads', 900 ;  
GO  
RECONFIGURE;  
GO  
```  
  
##  <a name="follow-up-after-you-configure-the-max-worker-threads-option"></a><a name="FollowUp"></a> 후속 작업: 최대 작업자 스레드 수 옵션을 구성한 후  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]를 다시 시작할 필요 없이 [RECONFIGURE](../../t-sql/language-elements/reconfigure-transact-sql.md)을 실행하면 변경 사항이 즉시 적용됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [서버 구성 옵션&#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [데이터베이스 관리자를 위한 진단 연결](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)
