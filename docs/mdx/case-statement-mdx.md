---
description: CASE 문(MDX)
title: CASE 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7a5907eb58fa102c46fa22af97116c4fad0f217a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466505"
---
# <a name="case-statement-mdx"></a>CASE 문(MDX)


  여러 비교에서 조건에 따라 특정 값을 반환할 수 있습니다. CASE 문에는 다음과 같은 두 가지 유형이 있습니다.  
  
-   식을 일련의 단순 식과 비교하여 특정 값을 반환하는 단순 CASE 문  
  
-   일련의 부울 식을 계산하여 특정 값을 반환하는 검색된 CASE 문  
  
## <a name="syntax"></a>구문  
  
```  
  
Simple Case Statement  
CASE [input_expression]  
WHEN when_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
  
Search Case Statement  
CASE   
WHEN Boolean_expression THEN when_true_result_expression  
[...n]  
[ELSE else_result_expression]  
END  
```  
  
## <a name="arguments"></a>인수  
 *input_expression*  
 스칼라 값으로 확인되는 MDX 식입니다.  
  
 *when_expression*  
 *Input_expression* 계산 되는 지정 된 스칼라 값입니다 .이 값이 true로 평가 되 면 *else_result_expression*의 스칼라 값이 반환 됩니다.  
  
 *when_true_result_expression*  
 WHEN 절이 true일 때 반환되는 스칼라 값입니다.  
  
 *else_result_expression*  
 true인 WHEN 절이 없을 때 반환되는 스칼라 값입니다.  
  
 *Boolean_expression*  
 스칼라 값으로 계산되는 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 ELSE 절이 없고 WHEN 절이 모두 false를 반환한 경우 결과는 빈 셀이 됩니다.  
  
## <a name="simple-case-expression"></a>단순 CASE 식  
 MDX는 *input_expression* 을 스칼라 값으로 확인 하 여 단순 case 식을 계산 합니다. 그런 다음이 스칼라 값은 *when_expression*의 스칼라 값과 비교 됩니다. 두 스칼라 값이 일치 하는 경우 CASE 문은 *when_true_expression*의 값을 반환 합니다. 두 스칼라 값이 일치하지 않으면 다음 WHEN 절이 실행됩니다. 모든 WHEN 절이 false 이면 ELSE 절의 *else_result_expression* 값 (있는 경우)이 반환 됩니다.  
  
 다음 예에서는 여러 WHEN 절에 대해 Reseller Order Count 측정값을 확인하고 각 연도의 Reseller Order Count 측정값에 따라 결과를 반환합니다. 재판매인 주문 수 값이 WHEN 절의 *when_expression* 에 지정 된 스칼라 값과 일치 하지 않으면 *else_result_expression* 의 스칼라 값이 반환 됩니다.  
  
```  
WITH MEMBER [Measures].x AS   
CASE [Measures].[Reseller Order Count]  
   WHEN 0 THEN 'NONE'  
   WHEN 1 THEN 'SMALL'  
   WHEN 2 THEN 'SMALL'  
   WHEN 3 THEN 'MEDIUM'  
   WHEN 4 THEN 'MEDIUM'  
   WHEN 5 THEN 'LARGE'  
   WHEN 6 THEN 'LARGE'  
      ELSE 'VERY LARGE'  
END  
SELECT Calendar.[Calendar Year] on 0  
, NON EMPTY [Geography].[Postal Code].Members ON 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="searched-case-expression"></a>검색된 CASE 식  
 CASE 식을 사용하여 보다 복잡한 평가를 수행하려면 검색된 CASE 식을 사용합니다. 이 검색 식의 변형을 사용하면 입력 식이 값 범위 내에 있는지 여부를 확인할 수 있습니다. MDX는 WHEN 절이 CASE 문에 나타나는 순서대로 WHEN 절을 반환합니다.  
  
 다음 예에서는 여러 개의 WHEN 절에 대해 지정 된 *Boolean_expression* 에 대해 재판매인 Order Count 측정값이 평가 됩니다. 각 연도의 Reseller Order Count 측정값에 따라 결과를 반환합니다. WHEN 절은 나타나는 순서대로 확인되므로 6보다 큰 모든 값에 대해 각 값을 명시적으로 지정하지 않고 "VERY LARGE"라는 값을 쉽게 할당할 수 있습니다. 재판매인 Order Count 값이 WHEN 절에 지정 되지 않은 경우 *else_result_expression* 의 스칼라 값이 반환 됩니다.  
  
```  
WITH MEMBER [Measures].x AS   
CASE   
   WHEN [Measures].[Reseller Order Count] > 6 THEN 'VERY LARGE'  
   WHEN [Measures].[Reseller Order Count] > 4 THEN 'LARGE'  
   WHEN [Measures].[Reseller Order Count] > 2 THEN 'MEDIUM'  
   WHEN [Measures].[Reseller Order Count] > 0 THEN 'SMALL'  
   ELSE "NONE"  
END  
SELECT Calendar.[Calendar Year] on 0,  
NON EMPTY [Geography].[Postal Code].Members on 1  
FROM [Adventure Works]  
WHERE [Measures].x  
```  
  
## <a name="see-also"></a>참고 항목  
 [MDX 스크립팅 문&#40;MDX&#41;](../mdx/mdx-scripting-statements-mdx.md)  
  
  
