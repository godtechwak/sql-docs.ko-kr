---
title: XML 생성 (XQuery) | Microsoft Docs
description: 직접 및 계산 된 생성자를 사용 하 여 XQuery에서 XML 구조를 생성 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- white space [XQuery]
- computed constructor
- construct XML structures [XQuery]
- constructors [XQuery]
- prolog
- direct constructor [SQL Server]
- XML [SQL Server], construction
- XQuery, XML construction
ms.assetid: a6330b74-4e52-42a4-91ca-3f440b3223cf
author: rothja
ms.author: jroth
ms.openlocfilehash: 16bffa4040e1a5068f83e9f68da981ed4aa0d7f1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730731"
---
# <a name="xml-construction-xquery"></a>XML 생성(XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  XQuery에서는 **직접** 및 **계산** 된 생성자를 사용 하 여 쿼리 내에서 XML 구조를 생성할 수 있습니다.  
  
> [!NOTE]  
>  **직접** 생성자와 **계산** 된 생성자 간에는 차이가 없습니다.  
  
## <a name="using-direct-constructors"></a>직접 생성자 사용  
 직접 생성자를 사용할 경우 XML을 생성할 때 XML 유형 구문을 지정합니다. 다음 예에서는 직접 생성자를 사용하여 XML을 생성하는 방법을 보여 줍니다.  
  
### <a name="constructing-elements"></a>요소 생성  
 XML 표기를 사용할 때 요소를 생성할 수 있습니다. 다음 예제에서는 직접 요소 생성자 식을 사용 하 고 요소를 만듭니다 \<ProductModel> . 생성된 요소에는 3개의 자식 요소가 있습니다.  
  
-   텍스트 노드  
  
-   및 라는 두 개의 요소 노드 \<Summary> \<Features>  
  
    -   요소에는 \<Summary> 값이 "Some description" 인 텍스트 노드 자식이 하나 있습니다.  
  
    -   요소에는 \<Features> 세 개의 요소 노드 자식,, 및가 있습니다 \<Color> \<Weight> \<Warranty> . 이러한 노드마다 텍스트 노드 자식이 한 개씩 있으며 값은 각각 Red, 25, 2 years parts and labor입니다.  
  
```sql
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
<Features>  
  <Color>Red</Color>  
  <Weight>25</Weight>  
  <Warranty>2 years parts and labor</Warranty>  
</Features></ProductModel>')  
  
```  
  
 결과 XML은 다음과 같습니다.  
  
```xml
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
  <Features>  
    <Color>Red</Color>  
    <Weight>25</Weight>  
    <Warranty>2 years parts and labor</Warranty>  
  </Features>  
</ProductModel>  
```  
  
 이 예와 같이 상수 식에서 요소를 생성하는 것도 유용하지만 XQuery 언어 기능의 진정한 강점은 데이터베이스에서 동적으로 데이터를 추출하는 XML을 생성하는 기능입니다. 중괄호를 사용하여 쿼리 식을 지정할 수 있습니다. 결과 XML에서 식이 해당 값으로 바뀝니다. 예를 들어 다음 쿼리는 `NewRoot` 하나의 자식 요소 (<>)를 사용 하 여 <> 요소를 생성 `e` 합니다. 요소 <>의 값은 중괄호 `e` ("{...}") 안에 경로 식을 지정 하 여 계산 됩니다.  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
SELECT @x.query('<NewRoot><e> { /root } </e></NewRoot>');  
```  
  
 중괄호는 컨텍스트 전환 토큰으로 사용되며 XML 생성에서 쿼리 계산으로 쿼리를 전환합니다. 이 경우 중괄호 안의 XQuery 경로 식 `/root`가 계산되어 결과로 대체됩니다.  
  
 다음은 결과입니다.  
  
```xml
<NewRoot>  
  <e>  
    <root>5</root>  
  </e>  
</NewRoot>  
```  
  
 다음 쿼리는 이전 쿼리와 비슷합니다. 그러나 중괄호 안에 있는 식에서는 **data ()** 함수를 지정 하 여 <> 요소의 원자성 값을 검색 하 `root` 고 생성 된 요소인 <>에 할당 합니다 `e` .  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
                           <NewRoot>  
                             <e> { data(/root) } </e>  
                           </NewRoot>' ));  
SELECT @y;  
```  
  
 다음은 결과입니다.  
  
