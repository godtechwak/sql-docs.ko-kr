---
description: Except (MDX) 연산자
title: '- 남기고 (MDX) | Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f45c01cb4a2c3e4383790637b6603f789048078d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341499"
---
# <a name="except-mdx-operator"></a>Except (MDX) 연산자


  중복된 멤버를 제거하고 두 집합 간의 차집합을 반환하는 집합 연산을 수행합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Set_Expression - Set_Expression  
```  
  
#### <a name="parameters"></a>매개 변수  
 *Set_Expression*  
 집합을 반환하는 유효한 MDX 식입니다.  
  
## <a name="return-value"></a>반환 값  
 지정된 두 매개 변수에서 공유되지 않는 멤버가 포함된 집합입니다.  
  
## <a name="remarks"></a>설명  
 **-(Except)** 연산자는 [except](../mdx/except-mdx-function.md) 함수와 기능적으로 동일 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 이 연산자의 사용 방법을 보여 줍니다.  
  
```  
// This query shows the quantity of orders for all product categories  
// with the exception of Components.  
SELECT   
   [Measures].[Order Quantity] ON COLUMNS,  
   [Product].[Product Categories].[All].Children   
   - [Product].[Product Categories].[Components] ON ROWS  
FROM  
    [Adventure Works]  
```  
  
## <a name="see-also"></a>참고 항목  
 [Mdx 연산자 참조 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
