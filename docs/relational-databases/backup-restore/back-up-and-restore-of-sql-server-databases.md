---
title: SQL Server 데이터베이스 백업 및 복원 | Microsoft 문서
description: 이 문서에서는 SQL Server 데이터베이스 백업의 이점을 설명하고 백업 및 복원 전략과 보안 고려 사항을 소개합니다.
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], see restoring [SQL Server]
- backups [SQL Server]
- restoring databases [SQL Server]
- backup [SQL Server], see backing up [SQL Server]
- databases [SQL Server], restoring
- backing up databases [SQL Server]
- restore [SQL Server], see restoring [SQL Server]
- disaster recovery [SQL Server], see backing up [SQL Server]
- backing up [SQL Server]
- Database Engine [SQL Server], backups
- databases [SQL Server], backups
ms.assetid: 570a21b3-ad29-44a9-aa70-deb2fbd34f27
author: cawrites
ms.author: chadam
ms.openlocfilehash: b6e369cc3677e399182f631885afdfb3b3ac53ee
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129411"
---
# <a name="back-up-and-restore-of-sql-server-databases"></a>SQL Server 데이터베이스 백업 및 복원
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 아티클에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 백업의 이점과 기본 백업 및 복원 용어에 대해 설명하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 백업 및 복원 전략과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 및 복원을 위한 보안 고려 사항에 대해 소개합니다. 

