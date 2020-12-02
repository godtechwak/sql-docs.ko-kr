---
description: ~(비트 Not)(SSIS 식)
title: ~(비트 Not)(SSIS 식) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- bitwise NOT (~)
- ~ (bitwise NOT)
ms.assetid: e4413ddd-0d0e-40c3-9c76-b5ce323218ec
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ae8fa8bb0aae6700d1082e52385c7d162c193b84
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127151"
---
# <a name="-bitwise-not-ssis-expression"></a>~(비트 Not)(SSIS 식)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  정수의 비트 부정을 수행합니다. 이 연산자는 부호 있는 정수 또는 부호 없는 정수 데이터 형식에 적용할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
~integer_expression  
  
```  
  
## <a name="arguments"></a>인수  
 *integer_expression*  
 정수 데이터 형식의 유효한 식입니다. *integer* _ *expression* 은 비트 연산을 위해 이진수로 변환되는 정수입니다. 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="result-types"></a>결과 형식  
 *integer_expression* 의 데이터 형식을 반환합니다.  
  
## <a name="remarks"></a>설명  
 None  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 숫자 170(0000 0000 1010 1010)에 비트 ~(NOT) 연산을 수행합니다. 숫자는 부호 있는 정수입니다.  
  
```  
  
~ 170  
```  
  
 식은 -170(1111111101010101)으로 계산됩니다.  
  
 0000000010101010  
  
 ---------------------\-  
  
 1111111101010101  
  
## <a name="see-also"></a>참고 항목  
 [연산자 우선 순위 및 계산 방향](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