```xml
<NewRoot>  
  <e>5</e>  
</NewRoot>  
```  
  
 컨텍스트 전환 토큰 대신 중괄호를 텍스트 일부로 사용하려면 다음 예와 같이 중괄호를 "}}" 또는 "{{"로 이스케이프할 수 있습니다.  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
<NewRoot> Hello, I can use {{ and  }} as part of my text</NewRoot>'));  
SELECT @y;  
```  
  
 다음은 결과입니다.  
  
```xml
<NewRoot> Hello, I can use { and  } as part of my text</NewRoot>  
```  
  
 다음 쿼리는 직접 요소 생성자를 사용하여 요소를 생성하는 또 다른 예입니다. 또한 <> 요소의 값은 중괄호 `FirstLocation` 에서 식을 실행 하 여 가져옵니다. 쿼리 식은 Production.ProductModel 테이블의 Instructions 열에서 첫 번째 업무 센터 위치의 제조 단계를 반환합니다.  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation>  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 다음은 결과입니다.  
  
```xml
<FirstLocation>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Attach <AWMI:tool>Trim Jig TJ-26</AWMI:tool> to the upper and lower right corners of the aluminum sheet.   
  </AWMI:step>  
   ...  
</FirstLocation>  
```  
  
#### <a name="element-content-in-xml-construction"></a>XML 생성의 요소 내용  
 다음 예에서는 직접 요소 생성자를 사용하여 요소 내용을 생성할 경우 식의 동작을 보여 줍니다. 다음 예에서는 직접 요소 생성자가 식 하나를 지정합니다. 이 식에서는 결과 XML에 텍스트 노드 하나가 생성됩니다.  
  
```sql
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { for $i in /root[1]/step  
    return string($i)  
 }  
</result>');  
  
```  
  
 결과에서와 같이 인접한 원자성 값 사이에 공백이 추가되고 식 계산 결과로 생성된 원자성 값 시퀀스가 텍스트 노드에 추가됩니다. 생성된 요소에는 자식 요소 한 개가 있습니다. 이 노드는 결과에 표시된 값을 포함하는 텍스트 노드입니다.  
  
```xml
<result>This is step 1 This is step 2 This is step 3</result>  
```  
  
 하나의 식 대신 텍스트 노드 3개를 생성하는 별도의 식 3개를 지정할 경우 결과 XML에서는 인접한 텍스트 노드가 연결을 통해 텍스트 노드 하나로 병합됩니다.  
  
```sql
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { string(/root[1]/step[1]) }  
 { string(/root[1]/step[2]) }  
 { string(/root[1]/step[3]) }  
</result>');  
```  
  
 생성된 요소 노드에는 자식 한 개가 있습니다. 이 노드는 결과에 표시된 값을 포함하는 텍스트 노드입니다.  
  
```xml
<result>This is step 1This is step 2This is step 3</result>  
```  
  
### <a name="constructing-attributes"></a>특성 생성  
 직접 요소 생성자를 사용하여 요소를 생성할 때 이 예에서와 같이 XML 유형 구문을 사용하여 요소의 특성을 지정할 수도 있습니다.  
  
```sql
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
</ProductModel>')  
```  
  
 결과 XML은 다음과 같습니다.  
  
```xml
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
</ProductModel>  
```  
  
 생성 된 요소 <`ProductModel`>에는 제품 Modelid 특성과 이러한 자식 노드가 있습니다.  
  
-   텍스트 노드 `This is product model catalog description.`  
  
-   요소 노드 <`Summary`>입니다. 이 노드에는 하나의 텍스트 노드 자식 `Some description`이 있습니다.  
  
 특성을 생성할 때 중괄호 안에 식을 사용하여 값을 지정할 수 있습니다. 이 경우 식의 결과가 특성 값으로 반환됩니다.  
  
 다음 예에서는 **data ()** 함수를 반드시 입력 해야 하는 것은 아닙니다. 식 값을 특성에 할당 하므로 **데이터 ()** 가 암시적으로 적용 되어 지정 된 식의 형식화 된 값을 검색 합니다.  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('<NewRoot attr="{ data(/root) }" ></NewRoot>'));  
SELECT @y;  
```  
  
 다음은 결과입니다.  
  
```xml
<NewRoot attr="5" />  
```  
  
 다음은 LocationID 및 SetupHrs 특성 생성을 위해 식이 지정되는 또 다른 예입니다. Instruction 열의 XML에 대해 이러한 식이 계산됩니다. 식의 형식화된 값이 특성에 할당됩니다.  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation   
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7;  
```  
  
 다음은 결과의 일부입니다.  
  
```xml
<FirstLocation LocationID="10" SetupHours="0.5" >  
  <AWMI:step ...   
  </AWMI:step>  
  ...  