> 이 문서에서는 SQL Server 백업을 소개합니다. SQL Server 데이터베이스를 백업하는 구체적 단계는 [백업 만들기](#creating-backups)를 참조하세요.
  
 SQL Server 백업 및 복원 구성 요소는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장된 중요한 데이터를 보호하기 위한 필수 보호 방법을 제공합니다. 치명적인 데이터 손실 위험을 최소화하려면 정기적으로 데이터베이스를 백업하여 수정 내용을 보존해야 합니다. 잘 계획된 백업 및 복원 전략은 다양한 오류로 인한 데이터 손실을 막아줍니다. 백업 세트를 복원하고 데이터베이스를 복구하는 방법으로 전략을 테스트하여 재해에 효과적으로 대응할 수 있도록 준비하세요.
  
 백업을 저장하기 위한 로컬 스토리지 외에도 SQL Server는 Azure Blob Storage 서비스로의 백업 및 복원도 지원합니다. 자세한 내용은 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요. Microsoft Azure Blob Storage 서비스를 사용하여 스토리지된 데이터베이스 파일의 경우 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 은(는) 거의 즉시 백업 및 빠른 복원에 Azure 스냅샷을 사용하는 옵션을 제공합니다. 자세한 내용은 [Azure에서 데이터베이스 파일에 대한 파일-스냅샷 Backup](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요. Azure는 Azure VM에서 실행 중인 SQL Server에 대한 엔터프라이즈 클래스 백업 솔루션도 제공합니다. 완전히 관리되는 백업 솔루션인 Azure는 Always On 가용성 그룹, 장기 보존, 지정 시간 복구, 중앙 관리 및 모니터링을 지원합니다. 자세한 내용은 [Azure VM에서 SQL Server에 대한 Azure Backup](/azure/backup/backup-azure-sql-database)을 참조하세요.
  
##  <a name="why-back-up"></a>백업 이유  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 백업하고 백업에 대한 테스트 복원 절차를 실행한 다음 안전한 오프 사이트 위치에 백업을 저장하여 치명적인 데이터 손실을 방지할 수 있습니다. **백업은 데이터를 보호하는 유일한 방법입니다.**

     유효한 데이터베이스 백업을 사용하여 다음의 여러 오류로부터 데이터를 복구할 수 있습니다.  
  
    -   미디어 오류    
    -   사용자 오류(예: 실수로 테이블 삭제)    
    -   하드웨어 오류(예: 손상된 디스크 드라이브 또는 서버의 영구적 손실)    
    -   자연 재해 Azure Blob Storage 서비스로 SQL Server 백업을 사용하면 온-프레미스 위치에 영향을 미치는 자연 재해가 발생할 경우에 사용할 오프사이트 백업을 온-프레미스 위치와 다른 영역에 만들 수 있습니다.  
  
-   또한 데이터베이스 백업은 서버 간 데이터베이스 복사, [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 또는 데이터베이스 미러링 설정, 보관 등의 일상적인 관리 용도로 유용하게 사용할 수 있습니다.  
  
##  <a name="glossary-of-backup-terms"></a>백업 용어 설명
 **백업** [동사]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터 레코드를 복사하거나 트랜잭션 로그에서 로그 레코드를 복사하여 **백업[명사]** 을 만드는 프로세스입니다.  
  
 **백업** [명사]  
 오류가 발생한 이후에 데이터를 복원 및 복구하는 데 사용할 수 있는 데이터 복사본입니다. 데이터베이스 백업을 사용하여 데이터베이스 복사본을 새 위치에 복원할 수도 있습니다.  
  
**백업** 디바이스  
 SQL Server 백업이 기록되는 대상이자 백업을 복원하는 원본이 되는 디스크 또는 테이프 디바이스입니다. SQL Server 백업은 Azure Blob Storage 서비스에 기록할 수도 있으며 백업 파일의 대상과 이름을 지정하기 위해 **URL** 형식이 사용됩니다. 자세한 내용은 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요.  
  
**백업 미디어**  
 하나 이상의 백업이 기록된 하나 이상의 테이프 또는 디스크 파일입니다.  
  
**데이터 백업(data backup)**  
 전체 데이터베이스(데이터베이스 백업), 부분 데이터베이스(부분 백업) 또는 데이터 파일 집합이나 파일 그룹(파일 백업)의 데이터 백업입니다.  
  
**데이터베이스 백업(database backup)**  
 데이터베이스 백업입니다. 전체 데이터베이스 백업은 백업이 완료된 시점의 전체 데이터베이스를 나타냅니다. 차등 데이터베이스 백업은 가장 최근의 전체 데이터베이스 백업 이후에 데이터베이스에 수행된 변경 내용만 포함합니다.  
  
**차등 백업(differential backup)**  
 전체 또는 부분 데이터베이스, 데이터 파일 집합 또는 파일 그룹(차등 기반)에 대한 최신 전체 백업을 기반으로 하고, 해당 기준 이후에 변경된 데이터만 포함하는 데이터 백업입니다.  
  
**전체 백업(full backup)**  
 특정 데이터베이스나 파일 그룹 또는 파일 집합에 있는 모든 데이터와 그러한 데이터를 복구할 수 있을 만큼의 로그를 포함하는 데이터 백업입니다.  
  
**로그 백업(log backup)**  
 이전 로그 백업에서 백업되지 않은 모든 로그 레코드를 포함하는 트랜잭션 로그 백업입니다. (전체 복구 모델)  
  
**recover**  
 데이터베이스를 안정적이고 일관된 상태로 되돌립니다.  
  
**recovery**  
 데이터베이스를 일관된 트랜잭션 상태로 가져오는 데이터베이스 시작 단계 또는 restore with recovery 단계입니다.  
  
**복구 모델**  
 데이터베이스에서 트랜잭션 로그 유지 관리를 제어하는 데이터베이스 속성입니다. 사용할 수 있는 복구 모델은 3가지로 단순, 전체 및 대량 로그 복구 모델입니다. 데이터베이스의 복구 모델에 따라 백업 및 복원 요구 사항이 결정됩니다.  
  
**복원(restore)**  
 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업에서 지정된 데이터베이스로 모든 데이터 및 로그 페이지를 복사하고 기록된 변경 사항을 적용하여 데이터를 최신 상태로 전환함으로써 백업에 기록된 모든 트랜잭션을 롤포워드하는 다단계 프로세스입니다.  
  
 ##  <a name="backup-and-restore-strategies"></a>백업 및 복원 전략  
 데이터 백업 및 복원은 특정 환경에 맞게 사용자 지정되어야 하며 적절한 리소스도 마련되어야 합니다. 따라서 복구를 위해 백업 및 복원을 안정적으로 사용하려면 백업 및 복원 전략이 필요합니다. 잘 디자인된 백업 및 복원 전략은 백업 유지 관리 및 저장 비용을 고려하면서 최대 데이터 가용성 및 최소 데이터 손실을 위한 비즈니스 요구 사항의 균형을 조정합니다.  

 백업 및 복원 전략은 백업에 관련된 부분과 복원에 관련된 부분으로 이루어집니다. 전략의 백업 관련 부분에서는 백업 유형 및 빈도, 백업에 필요한 하드웨어의 특성 및 속도, 백업 테스트 방법 및 백업 미디어 보관 위치 및 보관 방법(보안 고려 사항 포함)을 정의합니다. 전략의 복원 관련 부분에서는 복원 담당자, 데이터베이스 가용성 및 데이터 손실 최소화 목표를 충족하기 위해 복원을 수행하는 방법, 복원 테스트 방법을 정의합니다. 
  
 효과적인 백업 및 복원 전략 설계를 위해서는 신중한 계획, 구현 및 테스트가 필요합니다. 테스트 필요: 복원 전략에 포함된 모든 조합의 백업을 성공적으로 복원하고 복원된 데이터베이스의 물리적 일관성을 테스트해야만 백업 전략이 완성됩니다. 다음과 같은 다양한 요소를 이러한 개체는 다음과 같습니다.  
  
- 프로덕션 데이터베이스와 관련된 조직의 목표(특히, 가용성과 데이터 손실 또는 손상 방지 요구 사항)  
  
-  각 데이터베이스의 특성: 크기, 사용 패턴, 콘텐츠 특성, 데이터 요구 사항 등  
  
-   하드웨어, 인력, 백업 미디어 저장 공간, 저장된 미디어의 물리적 보안 등과 같은 리소스의 제약 요건  

## <a name="best-practice-recommendations"></a>모범 사례 권장 사항

### <a name="use-separate-storage"></a>별도의 스토리지 사용 
> [!IMPORTANT] 
> 데이터베이스 파일과는 별도의 물리적 위치 또는 디바이스에 데이터베이스 백업을 저장해야 합니다. 데이터베이스를 저장하는 실제 드라이브가 오작동하거나 충돌하는 경우, 복구 기능은 복원을 수행하기 위해 백업을 저장한 별도의 드라이브나 원격 디바이스에 액세스할 수 있는지 여부에 따라 달라집니다. 동일한 실제 디스크 드라이브에서 여러 개의 논리 볼륨이나 파티션을 만들 수 있다는 것에 유의하세요. 백업의 스토리지 위치를 선택하기 전에 디스크 파티션 및 논리 볼륨 레이아웃을 신중하게 검토합니다.

### <a name="choose-appropriate-recovery-model"></a>적절한 복구 모델 선택
 백업 및 복원 작업은 [복구 모델](../backup-restore/recovery-models-sql-server.md)의 컨텍스트에서 수행됩니다. 복구 모델은 트랜잭션 로그의 관리 방법을 제어하는 데이터베이스 속성입니다. 따라서 데이터베이스 복구 모델은 데이터베이스에 지원되는 복원 시나리오 및 백업 유형과 트랜잭션 로그 백업의 크기를 결정합니다. 일반적으로 데이터베이스는 단순 복구 모델 또는 전체 복구 모델 중 하나를 사용합니다. 전체 복구 모델은 대량 작업 이전에 대량 로그된 복구 모델로 전환하여 보강할 수 있습니다. 이러한 복구 모델 및 이러한 복구 모델이 트랜잭션 로그 관리에 미치는 영향에 대한 자세한 내용은 [트랜잭션 로그(SQL Server)](../logs/the-transaction-log-sql-server.md)를 참조하세요.  
  
 데이터베이스에 가장 적합한 복구 모델은 비즈니스 요구 사항에 따라 달라집니다. 트랜잭션 로그 관리를 방지하고 백업 및 복원을 단순화하려면 단순 복구 모델을 사용하십시오. 관리 오버헤드가 증가하더라도 작업 손실 가능성을 최소화하려면 전체 복구 모델을 사용하십시오. 대량 로그된 작업 중 로그 크기에 미치는 영향을 최소화하는 동시에 이러한 작업의 복구를 허용하려면 대량 로그된 복구 모델을 사용합니다. 백업 및 복원에 미치는 복구 모델의 영향에 대한 자세한 내용은 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)을 참조하세요.  
  
### <a name="design-your-backup-strategy"></a>백업 전략 디자인  
 지정한 데이터베이스에 대해 비즈니스 요구 사항에 맞는 복구 모델을 선택한 후에는 해당 백업 전략을 계획 및 구현해야 합니다. 백업 전략을 최적화하는 요소는 다양합니다. 그 중에서도 특히 다음과 같은 요소에 의해 주로 영향을 받습니다.  
  
-   애플리케이션이 하루에 몇 시간 데이터베이스에 액세스해야 합니까?  
  
     사용량이 적은 기간을 예측할 수 있는 경우 해당 기간에 전체 데이터베이스 백업을 예약하는 것이 좋습니다.  
  
-   얼마나 자주 변경과 업데이트가 발생합니까?  
  
     자주 변경하는 경우 다음을 고려하십시오.  
  
    -   단순 복구 모델에서는 전체 데이터베이스 백업 사이에 차등 백업을 예약하십시오. 차등 백업은 마지막 전체 데이터베이스 백업 이후의 변경 내용만 캡처합니다.  
  
    -   전체 복구 모델에서는 자주 로그 백업을 예약해야 합니다. 전체 백업 사이에 차등 백업을 예약하면 데이터를 복원한 후 복원해야 하는 로그 백업 수가 감소하므로 복원 시간이 줄어들 수 있습니다.  
  
-   변경이 데이터베이스의 일부분에서만 발생합니까? 아니면 데이터베이스의 대부분에서 발생합니까?  
  
     변경 내용이 파일 또는 파일 그룹의 일부분에만 집중되어 있는 큰 데이터베이스의 경우 부분 백업이나 파일 백업이 유용할 수 있습니다. 자세한 내용은 [부분 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md) 및 [전체 파일 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md)을 참조하세요.  
  
-   전체 데이터베이스 백업에 필요한 디스크 공간은 어느 정도입니까?  
-   비즈니스에서 과거 어느 시점까지 백업을 유지 관리해야 합니까? 

    애플리케이션 및 비즈니스 요구 사항에 따라 적절한 백업 일정을 설정했는지 확인합니다. 백업한 지 오래되면 실패 시점까지 모든 데이터를 다시 생성하는 방법이 없을 경우 데이터 손실 위험이 커집니다. 스토리지 리소스 제한으로 인해 오래된 백업 삭제를 선택하기 전에 해당 시점까지 복구 기능이 필요한지를 고려합니다.

  
 ### <a name="estimate-the-size-of-a-full-database-backup"></a>전체 데이터베이스 백업의 크기 예측  
 백업 및 복원을 구현하기 전에 전체 데이터베이스 백업에 어느 정도의 디스크 공간이 필요한지 예측해야 합니다. 백업 작업은 데이터베이스의 데이터를 백업 파일로 복사합니다. 백업에는 데이터베이스의 실제 데이터만 포함되고 사용하지 않은 공간은 포함되지 않습니다. 따라서 백업은 일반적으로 데이터베이스 자체의 크기보다 작습니다. **sp_spaceused** 시스템 저장 프로시저를 사용하여 전체 데이터베이스 백업의 크기를 예측할 수 있습니다. 자세한 내용은 [sp_spaceused&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)를 참조하세요.  
  
### <a name="schedule-backups"></a>백업 예약  
 백업 작업을 수행해도 실행 중인 트랜잭션에는 큰 영향을 미치지 않으므로 일반 작업을 수행할 때도 백업 작업을 실행할 수 있습니다. 프로덕션 작업에 거의 영향을 주지 않고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업을 수행할 수 있습니다.  
   
>  백업 중 동시성 제한 사항에 대한 자세한 내용은 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)을 참조하세요.  
  
 각 경우에 필요한 백업 유형과 수행 빈도를 결정한 후 데이터베이스 유지 관리 계획의 일부로 데이터베이스에 대한 정기 백업을 예약하는 것이 좋습니다. 유지 관리 계획에 대한 정보와 데이터베이스 백업 및 로그 백업에 대한 유지 관리 계획을 만드는 방법은 [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)를 참조하십시오.
  
### <a name="test-your-backups"></a>백업 테스트  
 백업을 테스트해야만 복원 전략을 갖추게 됩니다. 데이터베이스 복사본을 테스트 시스템으로 복원하여 각 데이터베이스에 대한 백업 전략을 철저히 테스트하는 것이 중요합니다. 사용할 모든 유형의 백업 복원을 테스트해야 합니다. 백업을 복원한 후에 데이터베이스의 DBCC CHECKDB를 통해 데이터베이스 일관성 검사를 수행하여 백업 미디어가 손상되지 않았는지 확인하는 것이 좋습니다. 

### <a name="verify-media-stability-and-consistency"></a>미디어 안정성 및 일관성 확인
백업 유틸리티(BACKUP T-SQL 명령, SQL Server 유지 관리 계획, 백업 소프트웨어 또는 솔루션 등)에서 제공하는 확인 옵션을 사용합니다. 예를 보려면 [RESTORE VERIFYONLY] (../t-sql/statements/restore-statements-verifyonly-transact-sql.md)를 참조하세요. BACKUP CHECKSUM과 같은 고급 기능을 사용하여 백업 미디어 자체의 문제를 검색합니다. 자세한 내용은 [백업 및 복원 중 발생 가능한 미디어 오류(SQL Server)](../backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)를 참조하세요.

### <a name="document-backuprestore-strategy"></a>백업/복원 전략 문서화 
백업 및 복원 절차를 문서화하고 실행 문서에 사본을 보관하는 것이 좋습니다.
또한 각 데이터베이스의 작업 매뉴얼을 유지 관리하는 것이 좋습니다. 이 작업 매뉴얼에는 백업 위치, 백업 디바이스 이름(있는 경우) 및 테스트 백업을 복원하는 데 필요한 시간 등이 수록되어야 합니다.



## <a name="monitor-progress-with-xevent"></a>xEvent를 사용하여 진행률 모니터
백업 및 복원 작업은 데이터베이스의 크기 및 작업의 복잡성으로 인해 시간이 많이 걸릴 수 있습니다. 작업에 문제가 발생하는 경우 **backup_restore_progress_trace** 확장된 이벤트를 사용하여 진행 상황을 실시간으로 모니터링할 수 있습니다. 확장 이벤트에 대한 자세한 내용은 [확장 이벤트](../extended-events/extended-events.md)를 참조하세요.

  >[!WARNING]
  > backup_restore_progress_trace 확장된 이벤트를 사용하면 성능 문제를 일으키고 많은 양의 디스크 공간을 사용할 수 있습니다. 짧은 기간 동안 사용하고, 주의하고 프로덕션에서 구현하기 전에 철저히 테스트합니다.


```sql
-- Create the backup_restore_progress_trace extended event esssion
CREATE EVENT SESSION [BackupRestoreTrace] ON SERVER 
ADD EVENT sqlserver.backup_restore_progress_trace
ADD TARGET package0.event_file(SET filename=N'BackupRestoreTrace')
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=5 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)
GO

-- Start the event session  
ALTER EVENT SESSION [BackupRestoreTrace]  
ON SERVER  
STATE = start;  
GO  

-- Stop the event session  
ALTER EVENT SESSION [BackupRestoreTrace]  
ON SERVER  
STATE = stop;  
GO  
```

### <a name="sample-output-from-extended-event"></a>확장된 이벤트의 샘플 출력 

![백업 xEvent 출력의 예제](media/back-up-and-restore-of-sql-server-databases/backup-xevent-example.png)
![복원 xEvent 출력의 예제](media/back-up-and-restore-of-sql-server-databases/restore-xevent-example.png)
 
  
## <a name="more-about-backup-tasks"></a>백업 태스크에 대한 자세한 정보  
-   [유지 관리 계획 만들기](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
-   [작업 만들기](../../ssms/agent/create-a-job.md)  
  
-   [작업 예약](../../ssms/agent/schedule-a-job.md)  
  
## <a name="working-with-backup-devices-and-backup-media"></a>백업 디바이스 및 백업 미디어 사용  
-   [디스크 파일에 대한 논리적 백업 디바이스 정의&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [테이프 드라이브에 대한 논리적 백업 디바이스 정의&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [디스크 또는 테이프를 백업 대상으로 지정&#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [백업 디바이스 삭제&#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [백업의 만료 날짜 설정&#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [백업 테이프 또는 파일의 내용 보기&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [백업 세트의 데이터와 로그 파일 보기&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [논리적 백업 디바이스의 속성 및 내용 보기&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [디바이스에서 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="creating-backups"></a>백업 만들기  
**참고!** 부분 또는 복사 전용 백업의 경우 각각 PARTIAL 또는 COPY_ONLY 옵션과 함께 [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md) 문을 사용해야 합니다.  
  
 ### <a name="using-ssms"></a>SSMS 사용   
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [파일 및 파일 그룹 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 ### <a name="using-t-sql"></a>T-SQL 사용  
-   [Resource Governor를 사용하여 백업 압축을 통해 CPU 사용량 제한&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [데이터베이스가 손상된 경우 트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [백업 또는 복원 중 백업 체크섬 설정 또는 해제&#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [오류 발생 후 백업 또는 복원 작업 계속 또는 중지 여부 지정&#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
## <a name="restore-data-backups"></a>데이터 백업 복원 
### <a name="using-ssms"></a>SSMS 사용 
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
  
-   [차등 데이터베이스 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-differential-database-backup-sql-server.md)  
  
-   [파일 및 파일 그룹 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
### <a name="using-t-sql"></a>T-SQL 사용
-   [단순 복구 모델에서 데이터베이스 백업 복원&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [전체 복구 모델에서 특정 오류 지점으로 데이터베이스 복원&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [기존 파일에서 파일 및 파일 그룹 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [새 위치로 파일 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [master 데이터베이스 복원&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md)  

## <a name="restore-transaction-logs-full-recovery-model"></a>트랜잭션 로그 복원(전체 복구 모델)
### <a name="using-ssms"></a>SSMS 사용  
-   [데이터베이스를 표시된 트랜잭션으로 복원&#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
 ### <a name="using-t-sql"></a>T-SQL 사용 
-   [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
 
-   [중단된 복원 작업 다시 시작&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restart-an-interrupted-restore-operation-transact-sql.md)  
  
-   [데이터를 복원하지 않고 데이터베이스 복구&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
 
## <a name="more-information-and-resources"></a>자세한 정보 및 리소스
 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [복원 및 복구 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Analysis Services 데이터베이스 백업 및 복원](/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)   
 [전체 텍스트 카탈로그와 인덱스 백업 및 복원](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 [복제된 데이터베이스 백업 및 복원](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [복구 모델&#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
