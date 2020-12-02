---
description: 패키지에서 주석 사용
title: 패키지에서 주석 사용 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- self-documenting packages
- adding annotations
- annotations [Integration Services]
ms.assetid: 48c8ed9a-b10d-490c-9ba7-4b77aa44e3dd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 88a927a23696e5de7a1e079cb517078dc318b69c
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "92193765"
---
# <a name="use-annotations-in-packages"></a>패키지에서 주석 사용

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너는 패키지에 대한 설명을 제공하고 이해 및 유지 관리를 쉽게 하기 위해 사용할 수 있는 주석을 제공합니다. 주석은 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너의 제어 흐름, 데이터 흐름 및 이벤트 처리기에 추가할 수 있습니다. 주석에는 모든 종류의 텍스트가 포함될 수 있으며 패키지에 레이블, 설명 및 기타 설명 정보를 추가하는 데 유용합니다. 주석은 디자인 타임 전용 기능입니다. 예를 들어 주석은 로그에 기록되지 않습니다.  
  
 Enter 키를 누르면 텍스트가 다음 줄로 줄 바꿈됩니다. 텍스트 줄을 추가하면 주석 상자의 크기가 자동으로 늘어납니다. 패키지 파일의 CDATA 섹션에 있는 패키지 주석은 일반 텍스트로 유지됩니다.  
  
 패키지 파일의 형식을 변경하는 방법에 대한 자세한 내용은 [SSIS 패키지 형식](./integration-services-ssis-packages.md)을 참조하세요.  
  
 패키지가 저장될 때 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너는 주석을 해당 패키지에 저장합니다.  
  
## <a name="add-an-annotation-to-a-package"></a>패키지에 주석 추가  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]에서 주석을 추가할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
2.  솔루션 탐색기에서 패키지를 두 번 클릭하여 엽니다.  
  
3.  [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 **제어 흐름**, **데이터 흐름** 또는 **이벤트 처리기** 탭의 디자인 화면에서 아무 곳이나 마우스 오른쪽 단추로 클릭한 후 **주석 추가** 를 클릭합니다. 탭의 디자인 화면에 텍스트 블록이 표시됩니다.  
  
4.  텍스트를 추가합니다.  
  
    > [!NOTE]  
    >  텍스트를 추가하지 않은 상태에서 블록 바깥을 클릭하면 텍스트 블록이 제거됩니다.  
  
5.  주석 텍스트의 크기나 서식을 변경하려면 주석을 마우스 오른쪽 단추로 클릭하고 **텍스트 주석 글꼴 설정** 을 클릭합니다.  
  
6.  텍스트 줄을 추가하려면 Enter 키를 누릅니다.  
  
     텍스트 줄을 추가하면 주석 상자의 크기가 자동으로 늘어납니다.  
  
7.  그룹에 주석을 추가하려면 주석을 마우스 오른쪽 단추로 클릭하고 **그룹** 을 클릭합니다.  
  
8.  업데이트된 패키지를 저장하려면 **파일** 메뉴에서 **모두 저장** 을 클릭합니다.