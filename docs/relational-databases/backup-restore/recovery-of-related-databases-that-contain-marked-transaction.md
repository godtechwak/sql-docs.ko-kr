---
title: 표시된 트랜잭션을 사용하여 관련 데이터베이스 복구
description: SQL Server는 특정 표시로 복구할 수 있도록 트랜잭션 로그에서 명명된 표시를 지원합니다. 표시는 특정 작업에 연결될 수 있습니다.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], marks
- STOPBEFOREMARK option [RESTORE statement]
- STOPATMARK option [RESTORE statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
- recovery [SQL Server], databases
- restoring [SQL Server], point in time
- transactions [SQL Server], recovering to a mark
- database recovery [SQL Server]
- marked transactions [SQL Server], restoring
- database restores [SQL Server], point in time
ms.assetid: 77a0d9c0-978a-4891-8b0d-a4256c81c3f8
author: cawrites
ms.author: chadam
ms.openlocfilehash: e43b37dd96a931d98555f05fe6e70b9f8a4f99e3
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129169"
---
# <a name="recovery-of-related--databases-that-contain-marked-transaction"></a>표시된 트랜잭션이 포함된 관련 데이터베이스 복구
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 표시된 트랜잭션을 포함하며 전체 복구 모델 또는 대량 로그 복구 모델을 사용하는 데이터베이스와 관련된 내용을 다룹니다.  
  
 특정 복구 지점으로 복원하기 위한 요구 사항에 대한 자세한 내용은 [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 트랜잭션 로그에 명명된 표시를 삽입할 수 있으므로 특정 표시로의 복구가 가능합니다. 로그 표시는 트랜잭션과 관련되어 있으므로 관련된 트랜잭션이 커밋될 경우에만 삽입됩니다. 그러므로 표시는 특정한 작업에 연결될 수 있고 이 작업을 포함 또는 제외하는 지점으로 복구할 수 있습니다.  
  
 트랜잭션 로그에 명명된 표시를 삽입하기 전에 다음 사항을 주의하십시오.  
  
-   트랜잭션 표시는 로그 공간을 소비하므로 데이터베이스 복구 전략에서 중요한 역할을 하는 트랜잭션에 대해서만 사용해야 합니다.  
  
-   표시된 트랜잭션을 커밋한 후에 [msdb](../../relational-databases/system-tables/logmarkhistory-transact-sql.md) 의 **logmarkhistory** 테이블에 행이 삽입됩니다.  
  
-   표시된 트랜잭션이 같은 데이터베이스 서버 또는 다른 서버의 다중 데이터베이스에 걸쳐 있으면 영향 받은 모든 데이터베이스의 로그에 표시가 기록됩니다. 자세한 내용은 [표시된 트랜잭션을 사용하여 관련 데이터베이스를 일관되게 복구&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)을 참조하세요.  
  
> [!NOTE]  
>  트랜잭션을 표시하는 방법은 [표시된 트랜잭션을 사용하여 관련 데이터베이스를 일관되게 복구&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)을 참조하세요.  
  
## <a name="transact-sql-syntax-for-inserting-named-marks-into-a-transaction-log"></a>명명된 표시를 트랜잭션 로그에 삽입하는 Transact-SQL 구문  
 [BEGIN TRANSACTION](../../t-sql/language-elements/begin-transaction-transact-sql.md) 문과 WITH MARK [*description*] 절을 사용하여 표시를 트랜잭션 로그에 삽입합니다. 표시 이름은 트랜잭션 이름과 같습니다. 선택 요소인 *description* 은 표시의 이름이 아니라 표시의 텍스트 설명입니다. 예를 들어 다음 `BEGIN TRANSACTION` 문에서 생성된 표시 및 트랜잭션의 이름은 `Tx1`입니다.  
  
```sql  
BEGIN TRANSACTION Tx1 WITH MARK 'not the mark name, just a description'    
```  
  
 트랜잭션 로그는 표시 이름(트랜잭션 이름), 설명, 데이터베이스, 사용자, **datetime** 정보, LSN(로그 시퀀스 번호) 등을 기록합니다. **datetime** 정보는 표시를 고유하게 식별하는 표시 이름과 함께 사용됩니다.  
  
 여러 데이터베이스에 걸쳐 있는 트랜잭션에 표시를 삽입하는 방법은 [표시된 트랜잭션을 사용하여 관련 데이터베이스를 일관되게 복구&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)을 참조하세요.  
  
## <a name="transact-sql-syntax-for-recovering-to-a-mark"></a>표시 지점으로 복구하는 Transact-SQL 구문  
 [RESTORE LOG](../../t-sql/statements/restore-statements-transact-sql.md)문을 사용하여 표시된 트랜잭션을 대상으로 지정할 때 중지된 곳이나 표시 바로 앞에 다음 절 중 하나를 사용할 수 있습니다.  
  
-   표시된 트랜잭션이 복구 지점이라는 것을 지정하는 WITH STOPATMARK = **'** _<mark_name>_ **'** 절을 사용합니다.  
  
     STOPATMARK는 표시로 롤포워드하고 표시된 트랜잭션을 롤포워드에 포함시킵니다.  
  
-   표시 바로 앞에 있는 로그 레코드가 복구 지점이라는 것을 지정하는 WITH STOPBEFOREMARK = **'** _<mark_name>_ **'** 절을 사용합니다.  
  
     STOPBEFOREMARK는 표시로 롤포워드하고 롤포워드에서 표시된 트랜잭션을 제외시킵니다.  
  
 STOPATMARK 옵션과 STOPBEFOREMARK 옵션은 선택적으로 사용되는 AFTER *datetime* 절을 지원합니다. *datetime* 을 사용할 경우 표시 이름은 고유하지 않아도 됩니다.  
  
 AFTER *datetime* 이 생략되면 지정한 이름이 있는 첫 번째 표시 지점에서 복구가 중지됩니다. AFTER *datetime* 이 지정되면 *datetime* 에서 또는 이후에 지정한 이름이 있는 첫 번째 표시 지점에서 복구가 중지됩니다.  
  
> [!NOTE]  
>  모든 지정 시간 복원 작업에서처럼 데이터베이스에서 대량 로그 작업이 진행되는 동안 표시 지점으로 복구되지 않습니다.  
  
 **표시된 트랜잭션 지점으로 복원하려면**  
  
 [데이터베이스를 표시된 트랜잭션으로 복원&#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
### <a name="preparing-the-log-backups"></a>로그 백업 준비  
 이 예에서 이러한 관련된 데이터베이스에 대한 적절한 백업 전략은 다음과 같습니다.  
  
1.  두 데이터베이스 모두에 전체 복구 모델을 사용합니다.  
  
2.  각 데이터베이스의 전체 백업을 만듭니다.  
  
     데이터베이스를 연속적으로 또는 동시에 백업할 수 있습니다.  
  
3.  트랜잭션 로그를 백업하기 전에 모든 데이터베이스에서 실행되는 트랜잭션을 표시합니다. 표시된 트랜잭션을 만드는 방법은 [표시된 트랜잭션을 사용하여 관련 데이터베이스를 일관되게 복구&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)을 참조하세요.  
  
4.  각 데이터베이스에서 트랜잭션 로그를 백업합니다.  
  
### <a name="recovering-the-database-to-a-marked-transaction"></a>데이터베이스를 표시된 트랜잭션으로 복구  
 **백업을 복원하려면**  
  
1.  필요하면 손상되지 않은 데이터베이스의 [비상 로그 백업](../../relational-databases/backup-restore/tail-log-backups-sql-server.md) 을 만듭니다.  
  
2.  각 데이터베이스의 최신 전체 데이터베이스 백업을 복원합니다.  
  
3.  모든 트랜잭션 로그 백업에서 가장 최근에 표시된 사용 가능한 트랜잭션을 확인합니다. 이 내용은 각 서버의 **msdb** 데이터베이스에 있는 **logmarkhistory** 테이블에 저장되어 있습니다.  
  
4.  이 표시가 들어 있는 관련된 모든 데이터베이스에 대한 로그 백업을 식별합니다.  
  
5.  표시된 트랜잭션에서 중지된 각 로그 백업을 복원합니다.  
  
6.  각 데이터베이스를 복구합니다.  
  
## <a name="see-also"></a>참고 항목  
 [BEGIN TRANSACTION&#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)   
 [표시된 트랜잭션을 사용하여 관련 데이터베이스를 일관되게 복구&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [복원 및 복구 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [복원 시퀀스 계획 및 수행&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/plan-and-perform-restore-sequences-full-recovery-model.md)  
  
  
