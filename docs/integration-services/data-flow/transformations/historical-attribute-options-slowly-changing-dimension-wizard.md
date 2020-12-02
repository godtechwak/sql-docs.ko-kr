---
description: 기록 특성 옵션(느린 변경 차원 마법사)
title: 기록 특성 옵션(느린 변경 차원 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.histattriboption.f1
ms.assetid: a176ec66-ec39-4c99-99d1-c1afa8450e1e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9610a734543c9199e54d3f8489d86e03089f10ed
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88430705"
---
# <a name="historical-attribute-options-slowly-changing-dimension-wizard"></a>기록 특성 옵션(느린 변경 차원 마법사)

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  **기록 특성 옵션** 대화 상자를 사용하여 시작 및 종료 날짜별로 기록 특성을 표시하거나 이 용도로 특별히 만든 열에 기록 특성을 기록할 수 있습니다.  
  
 이 마법사에 대한 자세한 내용은 [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)를 참조하십시오.  
  
## <a name="options"></a>옵션  
 **단일 열을 사용하여 현재 및 만료 레코드 표시**  
 단일 열을 사용하여 기록 특성의 상태를 기록하도록 선택한 경우 다음 옵션을 사용할 수 있습니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**현재 레코드 표시 열**|현재 레코드를 표시할 열을 선택합니다.|  
|**현재 값**|**True** 또는 **현재** 를 사용하여 현재 레코드인지 여부를 표시할 수 있습니다.|  
|**만료 값**|**False** 또는 **만료됨** 을 사용하여 레코드가 기록 값인지 여부를 표시할 수 있습니다.|  
  
 **시작 및 종료 날짜를 사용하여 현재 및 만료 레코드 식별**  
 이 옵션의 차원 테이블에는 날짜 열이 포함되어 있어야 합니다. 시작 및 종료 날짜별로 기록 특성을 표시하도록 선택한 경우 다음 옵션을 사용할 수 있습니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**시작 날짜 열**|시작 날짜를 포함할 차원 테이블의 열을 선택합니다.|  
|**종료 날짜 열**|종료 날짜를 포함할 차원 테이블의 열을 선택합니다.|  
|**날짜 값 설정 변수**|목록에서 날짜 변수를 선택합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [느린 변경 차원 마법사를 사용하여 출력 구성](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
