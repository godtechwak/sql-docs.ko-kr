---
description: 데이터 마이닝 쿼리 변환
title: 데이터 마이닝 쿼리 변환 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataminingquerytrans.f1
- sql13.dts.designer.dmquerytransformation.miningmodel.f1
- sql13.dts.designer.dmquerytransformation.query.f1
helpviewer_keywords:
- Data Mining Query transformation
- prediction queries [Integration Services]
ms.assetid: 7960133b-a3e1-48af-ba43-55ed78c38e71
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8791836a066b658fb6775ce1cbf30f30c7d7d4a1
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123393"
---
# <a name="data-mining-query-transformation"></a>데이터 마이닝 쿼리 변환

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  데이터 마이닝 쿼리 변환은 데이터 마이닝 모델과 비교해서 예측 쿼리를 수행합니다. 이 변환에는 DMX(Data Mining Extensions) 쿼리를 만들기 위한 쿼리 작성기가 포함되어 있습니다. 쿼리 작성기를 사용하면 DMX 언어를 사용하는 기존 마이닝 모델과 비교해서 변환 입력 데이터를 평가하는 사용자 지정 문을 만들 수 있습니다. 자세한 내용은 [DMX&#40;Data Mining Extensions&#41; 참조](../../../dmx/data-mining-extensions-dmx-reference.md)를 참조하세요.  
  
 모델이 동일한 데이터 마이닝 구조를 기반으로 하는 경우 하나의 변환에서 여러 개의 예측 쿼리를 실행할 수 있습니다. 자세한 내용은 [데이터 마이닝 쿼리 도구](/analysis-services/data-mining/data-mining-query-tools)를 참조하세요.  
  
## <a name="configuration-of-the-data-mining-query-transformation"></a>데이터 마이닝 쿼리 변환 구성  
 데이터 마이닝 쿼리 변환은 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 연결 관리자를 사용하여 마이닝 구조와 마이닝 모델이 포함된 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 의 인스턴스나 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 프로젝트에 연결합니다. 자세한 내용은 [Analysis Services Connection Manager](../../../integration-services/connection-manager/analysis-services-connection-manager.md)을 참조하세요.  
  
 이 변환은 하나의 입력과 하나의 출력을 가지며 오류 출력은 지원하지 않습니다.  
  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 **고급 편집기** 대화 상자에는 프로그래밍 방식으로 설정할 수 있는 속성이 표시됩니다. **고급 편집기** 대화 상자를 사용하거나 프로그래밍 방식으로 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하세요.  
  
-   [Common Properties](../set-the-properties-of-a-data-flow-component.md)  
  
-   [변환 사용자 지정 속성](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 속성을 설정하는 방법에 대한 자세한 내용은 [데이터 흐름 구성 요소의 속성 설정](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)을 참조하세요.  
  
## <a name="data-mining-query-transformation-editor-mining-model-tab"></a>데이터 마이닝 쿼리 변환 편집기(마이닝 모델 탭)
  **데이터 마이닝 쿼리 변환 편집기** 대화 상자의 **마이닝 모델** 탭을 사용하여 데이터 마이닝 구조 및 해당 마이닝 모델을 선택할 수 있습니다.  
  
### <a name="options"></a>옵션  
 **연결**  
 목록 상자를 사용하여 기존 Analysis Services 연결을 선택하거나 아래에 설명된 **새로 만들기** 단추를 사용하여 새 연결을 만듭니다.  
  
 **새로 만들기**  
 **Analysis Services 연결 관리자 추가** 대화 상자를 사용하면 새 연결을 만들 수 있습니다.  
  
 **마이닝 구조**  
 사용 가능한 마이닝 모델 구조 목록에서 선택합니다.  
  
 **마이닝 모델**  
 선택한 데이터 마이닝 구조와 연관된 마이닝 모델 목록을 표시합니다.  
  
## <a name="data-mining-query-transformation-editor-query-tab"></a>데이터 마이닝 쿼리 변환 편집기(쿼리 탭)
  **데이터 마이닝 쿼리 변환 편집기** 대화 상자의 **쿼리** 탭을 사용하여 예측 쿼리를 만들 수 있습니다.  
  
### <a name="options"></a>옵션  
 **데이터 마이닝 쿼리**  
 입력란에 DMX(Data Mining Extensions) 쿼리를 직접 입력합니다.  
  
 **새 쿼리 작성**  
 그래픽 쿼리 작성기를 사용하여 DMX(Data Mining Extensions) 쿼리를 만들려면 **새 쿼리 작성** 을 클릭합니다.  
