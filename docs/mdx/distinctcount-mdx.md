---
description: DistinctCount(MDX)
title: DistinctCount (MDX) | Microsoft Docs
ms.date: 11/12/2020
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 28807d1a24f97a6b197ad56d0434399ab53cd742
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584850"
---
# <a name="distinctcount-mdx"></a>DistinctCount(MDX)


  집합에서 공백이 아닌 고유한 튜플 수를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
DistinctCount(Set_Expression)  
```  
  
## <a name="arguments"></a>인수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="remarks"></a>설명  
 **DistinctCount** 함수는와 동일 `Count(Distinct(Set_Expression), EXCLUDEEMPTY)` 합니다.  
  
## <a name="examples"></a>예  
 다음 쿼리에서는 DistinctCount 함수를 사용하는 방법을 보여 줍니다.  
  
 `WITH SET MySet AS`  
  
 `{[Customer].[Customer Geography].[Country].&[Australia],[Customer].[Customer Geography].[Country].&[Australia],`  
  
 `[Customer].[Customer Geography].[Country].&[Canada],[Customer].[Customer Geography].[Country].&[France],`  
  
 `[Customer].[Customer Geography].[Country].&[United Kingdom],[Customer].[Customer Geography].[Country].&[United Kingdom]}`  
  
 `*`  
  
 `{([Date].[Calendar].[Date].&[20010701],[Measures].[Internet Sales Amount] )}`  
  
 `//Returns the value 3 because Internet Sales Amount is null`  
  
 `//for the UK on the date specified`  
  
 `MEMBER MEASURES.SETDISTINCTCOUNT AS`  
  
 `DISTINCTCOUNT(MySet)`  
  
 `SELECT {MEASURES.SETDISTINCTCOUNT} ON 0`  
  
 `FROM [Adventure Works]`  
 
DistinctCount 함수는 집합에 있는 항목의 고유 개수를 반환 합니다. 이 예제에서 선택적 두 번째 매개 변수는 지정 된 튜플에 대 한 값이 없는 항목을 제외 하는 데 사용 됩니다. 이 경우 첫 번째 매개 변수에서 집합에 4 개의 고유한 항목이 있지만 함수는 오스트레일리아, 캐나다 및 프랑스만 Internet Sales Amount의 7 월 2001 1 일에 대 한 데이터를 포함 하기 때문에 3을 반환 합니다.
 
## <a name="see-also"></a>참고 항목  
 [MDX&#41; &#40;&#40;집합 수&#41;](../mdx/count-set-mdx.md)   
 [MDX 함수 참조&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
