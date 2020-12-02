---
title: 데이터베이스를 표시된 트랜잭션으로 복원(SSMS)
description: SQL Server 데이터베이스가 복원 상태인 경우, 트랜잭션 로그 복원 대화 상자를 사용하여 데이터베이스를 사용 가능한 로그 백업의 표시된 트랜잭션으로 복원합니다.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restoretlog.markedtransaction.f1
helpviewer_keywords:
- database restores [SQL Server], marked transactions
- restoring databases [SQL Server], marked transactions
- marked transactions [SQL Server], restoring
ms.assetid: 8f0ea144-1819-4832-905f-e5d0f49b066b
author: cawrites
ms.author: chadam
ms.openlocfilehash: d35f1478d3d9f290557a6eeebd6ce4365e461e21
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129118"
---
# <a name="restore-a-database-to-a-marked-transaction-sql-server-management-studio"></a>데이터베이스를 표시된 트랜잭션으로 복원(SQL Server Management Studio)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  데이터베이스가 복원 상태인 경우 **트랜잭션 로그 복원** 대화 상자를 사용하여 사용 가능한 로그 백업에서 데이터베이스를 표시된 트랜잭션으로 복원할 수 있습니다.  
  
> [!NOTE]  
>  자세한 내용은 [표시된 트랜잭션을 사용하여 관련 데이터베이스를 일관되게 복구&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md) 및 [표시된 트랜잭션을 포함하는 관련 데이터베이스 복구](../../relational-databases/backup-restore/recovery-of-related-databases-that-contain-marked-transaction.md)를 참조하세요.  
  
### <a name="to-restore-a-marked-transaction"></a>표시된 트랜잭션을 복원하려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 후 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스** 를 확장하고 해당 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크** 를 가리킨 다음 **복원** 을 클릭합니다.  
  
4.  **트랜잭션 로그** 를 클릭하여 **트랜잭션 로그 복원** 대화 상자를 엽니다.  
  
5.  **일반** 페이지의 **복원 위치** 섹션에서 **표시된 트랜잭션** 을 선택하여 **표시된 트랜잭션 선택** 대화 상자를 엽니다. 이 대화 상자는 선택된 트랜잭션 로그 백업에서 사용할 수 있는 표시된 트랜잭션을 표로 나열합니다.  
  
     기본적으로 표시된 트랜잭션 이전까지만 복원합니다. 표시된 트랜잭션도 복원하려면 **표시된 트랜잭션 포함** 을 선택합니다.  
  
     다음 표에서는 표의 열 머리글을 나열하고 해당 값을 설명합니다.  
  
    |헤더|값|  
    |------------|-----------|  
    |\<blank>|표시 선택을 위한 확인란을 표시합니다.|  
    |**트랜잭션 표시**|트랜잭션이 커밋될 때 사용자가 지정한 표시된 트랜잭션의 이름입니다.|  
    |**Date**|트랜잭션이 커밋된 날짜 및 시간입니다. 트랜잭션 날짜 및 시간은 클라이언트 컴퓨터의 날짜 및 시간이 아닌 **msdbgmarkhistory** 테이블에 기록된 날짜 및 시간으로 표시됩니다.|  
    |**설명**|트랜잭션이 커밋될 때 사용자가 지정한 표시된 트랜잭션에 대한 설명입니다(있는 경우).|  
    |**LSN**|표시된 트랜잭션의 로그 시퀀스 번호입니다.|  
    |**Database**|표시된 트랜잭션이 커밋된 데이터베이스의 이름입니다.|  
    |**사용자 이름**|표시된 트랜잭션을 커밋한 데이터베이스 사용자의 이름입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
  
