---
title: 로그 전달 보조로 장애 조치(failover)
description: SQL Server Management Studio 또는 Transact-SQL을 사용하여 SQL Server 로그 전달 보조 데이터베이스로 장애 조치(failover)하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- primary databases [SQL Server]
- secondary data files [SQL Server], manual fail over
- log shipping [SQL Server], failover
- failover [SQL Server], log shipping
ms.assetid: edfe5d59-4287-49c1-96c9-dd56212027bc
author: cawrites
ms.author: chadam
ms.openlocfilehash: d4e6ec31a1f1082ae13142fe521858122f079939
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130751"
---
# <a name="fail-over-to-a-log-shipping-secondary-sql-server"></a>로그 전달 보조 데이터베이스로 장애 조치(Failover)(SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  로그 전달 보조 데이터베이스로 장애 조치(Failover)는 주 서버 인스턴스에서 오류가 발생하거나 유지 관리가 필요한 경우에 유용합니다.  
  
## <a name="preparing-for-a-controlled-failover"></a>제어된 장애 조치(Failover) 준비  
 일반적으로 주 데이터베이스는 가장 최근의 백업 작업 이후 계속 업데이트되므로 주 데이터베이스와 보조 데이터베이스는 동기화되지 않습니다. 경우에 따라 최근 트랜잭션 로그 백업이 보조 서버 인스턴스로 복사되지 않았거나 복사된 일부 로그 백업이 보조 데이터베이스에 아직 적용되지 않았을 수도 있습니다. 가능한 경우 먼저 모든 보조 데이터베이스를 주 데이터베이스와 동기화하는 것이 좋습니다.  
  
 로그 전달 작업에 대한 자세한 내용은 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)를 참조하세요.  
  
## <a name="failing-over"></a>장애 조치(Failover)  
 보조 데이터베이스로 장애 조치(Failover)하려면  
  
1.  백업 공유에서 복사되지 않은 백업 파일을 각 보조 서버의 복사 대상 폴더로 모두 복사합니다.  
  
2.  적용되지 않은 트랜잭션 로그 백업을 각 보조 데이터베이스에 순서대로 적용합니다. 자세한 내용은 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)을 참조하세요.  
  
3.  주 데이터베이스에 액세스할 수 있는 경우, 활성 트랜잭션 로그를 백업한 후 이 로그 백업을 보조 데이터베이스에 적용합니다. 복원 명령을 실행하기 전에 데이터베이스를 [단일 사용자 모드](../../relational-databases/databases/set-a-database-to-single-user-mode.md)로 설정하여 단독 액세스 권한을 얻은 다음, 복원이 완료된 후 다중 사용자로 다시 전환해야 할 수도 있습니다.  
  
     원래 주 서버 인스턴스가 손상되지 않은 경우 WITH NORECOVERY를 사용하여 주 데이터베이스의 트랜잭션 비상 로그를 백업합니다. 이렇게 하면 데이터베이스가 복원 상태로 남아 있으므로 사용자가 사용할 수 없습니다. 그러므로 대체 주 데이터베이스에서 트랜잭션 로그 백업을 적용하여 이 데이터베이스를 롤포워드할 수 있습니다.  
  
     자세한 내용은 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)을 참조하세요.   
  
4.  보조 서버가 동기화된 후 해당 보조 데이터베이스를 복구하고 해당 서버 인스턴스로 리디렉션하여 원하는 데이터베이스로 장애 조치(Failover)할 수 있습니다. 복구하면 데이터베이스가 일관성 있는 온라인 상태가 됩니다.  
  
    > [!NOTE]  
    >  보조 데이터베이스를 사용하는 경우 메타데이터가 원래 주 데이터베이스의 메타데이터와 일치하는지 확인해야 합니다. 자세한 내용은 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)을 참조하세요.  
  
5.  보조 데이터베이스를 복구한 후에는 다른 보조 데이터베이스에 대해 주 데이터베이스의 역할을 하도록 다시 구성할 수 있습니다.  
  
     다른 보조 데이터베이스를 사용하는 경우 [로그 전달 구성&#40;SQL Server&#41;](../../database-engine/log-shipping/configure-log-shipping-sql-server.md)을 참조하세요.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [주 로그 전달 서버와 보조 로그 전달 서버 간 역할 변경&#40;SQL Server&#41;](../../database-engine/log-shipping/change-roles-between-primary-and-secondary-log-shipping-servers-sql-server.md)  
  
-   [역할 전환 후 로그인 및 작업 관리&#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [로그 전달 테이블 및 저장 프로시저](../../database-engine/log-shipping/log-shipping-tables-and-stored-procedures.md)   
 [로그 전달 정보&#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [비상 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)  
  
  
