---
title: 와일드카드 문자를 사용하여 열 지정(SQLXML) | Microsoft Docs
description: 와일드카드 문자로 지정된 열 이름이 XQuery의 결과에 미치는 영향에 대해 알아봅니다.
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: d9551df1-5bb4-4c0b-880a-5bb049834884
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: 915bd2824f6e3a706587769413c0f116df859f06
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96125022"
---
# <a name="columns-with-a-name-specified-as-a-wildcard-character"></a>이름이 와일드카드 문자로 지정된 열

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

지정된 열 이름이 와일드카드 문자(\*)이면 열 이름이 지정되지 않은 경우처럼 열 내용이 삽입됩니다. 이 열이 비-**xml** 유형 열이면 다음 예에서와 같이 열 내용이 텍스트 노드로 삽입됩니다.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT E.BusinessEntityID "@EmpID",   
       FirstName "*",   
       MiddleName "*",   
       LastName "*"  
FROM   HumanResources.Employee AS E  
  INNER JOIN Person.Person AS P  
    ON E.BusinessEntityID = P.BusinessEntityID  
WHERE E.BusinessEntityID=1  
FOR XML PATH;  
```  
  
 다음은 결과입니다.  

```xml
<row EmpID="1">KenJSánchez</row>
```

 열이 **xml** 유형일 경우 해당 XML 트리가 삽입됩니다. 예를 들어 다음 쿼리는 Instructions 열에 대해 XQuery에서 반환한 XML이 포함된 열 이름에 "*"를 지정합니다.  
  
```sql
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
                /MI:root/MI:Location   
              ') as "*"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;   
```  
  
 다음은 결과입니다. XQuery에서 반환한 XML이 래핑 요소 없이 삽입됩니다.  

```xml
<row>
  <ProductModelID>7</ProductModelID>
  <Name>HL Touring Frame</Name>
  <MI:Location LocationID="10">...</MI:Location>
  <MI:Location LocationID="20">...</MI:Location>
  ...
</row>
```

## <a name="see-also"></a>참고 항목  
 [FOR XML에서 PATH 모드 사용](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
