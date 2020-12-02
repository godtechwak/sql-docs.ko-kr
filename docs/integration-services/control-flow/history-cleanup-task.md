---
description: 기록 정리 태스크
title: 기록 정리 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.historycleanuptask.f1
helpviewer_keywords:
- history tables [SQL Server]
- History Cleanup task [Integration Services]
ms.assetid: 5defc5b9-dfd3-4859-a7fe-ac8c2b5480f8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2455138c200097adc1547d3d57fbe4014b2be022
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "92194261"
---
# <a name="history-cleanup-task"></a>기록 정리 태스크

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  기록 정리 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] msdb 데이터베이스의 다음 기록 테이블에서 항목을 삭제합니다.  
  
-   backupfile  
  
-   backupfilegroup  
  
-   backupmediafamily  
  
-   backupmediaset  
  
-   backupset  
  
-   restorefile  
  
-   restorefilegroup  
  
-   restorehistory  
  
 기록 정리 태스크를 사용하면 패키지가 백업 및 복원 작업, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 및 데이터베이스 유지 관리 계획과 관련된 기록 데이터를 삭제할 수 있습니다.  
  
 이 태스크는 sp_delete_backuphistory 시스템 저장 프로시저를 캡슐화하고 지정한 날짜를 프로시저에 인수로 전달합니다. 자세한 내용은 [sp_delete_backuphistory&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)를 참조하세요.  
  
## <a name="configuration-of-the-history-cleanup-task"></a>기록 정리 태스크 구성  
 이 태스크에는 기록 테이블에 보관되는 데이터의 가장 오래된 날짜를 지정하는 속성이 있습니다. 현재 날짜로부터의 일, 주, 월 또는 연 수로 날짜를 지정하면 태스크에서 자동으로 이 간격이 특정 날짜로 변환됩니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 속성을 설정할 수 있습니다. 이 태스크는 **디자이너의** 도구 상자 **에 있는** 유지 관리 계획 태스크 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 섹션에서 수행할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [기록 정리 태스크&#40;유지 관리 계획&#41;](../../relational-databases/maintenance-plans/history-cleanup-task-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](./add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)  
  
