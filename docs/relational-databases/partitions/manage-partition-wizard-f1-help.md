---
description: 파티션 관리 마법사
title: 파티션 관리 마법사
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
f1_keywords:
- sql13.swb.managepartition.createjob.f1
- sql13.swb.managepartition.progress.f1
- sql13.swb.managepartition.getstart.f1
- sql13.swb.managepartition.selectswitchtables.f1
- sql13.swb.managepartition.stagingtable.f1
- sql13.swb.managepartition.switchin.f1
- sql13.swb.managepartition.switchout.f1
- sql13.swb.managepartition.partitionaction.f1
- sql13.swb.managepartition.summary.f1
- sql13.swb.managepartition.selectoutput.f1
helpviewer_keywords:
- wizards [SQL Server Management Studio] See Manage Partition Wizard
ms.assetid: e2478d26-dea4-428d-98c5-aad2d2a30da8
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 756dd29442fe224f5e0518066cbbfdcbf2ba5ea6
ms.sourcegitcommit: b3a711a673baebb2ff10d7142b209982b46973ae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93364679"
---
# <a name="manage-partition-wizard"></a>파티션 관리 마법사 
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **파티션 관리 마법사** 를 사용하여 파티션 전환이나 슬라이딩 윈도우(Sliding Window) 시나리오의 구현을 통해 기존 파티션 테이블을 관리하고 수정할 수 있습니다. 이 마법사는 파티션 관리를 용이하게 하고 테이블로 또는 테이블로부터의 정기적인 데이터 마이그레이션을 단순화합니다.  
  
### <a name="to-start-the-manage-partition-wizard"></a>파티션 관리 마법사를 시작하려면  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 데이터베이스를 선택하고 파티션을 만들려는 테이블을 마우스 오른쪽 단추로 클릭하고 **스토리지** 를 가리킨 후 **파티션 관리** 를 클릭합니다.  
  
     **Note** **파티션 관리** 를 사용할 수 없으면 선택한 테이블에 파티션이 포함되어 있지 않은 것입니다. 테이블에 파티션을 만들려면 **스토리지** 하위 메뉴에서 **파티션 만들기** 를 클릭하고 **파티션 작성 마법사** 를 사용합니다.  
  
 파티션과 인덱스에 대한 자세한 내용은 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)를 참조하십시오.  
  
 이 섹션에서는 **파티션 관리 마법사** 를 사용하여 파티션을 관리, 수정 및 구현하는 데 필요한 정보를 제공합니다.  
  
