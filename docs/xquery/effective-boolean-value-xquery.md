---
title: 유효한 부울 값 (XQuery) | Microsoft Docs
description: XQuery의 유효한 부울 값에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- effective Boolean value [XQuery]
- Boolean values
- XQuery, effective Boolean values
- EBV
ms.assetid: 506682b1-b6c9-45e2-aa54-7abd5844c3f1
author: rothja
ms.author: jroth
ms.openlocfilehash: 748042147b2e776c096296a98ce27dbc645e2d49
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85753652"
---
# <a name="effective-boolean-value-xquery"></a>유효한 부울 값(XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  다음은 유효한 부울 값입니다.  
  
-   피연산자가 빈 시퀀스이거나 부울이 거짓인 경우 False입니다.  
  
-   그렇지 않으면 값이 True입니다.  
  
 유효한 부울 값은 단일 부울 값, 노드 시퀀스 또는 빈 시퀀스를 반환하는 식에 대해 계산될 수 있습니다. 다음 유형의 식을 처리할 때는 부울 값이 암시적으로 계산됩니다.  
  
-   논리 식  
  
-   [Not 함수](../xquery/functions-on-boolean-values-not-function.md)  
  
-   FLWOR 식의 WHERE 절  
  
-   [조건식](../xquery/conditional-expressions-xquery.md)  
  
-   [QuantifiedeExpressions](../xquery/quantified-expressions-xquery.md)  
  
 다음은 유효한 부울 값 예입니다. **If** 식이 처리 되 면 조건의 유효한 부울 값이 결정 됩니다. `/a[1]`은 빈 시퀀스를 반환하기 때문에 유효한 부울 값은 False입니다. 결과는 하나의 텍스트 노드(False)가 포함된 XML로 반환됩니다.  
  
```  
value is false  
DECLARE @x XML  
SET @x = '<b/>'  
SELECT @x.query('if (/a[1]) then "true" else "false"')  
go  
```  
  
 다음 예에서는 식이 비어 있지 않은 시퀀스를 반환하기 때문에 유효한 부울 값이 True입니다.  
  
```  
DECLARE @x XML  
SET @x = '<a/>'  
SELECT @x.query('if (/a[1]) then "true" else "false"')  
go  
```  
  
 형식화 된 **xml** 열 또는 변수를 쿼리할 때 부울 유형의 노드를 가질 수 있습니다. 이 경우 **데이터 ()** 는 부울 값을 반환 합니다. 쿼리 식이 부울 값 True를 반환하는 경우 유효한 부울 값은 다음 예에서와 같이 True입니다. 이 예에는 다음 내용에 대해서도 설명됩니다.  
  
-   XML 스키마 컬렉션이 생성됩니다. 컬렉션의 요소는 \<b> 부울 형식입니다.  
  
-   형식화 된 **xml** 변수를 만들고 쿼리 합니다.  
  
-   `data(/b[1])` 식은 부울 값 True를 반환합니다. 따라서 이 경우 유효한 부울 값은 True입니다.  
  
-   식에서 `data(/b[2])` 부울 false 값을 반환 합니다. 따라서 이 경우 유효한 부울 값은 False입니다.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="s" type="string"/>  
      <element name="b" type="boolean"/>  
</schema>'  
go  
DECLARE @x XML(SC)  
SET @x = '<b>true</b><b>false</b>'  
SELECT @x.query('if (data(/b[1])) then "true" else "false"')  
SELECT @x.query('if (data(/b[2])) then "true" else "false"')  
go  
```  
  
## <a name="see-also"></a>참고 항목  
 [XQuery 기본 사항](../xquery/xquery-basics.md)   
 [FLWOR 문과 반복 &#40;XQuery&#41;](../xquery/flwor-statement-and-iteration-xquery.md)  
  
  