</FirstLocation>  
```  
  
#### <a name="implementation-limitations"></a>구현 시 제한 사항  
 제한 사항은 다음과 같습니다.  
  
-   다중 또는 혼합(문자열 및 XQuery 식) 특성 식은 지원되지 않습니다. 예를 들어 다음 쿼리에서와 같이 `Item`이 상수이고 쿼리 식을 계산하여 값 `5`를 구하는 XML을 생성합니다.  
  
    ```xml
    <a attr="Item 5" />  
    ```  
  
     상수 문자열을 식({/x})과 함께 사용하지만 지원되지 않으므로 다음 쿼리에서는 오류를 반환합니다.  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="Item {/x}"/>' )   
    ```  
  
     이 경우 다음과 같은 옵션을 사용할 수 있습니다.  
  
    -   원자성 값 두 개를 연결하여 특성 값을 만듭니다. 이 원자성 값은 원자성 값 사이에 공백이 있는 특성 값으로 직렬화됩니다.  
  
        ```sql
        SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
        ```  
  
         다음은 결과입니다.  
  
        ```xml
        <a attr="Item 5" />  
        ```  
  
    -   [Concat 함수](../xquery/functions-on-string-values-concat.md) 를 사용 하 여 두 문자열 인수를 결과 특성 값에 연결 합니다.  
  
        ```sql
        SELECT @x.query( '<a attr="{concat(''Item'', /x[1])}"/>' )   
        ```  
  
         이 경우 두 문자열 값 사이에 공백이 추가되지 않습니다. 두 값 사이에 공백을 추가하려면 명시적으로 공백을 제공해야 합니다.  
  
         다음은 결과입니다.  
  
        ```xml
        <a attr="Item5" />  
        ```  
  
-   여러 개의 식을 특성 값으로 사용할 수 없습니다. 예를 들어 다음 쿼리는 오류를 반환합니다.  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="{/x}{/x}"/>' )  
    ```  
  
-   다른 유형의 시퀀스는 지원되지 않습니다. 다음 예와 같이 다른 유형의 시퀀스를 특성 값으로 할당하면 오류가 반환됩니다. 이 예제에서는 유형이 다른 시퀀스, 문자열 "Item" 및> <요소를 `x` 특성 값으로 지정 합니다.  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    select @x.query( '<a attr="{''Item'', /x }" />')  
    ```  
  
     **Data ()** 함수를 적용 하는 경우 쿼리는 문자열과 연결 된 식의 원자성 값을 검색 하기 때문에 작동 합니다 `/x` . 다음은 원자성 값의 시퀀스입니다.  
  
    ```sql
    SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
    ```  
  
     다음은 결과입니다.  
  
    ```xml
    <a attr="Item 5" />  
    ```  
  
-   특성 노드 순서는 정적 유형 확인 중이 아니라 직렬화 중에 적용됩니다. 예를 들어 다음 쿼리는 특성 노드가 아닌 노드 뒤에 특성을 추가하려고 시도하기 때문에 실패합니다.  
  
    ```sql
    select convert(xml, '').query('  
    element x { attribute att { "pass" }, element y { "Element text" }, attribute att2 { "fail" } }  
    ')  
    go  
    ```  
  
     위의 쿼리는 다음 오류를 반환합니다.  
  
    ```  
    XML well-formedness check: Attribute cannot appear outside of element declaration. Rewrite your XQuery so it returns well-formed XML.  
    ```  
  
### <a name="adding-namespaces"></a>네임스페이스 추가  
 직접 생성자를 사용하여 XML을 생성하면 네임스페이스 접두사를 사용하여 생성된 요소와 특성 이름을 한정할 수 있습니다. 다음과 같은 방법으로 네임스페이스에 접두사를 바인딩할 수 있습니다.  
  
-   네임스페이스 선언 특성 사용  
  
-   WITH XMLNAMESPACES 절 사용  
  
-   XQuery 프롤로그에서 바인딩  
  
