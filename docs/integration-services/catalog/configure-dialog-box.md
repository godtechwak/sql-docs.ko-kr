---
description: 구성 대화 상자
title: 구성 대화 상자 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.configure.f1
- sql13.SSIS.SSMS.ISPROJECTPROP.REFERENCES.F1
- sql13.SSIS.SSMS.ISPROJECTPROP.PARAMETERS.F1
ms.assetid: 10183c8d-b1be-420f-972a-96ea97d4f4d8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cdbcc9b0a03b0afefe56152dc6b29c7ae59ea4cc
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130682"
---
# <a name="configure-dialog-box"></a>구성 대화 상자

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **구성** 대화 상자를 사용하여 패키지 및 프로젝트에 대한 매개 변수, 연결 관리자, 환경 참조 등을 구성할 수 있습니다.  
  
 **수행 작업**  
  
-   [구성 대화 상자 열기](#open_dialog)  
  
-   [매개 변수 페이지에서 옵션 설정](#parameter)  
  
-   [참조 페이지에서 옵션 설정](#references)  
  
##  <a name="open-the-configure-dialog-box"></a><a name="open_dialog"></a> 구성 대화 상자 열기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 연결합니다.  
  
     SSISDB 데이터베이스를 호스팅하는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 트리를 확장하여 **Integration Services 카탈로그** 노드를 표시합니다.  
  
3.  **SSISDB** 노드를 확장합니다.  
  
4.  구성할 패키지 또는 프로젝트가 포함된 폴더를 확장합니다.  
  
5.  패키지 또는 프로젝트를 다시 마우스 오른쪽 단추로 클릭한 다음 **구성** 을 클릭합니다.  
  
##  <a name="set-the-options-on-the-parameters-page"></a><a name="parameter"></a> 매개 변수 페이지에서 옵션 설정  
 **매개 변수** 페이지를 사용하여 매개 변수 이름 및 값을 확인한 후 값을 수정합니다.  
  
 **범위** 드롭다운 목록에서 **매개 변수** 및 **연결 관리자** 탭에 표시된 매개 변수의 범위를 선택합니다.  
  
 다음은 **매개 변수** 탭의 옵션 목록입니다.  
  
 **컨테이너**  
 매개 변수가 포함된 개체를 나열합니다.  
  
 **이름**  
 매개 변수 이름을 나열합니다.  
  
 **값**  
 매개 변수 값을 나열합니다. 줄임표 단추를 클릭하여 **매개 변수 값 설정** 대화 상자의 값을 변경합니다.  
  
 다음은 **연결 관리자** 탭의 옵션 목록입니다. 연결 관리자 속성 값을 변경하려면 이 탭을 사용합니다. 속성에 대한 매개 변수가 SSIS 서버에 자동으로 생성됩니다.  
  
 **컨테이너**  
 연결 관리자 이름이 포함된 개체를 나열합니다.  
  
 **이름**  
 연결 관리자 이름을 나열합니다.  
  
 **속성 이름**  
 연결 관리자 속성 이름을 나열합니다.  
  
 **값**  
 연결 관리자 속성에 할당된 값을 나열합니다. 줄임표 단추를 클릭하여 **매개 변수 값 설정** 대화 상자의 값을 변경합니다. 리터럴 값을 입력하거나 사용하려는 값이 포함된 환경 변수를 매핑하거나, 패키지의 기본값을 사용할 수 있습니다.  
  
##  <a name="set-the-options-on-the-references-page"></a><a name="references"></a> 참조 페이지에서 옵션 설정  
 **참조** 페이지를 사용하여 환경에 대한 참조를 추가 및 제거하고 환경 속성에 액세스합니다.  
  
 환경에서는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포한 프로젝트에 포함된 패키지의 런타임 값을 지정합니다.  
  
 **환경**  
 환경을 나열합니다.  
  
 **환경 폴더**  
 환경이 포함된 폴더를 나열합니다.  
  
 **열기**  
 **환경 속성** 대화 상자를 열려면 클릭합니다.  
  
 **추가**  
 환경에 대한 참조를 추가하려면 클릭합니다. **환경 찾아보기** 대화 상자에서 환경을 클릭한 다음 **확인** 을 클릭합니다.  
  
 **SSISDB** 노드 아래의 모든 프로젝트 폴더에 포함된 환경을 선택할 수 있습니다.  
  
 **제거**  
 **참조** 영역에 나열된 환경을 클릭한 다음 **제거** 를 클릭합니다.  
  
  
