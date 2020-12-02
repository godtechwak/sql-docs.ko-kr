---
description: 작업 활동 모니터(필터 설정)
title: 작업 활동 모니터(필터 설정) | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.jobactivitymon.filter.f1
ms.assetid: 89cb0055-5262-447f-8464-7203d4caba78
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f7533366a28517fcc2fdb8ca5c2e4ad0c0dd01c5
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88424055"
---
# <a name="job-activity-monitor-filter-settings"></a>작업 활동 모니터(필터 설정)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 페이지를 사용하여 작업 활동 모니터에 표시되는 행 수를 줄일 수 있습니다. 하나 또는 여러 개의 사용 가능한 상자에 조건을 입력하여 지정한 값을 만족하는 행만 표시합니다. **상태** 또는 **차단 유형** 과 같은 일부 상자에서는 드롭다운 목록으로 한정된 수의 가능한 값을 제공합니다. **애플리케이션** 과 같은 기타 상자에서는 어떤 값이든 원하는 만큼 쉼표로 구분된 목록으로 입력할 수 있습니다. 도구 모음 아이콘을 사용하면 범주별 또는 사전순으로 사용 가능한 상자를 정렬할 수 있습니다. 각각에 대해 간단한 설명을 표시할 조건을 클릭합니다.  
  
 작업 활동 모니터를 필터링하려면 원하는 개수만큼 필터 조건을 제공하고 **필터 적용** 을 클릭한 다음 **확인** 을 클릭합니다.  
  
## <a name="all-jobs"></a>모든 작업  
 이 필터 조건 그룹은 작업 활동 모니터를 필터링할 때 사용할 수 있습니다.  
  
 **이름**  
 이름으로 작업을 필터링합니다.  
  
 **다음 실행**  
 다음에 실행하도록 예약된 날짜로 필터링합니다.  
  
 **실행 가능**  
 실행할 수 있는 작업을 표시하거나 실행할 수 없는 작업을 표시합니다. **예** 를 선택하여 실행할 수 있는 작업만 표시하거나 **아니요** 를 선택하여 실행할 수 없는 작업만 표시하거나 또는 **모두** 를 선택하여 실행할 수 있는 작업과 실행할 수 없는 작업을 모두 표시합니다.  
  
 **마지막 실행**  
 마지막으로 실행한 날짜로 필터링합니다.  
  
 **마지막 실행 결과**  
 마지막으로 작업을 실행했을 때의 상태로 작업을 필터링합니다.  
  
 **Enabled**  
 사용하는 작업만 표시하거나 사용하지 않는 작업만 표시합니다.  
  
 **범주**  
 작업 범주로 작업을 필터링합니다.  
  
 **예약**  
 일정이 있는 작업을 모두 표시하거나 일정이 없는 작업을 모두 표시합니다.  
  
 **상태**  
 상태로 작업을 필터링합니다.  
  
## <a name="description-area"></a>설명 영역  
 **설명 상자**  
 이름이 지정되지 않은 이 상자에서는 선택된 조건에 대한 간단한 설명을 제공합니다.  
  
 **필터 적용**  
 필터를 적용하려면 **Applyfilter** 를 클릭한 다음, **확인** 을 클릭합니다. **FilterSettings** 대화 상자의 필터 설정을 유지하되 적용하지 않으려면 **Applyfilter** 의 선택을 취소한 다음, **확인** 을 클릭하여 모든 행을 표시합니다.  
  
 **지우기**  
 필터 설정을 기본 설정으로 되돌립니다.  
  
## <a name="see-also"></a>참고 항목  
 [작업 활동 모니터링](../../ssms/agent/monitor-job-activity.md)  
  
  