#### <a name="using-a-namespace-declaration-attribute-to-add-namespaces"></a>네임스페이스 선언 특성을 사용하여 네임스페이스 추가  
 다음 예제에서는 <> 요소를 생성 하는 데 네임 스페이스 선언 특성을 사용 하 여 `a` 기본 네임 스페이스를 선언 합니다. 자식 요소의 생성은 `b` 부모 요소에 선언 된 기본 네임 스페이스의 선언을 실행 취소 <> 합니다.  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <a xmlns="a">  
    <b xmlns=""/>  
  </a>' )   
```  
  
 다음은 결과입니다.  
  
```xml
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
 네임스페이스에 접두사를 할당할 수 있습니다. 접두사는 요소 <> 생성 시 지정 됩니다 `a` .  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b/>  
  </x:a>' )  
```  
  
 다음은 결과입니다.  
  
```xml
<x:a xmlns:x="a">  
  <b />  
</x:a>  
```  
  
 XML 생성에서 기본 네임스페이스를 선언하지 않아도 되지만 네임스페이스 접두사는 선언해야 합니다. 다음 쿼리는 <> 요소 생성에 지정 된 대로 접두사를 선언 취소할 수 없기 때문에 오류를 반환 합니다 `b` .  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b xmlns:x=""/>  
  </x:a>' )  
```  
  
 새로 생성된 네임스페이스는 쿼리 안에서 사용할 수 있습니다. 예를 들어 다음 쿼리는 요소를 생성 하 고> <하 여 네임 스페이스를 선언 `FirstLocation` 하 고 LocationID 및 SetupHrs 특성 값에 대 한 식에 접두사를 지정 합니다.  
  
