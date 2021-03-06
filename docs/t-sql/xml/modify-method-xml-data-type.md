---
description: modify() 메서드(xml 데이터 형식)
title: modify() 메서드(xml 데이터 형식)
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- modify() method
- modify method
ms.assetid: 52430735-51f4-46d1-a308-9aecf8648fda
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8f374a9a935a0bc0e4c015fb3eff4e87a2be4e20
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91117170"
---
# <a name="modify-method-xml-data-type"></a>modify() 메서드(xml 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  XML 문서의 내용을 수정합니다. 이 메서드를 사용하면 **xml** 형식의 변수 또는 열의 콘텐츠를 수정할 수 있습니다. 이 메서드는 XML DML 문을 사용하여 XML 데이터에서 노드를 삽입, 업데이트 또는 삭제합니다. UPDATE 문의 SET 절에서는 **xml** 데이터 형식의 **modify()** 메서드만 사용할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
modify (XML_DML)  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 XML_DML  
 XML DML(데이터 조작 언어)에 있는 문자열입니다. XML 문서는 이 식에 따라 업데이트됩니다.  
  
> [!NOTE]  
>  Null 값에 **modify()** 메서드를 호출하거나 결과 값이 Null이면 오류가 반환됩니다.  
  
## <a name="examples"></a>예제  
 **modify()** 메서드가 XML DML(데이터 조작 언어)의 문자열이 필요하므로 **modify()** 의 예제는 XML DML 문을 설명하는 항목에 포함됩니다. 이러한 예제의 경우 [삽입&#40;XML DML&#41;](../../t-sql/xml/insert-xml-dml.md), [삭제&#40;XML DML&#41;](../../t-sql/xml/delete-xml-dml.md) 및 [값 바꾸기&#40;XML DML&#41;](../../t-sql/xml/replace-value-of-xml-dml.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 데이터 인스턴스 만들기](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [xml 데이터 형식 메서드](../../t-sql/xml/xml-data-type-methods.md)   
 [XML DML&#40;XML 데이터 수정 언어&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
