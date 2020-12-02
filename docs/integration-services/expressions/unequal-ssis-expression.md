---
description: '!=(같지 않음)(SSIS 식)'
title: '!=(같지 않음)(SSIS 식) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- unequal operator (!=)
- '!= (not equal to)'
ms.assetid: fad20e85-c0e6-42bf-af70-2bc80ee09be5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7149d9e82243d1bd377fd4e7f75c2ce16edd2947
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123236"
---
# <a name="-unequal-ssis-expression"></a>!=(같지 않음)(SSIS 식)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  호환 가능한 데이터 형식의 두 식이 같지 않은지 비교합니다. 식 계산기는 비교를 수행하기 전에 많은 데이터 형식을 자동으로 변환합니다.  
  
 그러나 일부 데이터 형식을 사용할 경우 식이 성공적으로 계산되려면 식에 명시적 캐스트가 포함되어야 합니다. 데이터 형식 간 올바른 캐스트에 대한 자세한 내용은 [캐스트&#40;SSIS 식&#41;](../../integration-services/expressions/cast-ssis-expression.md)를 참조하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
expression1 != expression2  
  
```  
  
## <a name="arguments"></a>인수  
 *expression1, expression2*  
 유효한 식입니다.  
  
## <a name="result-types"></a>결과 형식  
 DT_BOOL  
  
## <a name="remarks"></a>설명  
 비교하는 두 식 중 하나가 Null이면 비교 결과도 Null입니다. 두 식이 모두 Null이면 결과도 Null입니다.  
  
 식 집합 *expression1* 및 *expression2* 는 다음 규칙 중 하나를 따라야 합니다.  
  
-   **Numeric***expression1* 및 *expression2* 모두 숫자 데이터 형식이어야 합니다. 데이터 형식의 교집합은 식 계산기가 수행하는 암시적 숫자 변환에 대한 규칙에 지정된 대로 숫자 데이터 형식이어야 합니다. 두 숫자 데이터 형식의 교집합은 Null일 수 없습니다. 자세한 내용은 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)을 참조하세요.  
  
-   **Character***expression1* 및 *expression2* 모두 DT_STR 또는 DT_WSTR 데이터 형식으로 계산되어야 합니다. 두 식이 서로 다른 문자열 데이터 형식으로 계산될 수 있습니다.  
  
    > [!NOTE]  
    >  문자열 비교는 대/소문자, 악센트, 일본어 가나 및 전자/반자를 구분합니다.  
  
-   **Date, Time 또는 Date/Time***expression1* 및 *expression2* 모두는 DT_DBDATE, DT_DATE, DT_DBTIME, DT_DBTIME2, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAPMOFFSET 또는 DT_FILETIME 데이터 형식 중 하나로 계산되어야 합니다.  
  
    > [!NOTE]  
    >  시간 데이터 형식으로 계산되는 식과 날짜 또는 날짜/시간 데이터 형식 중 하나로 계산되는 식 사이의 비교는 지원되지 않습니다. 시스템에서 오류가 발생합니다.  
  
     식을 비교하는 경우 시스템은 다음 변환 규칙을 나열된 순서대로 적용합니다.  
  
    -   두 식이 같은 데이터 형식으로 계산되는 경우 해당 데이터 형식의 비교가 수행됩니다.  
  
    -   하나의 식이 DT_DBTIMESTAMPOFFSET 데이터 형식인 경우 다른 식은 DT_DBTIMESTAMPOFFSET으로 암시적으로 변환되며 DT_DBTIMESTAMPOFFSET 비교가 수행됩니다. 자세한 내용은 [Integration Services Data Types in Expressions](../../integration-services/expressions/integration-services-data-types-in-expressions.md)을 참조하세요.  
  
    -   하나의 식이 DT_DBTIMESTAMP2 데이터 형식인 경우 다른 식은 DT_DBTIMESTAMP2로 암시적으로 변환되며 DT_DBTIMESTAMP2 비교가 수행됩니다.  
  
    -   하나의 식이 DT_DBTIME2 데이터 형식인 경우 다른 식은 DT_DBTIME2로 암시적으로 변환되며 DT_DBTIME2 비교가 수행됩니다.  
  
    -   하나의 식이 DT_DBTIMESTAMPOFFSET, DT_DBTIMESTAMP2 또는 DT_DBTIME2 이외의 형식인 경우 다른 식은 DT_DBTIMESTAMP 데이터 형식으로 변환되어 비교됩니다.  
  
     식을 비교할 때 시스템에서는 다음과 같이 가정합니다.  
  
    -   각 식이 소수 자릿수 초를 포함하는 데이터 형식인 경우 시스템은 소수 자릿수 초의 자릿수가 가장 적은 데이터 형식의 나머지 자릿수를 0으로 가정합니다.  
  
    -   각 식이 날짜 데이터 형식이고 이 중 하나에만 표준 시간대 오프셋이 있는 경우 시스템은 표준 시간대 오프셋이 없는 날짜 데이터 형식을 UTC(Coordinated Universal Time)로 가정합니다.  
  
-   **Logical***expression1* 과 *expression2* 는 모두 부울로 계산되어야 합니다.  
  
-   **GUID***expression1* 및 *expression2* 모두 DT_GUID 데이터 형식으로 계산되어야 합니다.  
  
-   **Binary***expression1* 및 *expression2* 모두 DT_BYTES 데이터 형식으로 계산되어야 합니다.  
  
-   **BLOB***expression1* 및 *expression2* 모두 동일한 BLOB(Binary Large Object Block) 데이터 형식 DT_TEXT, DT_NTEXT 또는 DT_IMAGE로 계산되어야 합니다.  
  
 데이터 형식에 대한 자세한 내용은 [Integration Services Data Types](../../integration-services/data-flow/integration-services-data-types.md)을 참조하세요.  
  
## <a name="expression-examples"></a>식 예  
 이 예에서는 현재 날짜가 2003년 7월 4일이 아닌 경우에만 TRUE가 됩니다. 자세한 내용은 [GETDATE&#40;SSIS 식&#41;](../../integration-services/expressions/getdate-ssis-expression.md)를 참조하세요.  
  
```  
"7/4/2003" != GETDATE()  
```  
  
 이 예에서는 **ListPrice** 열의 값이 500이 아니면 TRUE가 됩니다.  
  
```  
ListPrice != 500  
```  
  
 이 예에서는 변수 **LPrice** 를 사용합니다. **LPrice** 의 값이 500이 아니면 이 예는 TRUE가 됩니다. 식을 구문 분석하려면 변수의 데이터 형식이 숫자여야 합니다.  
  
```  
@LPrice != 500  
```  
  
## <a name="see-also"></a>참고 항목  
 [== &#40;같음&#41;&#40;SSIS 식&#41;](../../integration-services/expressions/equal-ssis-expression.md)   
 [연산자 우선 순위 및 계산 방향](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [연산자&#40;SSIS 식&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