```sql
SELECT Instructions.query('  
        <FirstLocation xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 이 방법으로 네임스페이스 접두사를 새로 만들면 이 접두사에 대한 기존의 네임스페이스 선언이 무시됩니다. 예를 들어 `AWMI="https://someURI"` 쿼리 프롤로그에 있는 네임 스페이스 선언은 <> 요소의 네임 스페이스 선언에 의해 재정의 됩니다 `FirstLocation` .  
  
```sql
SELECT Instructions.query('  
declare namespace AWMI="https://someURI";  
        <FirstLocation xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
#### <a name="using-a-prolog-to-add-namespaces"></a>프롤로그를 사용하여 네임스페이스 추가  
 이 예에서는 생성된 XML에 네임스페이스를 추가하는 방법을 보여 줍니다. 기본 네임스페이스는 쿼리 프롤로그에 선언됩니다.  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
           declare default element namespace "a";  
            <a><b xmlns=""/></a>' )  
```  
  
 요소 <`b`>를 생성할 때 네임 스페이스 선언 특성은 빈 문자열을 값으로 사용 하 여 지정 됩니다. 그러면 부모에 선언된 기본 네임스페이스를 선언하지 않습니다.  
  

다음은 결과입니다.  

```xml
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
### <a name="xml-construction-and-white-space-handling"></a>XML 생성 및 공백 처리  
 XML 생성의 요소 내용은 공백 문자를 포함할 수 있습니다. 이러한 문자는 다음 방법으로 처리됩니다.  
  
-   네임 스페이스 Uri의 공백 문자는 XSD 형식 **anyURI**으로 처리 됩니다. 특히 처리 방법은 다음과 같습니다.  
  
    -   처음과 끝에 있는 공백 문자는 잘립니다.  
  
    -   내부 공백 문자 값은 공백 한 개로 줄어듭니다.  
  
-   특성 내용에 있는 줄 바꿈 문자는 공백으로 바뀝니다. 다른 모든 공백 문자는 그대로 유지됩니다.  
  
-   요소 안의 공백은 유지됩니다.  
  
 다음 예에서는 XML 생성의 공백 처리를 보여 줍니다.  
  
```sql
-- line feed is repaced by space.  
declare @x xml  
set @x=''  
select @x.query('  
  
declare namespace myNS="   https://       
 abc/  
xyz  
  
";  
<test attr="    my   
test   attr   
value    " >  
  
<a>  
  
This     is  a  
  
test  
  
</a>  
</test>  
') as XML_Result  
  
```  
  
 다음은 결과입니다.  
  
```xml
-- result  
<test attr="<test attr="    my test   attr  value    "><a>  
  
This     is  a  
  
test  
  
</a></test>  
"><a>  
  
This     is  a  
  
test  
  
</a></test>  
```  
  
### <a name="other-direct-xml-constructors"></a>그 밖의 직접 XML 생성자  
 처리 명령과 XML 주석에 대한 생성자는 해당 XML 구문에서와 같은 구문을 사용합니다. 텍스트 노드의 계산된 생성자도 지원되지만 이는 기본적으로 XML DML에 사용되어 텍스트 노드를 생성합니다.  
  
 **참고** 명시적 텍스트 노드 생성자를 사용 하는 예제는 [insert &#40;XML DML&#41;](../t-sql/xml/insert-xml-dml.md)의 특정 예제를 참조 하십시오.  
  
 다음 쿼리에서 생성된 XML에는 요소, 특성 두 개, 주석 및 처리 명령이 포함됩니다. 시퀀스를 생성 하기 때문에 <> 하기 전에 쉼표가 사용 됩니다 `FirstLocation` .  
  
```sql
SELECT Instructions.query('  
  declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   <?myProcessingInstr abc="value" ?>,   
   <FirstLocation   
        WorkCtrID = "{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
        SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
       <!-- some comment -->  
       <?myPI some processing instructions ?>  
       { (/AWMI:root/AWMI:Location[1]/AWMI:step) }  
    </FirstLocation>   
') as Result   
FROM Production.ProductModel  
where ProductModelID=7;  
  
```  
  
 다음은 결과의 일부입니다.  
  
```xml
<?myProcessingInstr abc="value" ?>  
<FirstLocation WorkCtrID="10" SetupHrs="0.5">  
  <!-- some comment -->  
  <?myPI some processing instructions ?>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">I  
  nsert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
    ...  
</FirstLocation>  
  
```  
  
## <a name="using-computed-constructors"></a>계산된 생성자 사용  
 . 이 경우 생성할 노드 유형을 나타내는 키워드를 지정합니다. 다음 키워드만 지원됩니다.  
  
-   element  
  
-   특성  
  
-   text  
  
 요소 및 특성 노드의 경우 이러한 키워드 다음에 노드 이름과 식이 중괄호 안에 포함되어 해당 노드의 내용을 생성합니다. 다음 예에서는 이 XML을 생성합니다.  
  
```xml
<root>  
  <ProductModel PID="5">Some text <summary>Some Summary</summary></ProductModel>  
</root>  
```  
  
 다음은 계산된 생성자를 사용하여 XML을 생성하는 쿼리입니다.  
  
```sql
declare @x xml  
set @x=''  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { 5 },  
text{"Some text "},  
    element summary { "Some Summary" }  
 }  
               } ')  
  
```  
  
 노드 내용을 생성하는 식은 쿼리 식을 지정할 수 있습니다.  
  
```sql
declare @x xml  
set @x='<a attr="5"><b>some summary</b></a>'  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { /a/@attr },  
text{"Some text "},  
    element summary { /a/b }  
 }  
               } ')  
```  
  
 XQuery 사양에 정의된 대로 계산된 요소 및 특성 생성자를 사용하면 노드 이름을 계산할 수 있습니다. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 직접 생성자를 사용할 경우 요소 및 특성과 같은 노드 이름을 상수 리터럴로 지정해야 합니다. 따라서 요소와 특성에서는 직접 생성자와 계산된 생성자 간에 차이가 없습니다.  
  
 다음 예에서는 생성 된 노드의 내용을 제품 모델 테이블에 있는 **xml** 데이터 형식의 명령 열에 저장 된 xml 제조 지침에서 가져옵니다.  
  
```sql
SELECT Instructions.query('  
  declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   element FirstLocation   
     {  
        attribute LocationID { (/AWMI:root/AWMI:Location[1]/@LocationID)[1] },  
        element   AllTheSteps { /AWMI:root/AWMI:Location[1]/AWMI:step }  
     }  
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 다음은 결과의 일부입니다.  
  
```xml
<FirstLocation LocationID="10">  
  <AllTheSteps>  
    <AWMI:step> ... </AWMI:step>  
    <AWMI:step> ... </AWMI:step>  
    ...  
  </AllTheSteps>  
</FirstLocation>    
```  
  
## <a name="additional-implementation-limitations"></a>구현 시 추가 제한 사항  
 계산된 특성 생성자를 사용하여 새 네임스페이스를 선언할 수는 없습니다. 또한 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서는 다음의 계산된 생성자가 지원되지 않습니다.  
  
-   계산된 문서 노드 생성자  
  
-   계산된 처리 명령 생성자  
  
-   계산된 주석 생성자  
  
## <a name="see-also"></a>참고 항목  
 [XQuery 식](../xquery/xquery-expressions.md)  
  
  
