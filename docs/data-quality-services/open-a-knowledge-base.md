---
description: 기술 자료 열기
title: 기술 자료 열기
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.openkb.f1
ms.assetid: a5f010a5-b762-41c9-881b-bf0c192dca83
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 5d93731b7e28aafbffdf659678c0017d37ce61db
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88395889"
---
# <a name="open-a-knowledge-base"></a>기술 자료 열기

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )에서 기존 기술 자료를 열어 도메인 관리, 기술 자료 검색 또는 일치 정책 추가를 수행할 준비를 갖추는 방법에 대해 설명합니다.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
 기술 자료를 열려면 기술 자료가 이미 생성되어 있고 게시되었거나(다른 사람이 생성한 경우) 닫혀 있어야 합니다(본인이 생성한 경우).  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 기술 자료를 열려면 DQS_MAIN 데이터베이스에 대한 dqs_kb_editor 또는 dqs_administrator 역할이 있어야 합니다.  
  
##  <a name="open-a-knowledge-base"></a><a name="Open"></a> 기술 자료 열기  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Data Quality Client 응용 프로그램을 실행](../data-quality-services/run-the-data-quality-client-application.md)합니다.  
  
2.  [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 홈 화면에서 **기술 자료 열기**를 클릭합니다.  
  
3.  테이블에서 기술 자료를 선택합니다. 기술 자료의 도메인 및 일치 규칙이 페이지의 오른쪽 창에 표시됩니다.  
  
    > [!NOTE]  
    >  테이블에서 기술 자료를 마우스 오른쪽 단추로 클릭하여 기술 자료에 대한 작업을 수행할 수 있습니다. 기술 자료를 열거나, 다른 이름으로 저장하거나, 잠금을 해제하거나, 작업을 취소하거나, 이름을 바꾸거나, 속성을 표시할 수 있습니다.  
  
4.  **작업 선택**에서 기술 자료에 대해 수행할 작업을 선택합니다.  
  
    -   **도메인 관리** 를 선택하여 기술 자료의 도메인을 수정하는 데 사용하는 화면으로 이동합니다.  
  
    -   **기술 자료 검색** 을 선택하여 데이터 샘플을 분석하고 기술 자료의 도메인을 결과로 채우는 데 사용하는 마법사를 시작합니다.  
  
    -   **일치 정책** 을 선택하여 일치 정책을 만들고 기술 자료에 추가합니다.  
  
5.  **열기**를 클릭합니다.  
  
    > [!NOTE]  
    >  기술 자료를 마우스 오른쪽 단추로 클릭한 다음 열기를 클릭하여 기술 자료를 열 수도 있습니다. 상황에 맞는 메뉴의 다른 명령을 사용하여 기술 자료를 다른 이름으로 저장하거나, 잠금을 해제하거나, 작업을 취소하거나, 이름을 바꾸거나, 속성을 표시할 수 있습니다.  
  
    > [!NOTE]  
    >  기술 자료가 잠겨 있어 열 수 없는 경우 아래 섹션을 참조하세요.  
  
## <a name="open-a-recent-knowledge-base"></a>최신 기술 자료 열기  
 가장 최근에 열어 본 5개 기술 자료가 DQS 홈 페이지의 **최근 기술 자료** 목록에 표시됩니다. 따라서 **기술 자료 열기** 페이지로 이동하지 않고도 최근에 작업한 기술 자료를 열 수 있습니다.  
  
-   잠겨 있지 않은 최근에 사용한 항목 목록에서 기술 자료를 열려면 기술 자료에 대한 오른쪽 화살표를 클릭한 다음 기술 자료를 열려는 작업을 선택합니다.  
  
-   잠겨 있는 최근에 사용한 항목 목록에서 기술 자료를 열려면 기술 자료를 클릭합니다. 그러면 괄호 안에 표시된 작업 및 페이지에서 기술 자료가 열립니다.  
  
-   다른 사용자가 잠근 최근에 사용한 항목 목록에서 기술 자료를 열려면 해당 사용자에게 연락해 기술 자료의 잠금을 해제하도록 요청합니다.  
  
##  <a name="follow-up-after-opening-a-knowledge-base"></a><a name="FollowUp"></a> 후속 작업: 기술 자료를 연 후  
 기술 자료를 연 후에는 기술 자료가 기술 자료 테이블의 상태 열에 표시된 상태로 전환됩니다. 기술 자료 검색 및 일치 정책 작업의 경우 기술 자료가 특정 마법사 페이지에서 열립니다. 도메인 관리 작업의 경우 기술 자료가 도메인 관리 페이지에서 열립니다. 상태에 대한 자세한 내용은 [기술 자료 검색 수행](../data-quality-services/perform-knowledge-discovery.md), [도메인 관리](../data-quality-services/managing-a-domain.md) 또는 [일치 정책 만들기](../data-quality-services/create-a-matching-policy.md)를 참조하세요.  
  
##  <a name="if-the-knowledge-base-is-locked"></a><a name="Locked"></a> 기술 자료가 잠긴 경우  
 첫 번째 열의 자물쇠 아이콘이 기술 자료가 잠겨 있는지 여부를 보여 줍니다. 잠긴 기술 자료의 이름은 빨간색 글꼴로 표시됩니다. 특정 사용자가 기술 자료 작업을 통해 수정 중인 기술 자료는 잠금으로 표시됩니다. 잠긴 기술 자료에서 다른 사용자가 작업을 수행할 수는 없습니다. 기술 자료에서 작업하고 있는 사용자는 기술 자료 열기 페이지의 테이블에서 기술 자료를 마우스 오른쪽 단추로 클릭하고 **잠금 해제**를 클릭하거나 기술 자료를 게시하여 기술 자료의 잠금을 해제할 수 있습니다. 잠긴 기술 자료에 커서를 두면 해당 기술 자료를 잠근 사용자와 잠근 이유를 나타내는 힌트가 표시됩니다.  
  
##  <a name="state-of-a-knowledge-base"></a><a name="State"></a> 기술 자료의 상태  
 상태 필드는 기술 자료에 대한 현재 작업 단계를 나타냅니다. 기술 자료를 열면 해당 단계에서 기술 자료가 열립니다.  
  
-   **\<Empty>**: 도메인 관리 작업에서 **게시** 를 클릭 한 다음 **예-기술 자료를 게시 하 고 종료**를 클릭 하 여 기술 자료를 게시 한 경우 기술 자료에 대 한 상태 필드가 비어 있습니다.  
  
-   **작업**중: 도메인 관리 작업에서 **게시** 를 클릭 하 고 **기술 자료에 대 한 작업을 저장 하지 않고 종료**를 클릭 하 여 기술 자료에 대 한 작업을 저장 했습니다.  
  
-   **도메인 관리**: 기술 자료의 도메인에 대한 데이터가 입력되었지만 기술 자료가 게시되지 않았고 작업 내용이 도메인 관리 작업에 남아 있습니다. 기술 자료 검색 작업을 사용할 수 없습니다. 이 현상은 **도메인 관리** 화면에서 **닫기** 를 클릭할 때 발생합니다.  
  
-   **검색 - 매핑**: 기술 자료가 **기술 자료 관리: 매핑** 페이지에서 닫혔습니다. 기술 자료가 잠겨 있으며 도메인 관리 및 일치 작업을 사용할 수 없습니다.  
  
-   **검색 - 검색**: 기술 자료가 **기술 자료 관리: 분석** 페이지에서 닫혔습니다. 기술 자료가 잠겨 있으며 도메인 관리 작업을 사용할 수 없습니다.  
  
-   **검색-값 관리**: 기술 자료가 **기술 자료 관리: 도메인 용어 관리** 페이지에서 닫혔습니다. 기술 자료가 잠겨 있으며 도메인 관리 작업을 사용할 수 없습니다.  
  
-   **일치 정책-일치 정책**: 기술 자료가 **일치 정책-일치 정책** 페이지에서 닫혔습니다. 기술 자료가 잠겨 있으며 기술 자료 검색 및 도메인 관리 작업을 사용할 수 없습니다.  
  
-   **일치 정책-일치 결과**: 기술 자료가 **일치 정책-일치 결과** 페이지에서 닫혔습니다. 기술 자료가 잠겨 있으며 기술 자료 검색 및 도메인 관리 작업을 사용할 수 없습니다.  
  
  