##  <a name="in-this-section"></a><a name="Top"></a> 섹션 내용  
 다음 섹션에서는 **파티션 관리 마법사** 페이지에 대한 도움말을 제공합니다.  
  
 [파티션 관리 마법사(파티션 동작 선택 페이지)](#SelectPartitionAction)  
  
 [파티션 관리 마법사(내부 전환 페이지)](#SwitchIn)  
  
 [파티션 관리 마법사(외부 전환 페이지)](#SwitchOut)  
  
 [파티션 관리 마법사(준비 테이블 옵션 선택 페이지)](#StagingTableOptions)  
  
 [파티션 관리 마법사(출력 옵션 선택 페이지)](#OutputOption)  
  
 [파티션 관리 마법사(새 작업 일정 페이지)](#NewJob)  
  
 [파티션 관리 마법사(요약 페이지)](#Summary)  
  
 [파티션 관리 마법사(진행률 페이지)](#Progress)  
  
##  <a name="select-partition-action-page"></a><a name="SelectPartitionAction"></a> 파티션 작업 페이지 선택  
 **파티션 동작 선택** 페이지를 사용하여 파티션에서 수행할 동작을 선택할 수 있습니다.  
  
### <a name="create-a-staging-table"></a>준비 테이블 만들기  
 파티션 전환은 정기적으로 데이터 마이그레이션을 수행하는 분할된 테이블에서 일반적으로 수행되는 분할 태스크입니다. 예를 들어 현재 분기 데이터를 저장하는 분할된 테이블이 있을 경우 새 데이터를 이 테이블로 이동하고 오래된 데이터를 각 분기 끝에 보관해야 합니다.  
  
 이 마법사는 동일한 분할 열, 테이블/열 구조 및 인덱스를 사용하여 준비 테이블을 디자인하고 원본 파티션이 있는 파일 그룹에 새 테이블을 저장합니다.  
  
 준비 테이블을 사용하여 파티션 데이터를 전환하려면 **파티션 전환용 준비 테이블 만들기** 를 선택합니다.  
  
### <a name="sliding-window-scenario"></a>슬라이딩 윈도우(Sliding Window) 시나리오  
 슬라이딩 윈도우(Sliding Window) 시나리오에서 파티션을 관리하려면 **슬라이딩 윈도우 시나리오에서 분할된 데이터 관리** 를 선택합니다.  
  
### <a name="ui-element-list"></a>UI 요소 목록  
 **파티션 전환용 준비 테이블 만들기**  
 분할된 기존 테이블로 또는 분할된 기존 테이블에서 내부 전환하거나 외부 전환할 데이터의 준비 테이블을 만듭니다.  
  
 **외부 전환 파티션**  
 테이블에서 파티션을 제거할 때의 옵션을 제공합니다.  
  
 **내부 전환 파티션**  
 테이블에 파티션을 추가할 때의 옵션을 제공합니다.  
  
 **슬라이딩 윈도우 시나리오에서 분할된 데이터 관리**  
 데이터 전환에 사용할 수 있는 기존 테이블에 빈 파티션을 추가합니다. 이 마법사는 현재 마지막 파티션으로의 전환과 첫 번째 파티션으로부터의 전환을 지원합니다.  
  
 ![맨 위로 이동 링크와 함께 사용되는 화살표 아이콘](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [섹션 내용](#Top)  
  
##  <a name="select-partition-switching-in-options-page"></a><a name="SwitchIn"></a> 파티션 내부 전환 옵션 선택 페이지  
 **파티션 내부 전환 옵션 선택** 페이지를 사용하여 분할된 테이블로 내부 전환할 준비 테이블을 선택할 수 있습니다.  
  
### <a name="ui-element-list"></a>UI 요소 목록  
 **모든 파티션 표시**  
 분할된 테이블의 현재 파티션을 포함한 모든 파티션을 표시하려면 선택합니다.  
  
 **파티션 표**  
 선택한 파티션의 파티션 이름, **왼쪽 경계** , **오른쪽 경계** , **파일 그룹** 및 **행 개수** 를 표시합니다.  
  
 **내부 전환 테이블**  
 분할된 테이블에 추가할 파티션이 포함된 준비 테이블을 선택합니다. **파티션 관리 마법사** 를 사용하여 파티션을 내부 전환하기 전에 이 준비 테이블을 만들어야 합니다.  
  
 ![맨 위로 이동 링크와 함께 사용되는 화살표 아이콘](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [섹션 내용](#Top)  
  
##  <a name="select-partition-switching-out-options-page"></a><a name="SwitchOut"></a> 파티션 외부 전환 옵션 선택 페이지  
 **파티션 외부 전환 옵션 선택** 페이지를 사용하여 분할된 테이블에서 외부 전환할 분할된 데이터를 저장하기 위한 파티션 및 준비 테이블을 선택할 수 있습니다.  
  
### <a name="ui-element-list"></a>UI 요소 목록  
 **파티션 표**  
 선택한 파티션의 파티션 이름, **왼쪽 경계** , **오른쪽 경계** , **파일 그룹** 및 **행 개수** 를 표시합니다.  
  
 **외부 전환 테이블**  
 데이터를 외부 전환할 대상으로 새 테이블이나 기존 테이블을 선택합니다.  
  
 **새로 만들기**  
 현재 원본 테이블에서 외부 전환할 파티션에 사용할 준비 테이블의 새 이름을 입력합니다.  
  
 **기존**  
 현재 원본 테이블에서 외부 전환하려는 파티션에 사용할 기존 준비 테이블을 선택합니다. 기존 테이블에 데이터가 포함된 경우 외부 전환하는 데이터가 이 데이터를 덮어씁니다.  
  
 ![맨 위로 이동 링크와 함께 사용되는 화살표 아이콘](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [섹션 내용](#Top)  
  
##  <a name="select-the-staging-table-options-page"></a><a name="StagingTableOptions"></a> 준비 테이블 옵션 선택 페이지  
 **준비 테이블 옵션 선택** 페이지를 사용하여 분할된 데이터를 전환하는 데 사용할 준비 테이블을 만들 수 있습니다.  
  
 준비 테이블은 선택한 파티션에서 원본 테이블이 위치하는 파일 그룹과 같은 파일 그룹에 있어야 합니다. 준비 테이블은 원본 테이블과 대상 테이블의 디자인을 모두 반영해야 합니다.  
  
 원본 파티션에 존재하는 준비 테이블에 동일한 인덱스를 만들 수도 있습니다. 준비 테이블에는 원본 파티션의 요소를 기반으로 하는 제약 조건이 자동으로 포함됩니다. 이 제약 조건은 일반적으로 원본 파티션의 경계 값에서 생성됩니다.  
  
### <a name="ui-element-list"></a>UI 요소 목록  
 **준비 테이블 이름**  
 준비 테이블에 대한 이름을 만들거나 입력란에 표시되는 기본 이름을 사용합니다.  
  
 **파티션 전환**  
 현재 테이블에서 외부 전환하려는 원본 파티션을 선택합니다.  
  
 **새 경계 값**  
 준비 테이블의 파티션에 대해 원하는 경계 값을 선택하거나 입력합니다.  
  
 **파일 그룹**  
 새 테이블의 파일 그룹을 선택합니다.  
  
 ![맨 위로 이동 링크와 함께 사용되는 화살표 아이콘](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [섹션 내용](#Top)  
  
##  <a name="select-output-option-page"></a><a name="OutputOption"></a> 출력 옵션 선택 페이지  
 **출력 옵션 선택** 페이지를 사용하여 파티션에 대한 수정을 완료하는 방법을 지정할 수 있습니다.  
  
### <a name="create-script"></a>스크립트 만들기  
 마법사가 완료되면 쿼리 편집기에 테이블의 파티션을 수정하는 스크립트가 만들어집니다. 이 스크립트를 검토하려면 **스크립트 만들기** 를 선택한 다음 수동으로 스크립트를 실행합니다.  
  
 **파일로 스크립팅**  
 스크립트를 .sql 파일로 생성합니다. **유니코드** 또는 **ANSI 텍스트** 를 지정합니다. 파일의 이름과 위치를 지정하려면 **찾아보기** 를 클릭합니다.  
  
 **클립보드로 스크립팅**  
 스크립트를 클립보드에 저장합니다.  
  
 **새 쿼리 창으로 스크립팅**  
 쿼리 편집기 창에 스크립트를 생성합니다. 열려 있는 편집기 창이 없으면 스크립트 대상으로 사용할 새 편집기 창이 열립니다.  
  
### <a name="run-immediately"></a>즉시 실행  
 **Run immediately**  
 **다음** 또는 **마침** 을 클릭하면 마법사가 파티션에 대한 수정을 마치도록 합니다.  
  
### <a name="schedule"></a>일정  
 예약된 날짜 및 시간에 테이블 파티션을 수정하려면 선택합니다.  
  
 **일정 변경**  
 예약된 작업의 속성을 선택, 변경하거나 볼 수 있는 **새 작업 일정** 대화 상자를 엽니다.  
  
 ![맨 위로 이동 링크와 함께 사용되는 화살표 아이콘](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [섹션 내용](#Top)  
  
##  <a name="new-job-schedule-page"></a><a name="NewJob"></a> 새 작업 일정 페이지  
 **새 작업 일정** 페이지를 사용하여 일정 속성을 확인하고 변경할 수 있습니다.  
  
### <a name="options"></a>옵션  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업에 대해 원하는 일정 유형을 선택합니다.  
  
 **이름**  
 새 일정 이름을 입력합니다.  
  
 **이 일정 내의 작업**  
 이 일정을 사용하는 기존 작업을 표시합니다.  
  
 **일정 유형**  
 일정 유형을 선택합니다.  
  
 **Enabled**  
 일정을 사용하거나 사용하지 않습니다.  
  
### <a name="recurring-schedule-types-options"></a>되풀이 일정 유형 옵션  
 예약된 작업의 빈도를 선택합니다.  
  
 **되풀이**  
 일정 되풀이 간격을 선택합니다.  
  
 **매**  
 일정 되풀이 간격을 일 또는 주 단위(수)로 선택합니다. 월별 일정에는 이 옵션을 사용할 수 없습니다.  
  
 **월요일**  
 월요일에 작업이 수행되도록 설정합니다. 주별 일정에만 사용할 수 있습니다.  
  
 **화요일**  
 화요일에 작업이 수행되도록 설정합니다. 주별 일정에만 사용할 수 있습니다.  
  
 **수요일**  
 수요일에 작업이 수행되도록 설정합니다. 주별 일정에만 사용할 수 있습니다.  
  
 **목요일**  
 목요일에 작업이 수행되도록 설정합니다. 주별 일정에만 사용할 수 있습니다.  
  
 **금요일**  
 금요일에 작업이 수행되도록 설정합니다. 주별 일정에만 사용할 수 있습니다.  
  
 **토요일**  
 토요일에 작업이 수행되도록 설정합니다. 주별 일정에만 사용할 수 있습니다.  
  
 **일요일**  
 일요일에 작업이 수행되도록 설정합니다. 주별 일정에만 사용할 수 있습니다.  
  
 **Day**  
 일정이 시작되는 날짜를 선택합니다. 월별 일정에만 사용할 수 있습니다.  
  
 **일 /**  
 일정 되풀이 간격을 월 단위(수)로 선택합니다. 월별 일정에만 사용할 수 있습니다.  
  
 **이**  
 해당 월의 특정 주에 있는 특정 요일에 대한 일정을 지정합니다. 월별 일정에만 사용할 수 있습니다.  
  
 **한 번 수행**  
 매일 작업이 수행되도록 시간을 설정합니다.  
  
 **되풀이 수행**  
 작업 발생 간격을 시와 분으로 설정합니다.  
  
 **시작 날짜**  
 이 일정을 개시할 날짜를 설정합니다.  
  
 **종료 날짜**  
 일정을 종료할 날짜를 설정합니다.  
  
 **종료 날짜 없음**  
 일정을 무기한 유지하도록 지정합니다.  
  
### <a name="one-time-schedule-types-options"></a>일회 일정 유형 옵션  
 작업을 한 번 실행하도록 예약할 경우 미래의 날짜와 시간을 선택해야 합니다.  
  
 **Date**  
 작업을 실행할 날짜를 선택합니다.  
  
 **Time**  
 작업을 실행할 시간을 선택합니다.  
  
 ![맨 위로 이동 링크와 함께 사용되는 화살표 아이콘](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [섹션 내용](#Top)  
  
##  <a name="summary-page"></a><a name="Summary"></a> 요약 페이지  
 **요약** 페이지를 사용하여 이전 페이지에서 선택한 옵션을 검토할 수 있습니다.  
  
### <a name="ui-element-list"></a>UI 요소 목록  
 **선택 항목 검토**  
 마법사의 각 페이지에서 사용자가 선택한 항목을 표시합니다. 이전에 선택한 옵션을 확장하고 보려면 노드를 클릭합니다.  
  
 ![맨 위로 이동 링크와 함께 사용되는 화살표 아이콘](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [섹션 내용](#Top)  
  
##  <a name="progress-page"></a><a name="Progress"></a> 진행률 페이지  
 **진행률** 페이지를 사용하여 **파티션 관리 마법사** 의 동작에 대한 상태 정보를 모니터링할 수 있습니다. 마법사에서 선택한 옵션에 따라 **진행률** 페이지에 하나 이상의 동작이 포함될 수 있습니다. 맨 위에 있는 상자에는 전반적인 마법사 상태와 수신된 상태, 오류 및 경고 메시지의 수가 표시됩니다.  
  
### <a name="options"></a>옵션  
 **세부 정보**  
 동작, 상태 및 마법사가 수행한 동작의 결과로 반환된 모든 메시지를 제공합니다.  
  
 **동작**  
 각 동작의 이름과 유형을 지정합니다.  
  
 **상태**  
 마법사 동작 결과 전체적으로 **성공** 값을 반환했는지 또는 **실패** 값을 반환했는지 여부를 나타냅니다.  
  
 **메시지**  
 프로세스에서 반환된 모든 오류 또는 경고 메시지를 제공합니다.  
  
 **중지**  
 마법사의 동작을 중지합니다.  
  
 **Report**  
 **파티션 관리 마법사** 의 결과가 포함된 보고서를 만듭니다. 옵션은 다음과 같습니다.  
  
-   **보고서 보기**  
  
-   **보고서를 파일로 저장**  
  
-   **클립보드에 보고서 복사**  
  
-   **보고서를 전자 메일로 보내기**  
  
 **보고서 보기**  
 **보고서 보기** 대화 상자를 엽니다. 이 대화 상자에는 **파티션 관리 마법사** 의 진행률에 대한 텍스트 보고서가 들어 있습니다.  
  
 **닫기**  
 마법사를 닫습니다.  
  
 ![맨 위로 이동 링크와 함께 사용되는 화살표 아이콘](/analysis-services/analysis-services/instances/media/uparrow16x16.gif "맨 위로 이동 링크와 함께 사용되는 화살표 아이콘") [섹션 내용](#Top)  
  
## <a name="see-also"></a>참고 항목  
 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)  
  
