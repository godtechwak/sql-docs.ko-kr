---
title: '온라인 복원: 읽기 전용 파일(단순 복구 모델)'
description: 이 예제에서는 SQL Server에서 단순 복구 모델로 여러 파일 그룹을 사용하여 데이터베이스의 읽기 전용 파일을 온라인 복원하는 방법을 보여 줍니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restore sequences [SQL Server], online
- online restores [SQL Server], simple recovery model
- simple recovery model [SQL Server], RESTORE examples
ms.assetid: 0c691fc6-9865-46a7-b055-8097424492d6
author: cawrites
ms.author: chadam
ms.openlocfilehash: 58c4448ecde5bfed478ad19aa961dc74c1db59a5
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130434"
---
# <a name="example-online-restore-of-a-read-only-file-simple-recovery-model"></a>예제: 읽기 전용 파일의 온라인 복원(단순 복구 모델)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 항목에서는 읽기 전용 파일 그룹이 있는 단순 복구 모델에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 관련된 내용을 다룹니다. 단순 복구 모델의 경우 파일이 마지막으로 읽기 전용이 된 후에 수행된 파일 백업이 존재하는 경우 읽기 전용 파일을 온라인으로 복원할 수 있습니다.  
  
 이 예에서 `adb` 라는 데이터베이스에 3개의 파일 그룹이 있습니다. 파일 그룹 `A` 는 읽기/쓰기가 가능하며 파일 그룹 `B` 와 `C` 는 읽기 전용입니다. 처음에는 모든 파일 그룹이 온라인입니다. 파일 그룹 `B`의 읽기 전용 파일인 `b1`을 복원해야 합니다. 데이터베이스 관리자는 파일이 읽기 전용이 된 후에 수행된 백업을 사용하여 파일을 복원할 수 있습니다. 복원하는 동안 파일 그룹 `B` 는 오프라인 상태이지만 데이터베이스의 나머지 파일 그룹은 온라인 상태로 남아 있습니다.  
  
## <a name="restore-sequence"></a>복원 시퀀스  
  
> [!NOTE]  
>  온라인 복원 시퀀스의 구문은 오프라인 복원 시퀀스의 구문과 동일합니다.  
  
 데이터베이스 관리자는 다음 복원 시퀀스에 따라 파일을 복원할 수 있습니다.  
  
```  
RESTORE DATABASE adb FILE='b1' FROM filegroup_B_backup   
WITH RECOVERY  
```  
  
 이제 파일이 온라인입니다.  
  
## <a name="additional-examples"></a>추가 예  
  
-   [예: 데이터베이스의 증분 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [예: 일부 파일 그룹만 증분 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
-   [예: 데이터베이스의 증분 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [예: 일부 파일 그룹만 증분 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   [예: 읽기-쓰기 파일의 온라인 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-write-file-full-recovery-model.md)  
  
-   [예: 읽기 전용 파일의 온라인 복원&#40;전체 복구 모델&#41;](../../relational-databases/backup-restore/example-online-restore-of-a-read-only-file-full-recovery-model.md)  
  
## <a name="see-also"></a>참고 항목  
 [온라인 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [파일 복원&#40;단순 복구 모델&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [복원 및 복구 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
