---
title: 지연된 트랜잭션(SQL Server) | Microsoft 문서
description: SQL Server Enterprise의 지연된 트랜잭션은 롤백에 필요한 데이터가 오프라인인 경우에 발생합니다. 트랜잭션을 지연된 상태에서 벗어나게 하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- I/O [SQL Server], database recovery
- restoring pages [SQL Server]
- deferred transactions
- modifying transaction deferred state
ms.assetid: 6fc0f9b6-d3ea-4971-9f27-d0195d1ff718
author: cawrites
ms.author: chadam
ms.openlocfilehash: 8d748a5997df33ab9448fc9ba604ae700b87c0ee
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96127039"
---
# <a name="deferred-transactions-sql-server"></a>지연된 트랜잭션(SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise에서는 손상된 트랜잭션이 롤백(실행 취소)에 필요한 데이터가 데이터베이스 시작 시 오프라인 상태인 경우에 지연될 수 있습니다. *지연된 트랜잭션* 은 롤포워드 단계가 완료될 때 커밋되지 않으며, 오류로 인해 롤백할 수 없는 트랜잭션입니다. 트랜잭션을 롤백할 수 없으므로 해당 트랜잭션은 지연됩니다.  
  
> [!NOTE]  
>  손상된 트랜잭션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise에서만 지연됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 버전에서 트랜잭션이 손상되면 시작이 실패합니다.  
  
 일반적으로 데이터베이스가 롤포워드되는 동안 I/O 오류로 인해 트랜잭션에 필요한 페이지를 읽을 수 없으므로 지연된 트랜잭션이 발생합니다. 그러나 파일 수준에서의 오류로 인해 지연된 트랜잭션이 발생할 수도 있습니다. 또한 트랜잭션 롤백이 필요한 시점에 부분 복원 시퀀스가 중지되고 오프라인 상태인 데이터가 트랜잭션에 필요하면 지연된 트랜잭션이 발생할 수 있습니다.  
  
 롤백 중에 I/O 오류가 발생한 사용자 트랜잭션으로 인해 전체 데이터베이스가 오프라인 상태가 될 수 있습니다. 데이터베이스를 다시 온라인 상태로 만들면 다시 실행이 이전 잠금을 모두 다시 획득하며 커밋되지 않은 모든 트랜잭션을 롤백하려고 시도합니다. 트랜잭션에 의해 수정된 모든 데이터는 해당 트랜잭션이 롤백될 때까지 적절하게 잠긴 상태로 유지됩니다. 롤백할 수 없는 트랜잭션은 손상이 복구되고 데이터베이스가 다시 시작되거나, 온라인 복원 후에 데이터베이스가 온라인 상태일 동안 지연된 트랜잭션이 해결될 때 잠금을 해제합니다. 그 전까지는 지연된 트랜잭션이 데이터베이스에서의 특정 작업 전체를 수행하지 못하게 하는 잠금을 유지할 수 있습니다. 예를 들어 지연된 트랜잭션에 CREATE TABLE 명령이 있으면 지연된 트랜잭션이 해결될 때까지 어떤 사용자도 테이블을 만들 수 없습니다.  
  
 또한 증분 복원은 아직 복원되지 않고 현재 오프라인 상태인 파일 그룹에 영향을 주는 활성 트랜잭션이 하나 이상 있는 지점으로 데이터베이스를 복구하므로 지연된 트랜잭션이 발생할 수 있습니다. 트랜잭션을 롤백할 수 없으므로 해당 트랜잭션은 지연됩니다.  
  
 다음 표에서는 I/O 문제가 발생하는 경우 데이터베이스에서 복구를 수행하도록 하는 동작과 결과를 보여 줍니다.  
  
|작업|해결 방법(I/O 문제가 발생하거나 필요한 데이터가 오프라인 상태일 경우)|  
|------------|-----------------------------------------------------------------------|  
|서버 시작|지연된 트랜잭션|  
|복원|지연된 트랜잭션|  
|연결|연결 실패|  
|자동 재시작|지연된 트랜잭션|  
|데이터베이스 또는 데이터베이스 스냅샷 만들기|만들기 실패|  
|데이터베이스 미러링의 다시 실행|지연된 트랜잭션|  
|파일 그룹이 오프라인 상태|지연된 트랜잭션|  
  
