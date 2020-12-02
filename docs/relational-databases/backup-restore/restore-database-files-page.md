---
title: 데이터베이스 복원(파일 페이지) | Microsoft 문서
description: SQL Server에서 데이터베이스를 복원할 때 데이터베이스 복원 대화 상자의 파일 페이지를 사용하여 데이터베이스 내에서 복원할 특정 파일을 관리합니다.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restoredb.files.f1
- sql13.swb.restoredb.files.f1 in the code
ms.assetid: 714c36ea-a9f9-43a4-99f9-a6f73d1baf8e
author: cawrites
ms.author: chadam
ms.openlocfilehash: d94a143eae321f7ea01f97a54b351d72f8142ad6
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129157"
---
# <a name="restore-database-files-page"></a>데이터베이스 복원(파일 페이지)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **데이터베이스 복원** 대화 상자의 **파일** 페이지를 사용하여 데이터베이스 내에서 복원하려고 선택한 특정 파일을 관리할 수 있습니다.  
  
## <a name="options"></a>옵션  
  
### <a name="restore-database-files-as"></a>데이터베이스 파일을 다음으로 복원  
 복원된 파일의 파일 경로를 새로 할당하고 관리하려면 사용합니다.  
  
 **모든 폴더를 파일에 다시 배치**  
 복원된 파일의 위치를 다시 지정합니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**데이터 파일 폴더**|복원된 데이터 파일을 다시 배치할 데이터 파일 폴더 이름을 입력하거나 검색합니다.|  
|**로그 파일 폴더**|복원된 로그 파일을 다시 배치할 로그 파일 또는 파일 폴더를 입력하거나 검색합니다.|  
  
 **논리적 파일 이름**  
 복원할 각 데이터베이스 파일당 한 개의 행을 표시합니다.  
  
 **파일 유형**  
 파일 형식을 표시합니다.  
  
 **원래 파일 이름**  
 복원된 파일의 원래 파일 경로를 표시합니다.  
  
 **다음으로 복원**  
 복원된 파일을 저장할 파일 이름을 나열합니다. 적절한 파일 이름을 입력하거나 검색합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 복원&#40;일반 페이지&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)   
 [데이터베이스 복원&#40;옵션 페이지&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)   
 [RESTORE 인수&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [테이프 드라이브에 대한 논리적 백업 디바이스 정의&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
