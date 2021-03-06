---
title: 데이터베이스 백업 및 복원
description: 이 자습서에 따라 Azure Data Studio를 사용하여 데이터베이스를 백업 및 복원하는 방법을 알아봅니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: tutorial
author: markingmyname
ms.author: maghan
ms.reviewer: alayu
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: 808dec10c92bffe66122bfa9a55d7db1cc64f62e
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364173"
---
# <a name="tutorial-back-up-and-restore-databases-using-azure-data-studio"></a>자습서: Azure Data Studio를 사용하여 데이터베이스 백업 및 복원

이 자습서에서는 Azure Data Studio를 사용하여 다음을 수행하는 방법을 알아봅니다.
> [!div class="checklist"]
> * 데이터베이스를 백업합니다.
> * 백업 상태를 확인합니다.
> * 백업을 수행하는 데 사용되는 스크립트를 생성합니다.
> * 데이터베이스를 복원합니다.
> * 복원 작업의 상태를 확인합니다.

## <a name="prerequisites"></a>필수 구성 요소

이 자습서에는 SQL Server *TutorialDB*가 필요합니다. TutorialDB 데이터베이스를 만들려면 다음 빠른 시작을 완료합니다.

* [Azure Data Studio를 사용하여 SQL Server 연결 및 쿼리](quickstart-sql-server.md)

이 자습서를 사용하려면 SQL Server 데이터베이스에 연결해야 합니다. Azure SQL Database에는 자동화된 백업이 있으므로 Azure Data Studio는 Azure SQL Database 백업 및 복원을 수행하지 않습니다. 자세한 내용은 [자동 SQL 데이터베이스 백업에 대해 알아보기](/azure/sql-database/sql-database-automated-backups)를 참조하세요.

## <a name="back-up-a-database"></a>데이터베이스 백업

1. **서버** 사이드바를 열어 TutorialDB 데이터베이스 대시보드를 엽니다. 그런 다음, **Ctrl+G**를 선택하고, **데이터베이스**를 확장하고, **TutorialDB**를 마우스 오른쪽 단추로 클릭하고, **관리**를 선택합니다.

1. **작업** 위젯에서 **백업**을 선택하여 **데이터베이스 백업** 대화 상자를 엽니다.

   ![작업 위젯을 보여주는 스크린샷.](./media/tutorial-backup-restore-sql-server/tasks.png)

1. 이 자습서에서는 기본 백업 옵션을 사용하므로 **백업**을 선택합니다.

   ![백업 대화 상자를 보여주는 스크린샷.](./media/tutorial-backup-restore-sql-server/backup-dialog.png)

**백업**을 선택하면 **데이터베이스 백업** 대화 상자가 사라지고 백업 프로세스가 시작됩니다.

## <a name="view-the-backup-status-and-the-backup-script"></a>백업 상태 및 백업 스크립트 보기

1. **작업 기록** 창이 나타나거나 **Ctrl+T**를 선택하여 엽니다.

   ![작업 기록 창을 보여주는 스크린샷.](./media/tutorial-backup-restore-sql-server/task-history.png)

1. 편집기에서 백업 스크립트를 보려면 **데이터베이스 백업 성공**을 마우스 오른쪽 단추로 클릭하고 **스크립트**를 선택합니다.

   ![백업 스크립트를 보여주는 스크린샷.](./media/tutorial-backup-restore-sql-server/task-script.png)

## <a name="restore-a-database-from-a-backup-file"></a>백업 파일에서 데이터베이스 복원

1. **Ctrl+G**를 선택하여 **서버** 사이드바를 엽니다. 그런 다음, 서버를 마우스 오른쪽 단추로 클릭하고 **관리**를 선택합니다.

1. **작업** 위젯에서 **복원**을 선택하여 **데이터베이스 복원** 대화 상자를 엽니다.

   ![작업 복원을 보여주는 스크린샷.](media/tutorial-backup-restore-sql-server/tasks-restore.png)

1. **복원 원본** 상자에서 **백업 파일**을 선택합니다.

1. **백업 파일 경로** 상자에서 줄임표(...)를 선택하고 *TutorialDB*에 대한 최신 백업 파일을 선택합니다.

1. **대상** 섹션의 **대상 데이터베이스** 상자에 **TutorialDB_Restored**를 입력하여 백업 파일을 새 데이터베이스로 복원합니다. 그런 다음, **복원**을 선택합니다.

   ![백업 복원을 보여주는 스크린샷.](./media/tutorial-backup-restore-sql-server/restore.png)

1. 복원 작업의 상태를 보려면 **Ctrl+T**를 선택하여 **작업 기록**을 엽니다.

   ![기록 작업 복원을 보여주는 스크린샷.](./media/tutorial-backup-restore-sql-server/task-history-restore.png)