### <a name="requirements-and-limitations"></a>요구 사항 및 제한 사항

 - 데이터베이스는 전체 또는 대량 로그된 복구 모델을 사용해야 합니다.
 - 데이터베이스를 대상으로 하나 이상의 데이터베이스 및 로그 백업이 완료되어 있어야 합니다.
 - 데이터베이스가 온라인 상태가 된 이후 트랜잭션을 롤백하는 동안 발생한 오류에는 지연된 트랜잭션이 적용되지 않습니다. (예: 런타임 오류)
 - 데이터베이스를 연결하는 중에 복구 실패로 인해 트랜잭션이 지연될 수 없습니다.
 - 시스템 트랜잭션(예: 페이지 할당)과 같은 일부 트랜잭션은 지연될 수 없습니다.

## <a name="moving-a-transaction-out-of-the-deferred-state"></a>지연된 상태 밖으로 트랜잭션 이동  
  
> [!IMPORTANT]  
>  지연된 트랜잭션은 트랜잭션 로그를 활성 상태로 유지합니다. 지연된 트랜잭션을 포함하는 가상 로그 파일은 이러한 트랜잭션이 지연된 상태에서 벗어날 때까지는 잘릴 수 없습니다. 로그 잘림에 대한 자세한 내용은 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)를 참조하세요.  
  
 트랜잭션을 지연된 상태에서 벗어나게 하려면 데이터베이스가 I/O 오류 없이 깨끗하게 시작해야 합니다. 지연된 트랜잭션이 있으면 I/O 오류의 출처를 수정해야 합니다. 사용 가능한 해결 방법은 다음과 같으며 일반적으로 시도되는 순서대로 나열되어 있습니다.  
  
-   데이터베이스를 다시 시작합니다. 문제가 일시적인 경우에는 지연된 트랜잭션 없이 데이터베이스를 시작해야 합니다.  
  
-   파일 그룹이 오프라인 상태이기 때문에 트랜잭션이 지연된 경우에는 해당 파일 그룹을 온라인 상태로 되돌립니다.  
  
     오프라인 상태의 파일 그룹을 다시 온라인 상태로 만들려면 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용합니다.  
  
    ```  
    RESTORE DATABASE database_name FILEGROUP=<filegroup_name>  
    ```  
  
-   데이터베이스를 복원합니다. 온라인 복원 후에 지연된 트랜잭션이 모두 해결됩니다.  
  
     전체 또는 대량 로그 복구 모델에서 몇 개의 손상된 페이지로 인해 지연된 트랜잭션이 발생한 경우 온라인 페이지 복원을 통해 오류를 해결할 수 있습니다(지원되는 경우).  
  
-   지연된 트랜잭션을 발생하는 오프라인 상태인 파일 그룹이 더 이상 필요하지 않을 경우 오프라인 파일 그룹이 존재하지 않도록 합니다. 파일 그룹이 오프라인 상태이므로 지연된 트랜잭션은 이 파일 그룹이 존재하지 않게 된 후에 지연된 상태에서 벗어납니다.  
  
    > [!IMPORTANT]  
    >  존재하지 않는 파일 그룹은 복구할 수 없습니다.  
  
     자세한 내용은 [존재하지 않는 파일 그룹 제거&#40;SQL Server&#41;](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)를 참조하세요.  
  
-   잘못된 페이지 때문에 트랜잭션이 지연된 경우 및 올바른 데이터베이스 백업이 없는 경우 다음 프로세스에 따라 데이터베이스를 복구합니다.  
  
    -   우선 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하여 데이터베이스를 응급 모드로 설정합니다.  
  
        ```  
        ALTER DATABASE <database_name> SET EMERGENCY  
        ```  
  
         응급 모드에 대한 자세한 내용은 [Database States](../../relational-databases/databases/database-states.md)를 참조하십시오.  
  
    -   그런 후에 DBCC 문인 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md), [DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md), [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md) 중 하나에 DBCC REPAIR_ALLOW_DATA_LOSS 옵션을 사용하여 데이터베이스를 복구합니다.  
  
         DBCC에서 잘못된 페이지가 발생하면 DBCC에서 할당을 취소하고 관련 오류를 모두 복구합니다. 이 방법을 사용하면 물리적으로 일관된 상태로 데이터베이스를 다시 온라인 상태로 만들 수 있습니다. 그러나 추가 데이터가 손실될 수도 있으므로 이 방법은 마지막으로 선택해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [복원 및 복구 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [존재하지 않는 파일 그룹 제거&#40;SQL Server&#41;](../../relational-databases/backup-restore/remove-defunct-filegroups-sql-server.md)   
 [파일 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [파일 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [페이지 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [ALTER DATABASE &#40;Transact-SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
