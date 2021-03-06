---
description: 보기 개체(ADOX)
title: View 개체 (ADOX) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- View
helpviewer_keywords:
- View object [ADOX]
ms.assetid: 653421ce-7b94-43d0-9bc6-4900f8f2af45
author: rothja
ms.author: jroth
ms.openlocfilehash: eefc7c259d12f20ada1676a6518fa357719abe63
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88982994"
---
# <a name="view-object-adox"></a>보기 개체(ADOX)
레코드 또는 가상 테이블의 필터링 된 집합을 나타냅니다. ADO [명령](../ado-api/command-object-ado.md) 개체와 함께 사용 하는 경우 **뷰** 개체를 사용 하 여 뷰를 추가, 삭제 또는 수정할 수 있습니다.  
  
## <a name="remarks"></a>설명  
 뷰는 다른 데이터베이스 테이블 또는 뷰에서 만든 가상 테이블입니다. **뷰** 개체를 사용 하면 공급자의 "create View" 구문을 알거나 사용 하지 않고도 뷰를 만들 수 있습니다.  
  
 **View** 개체의 속성을 사용 하 여 다음을 수행할 수 있습니다.  
  
-   [Name](./name-property-adox.md) 속성을 사용 하 여 뷰를 식별 합니다.  
  
-   [명령](./command-property-adox.md) 속성을 사용 하 여 뷰를 추가, 삭제 또는 수정 하는 데 사용할 수 있는 ADO **명령** 개체를 지정 합니다.  
  
-   [DateCreated](./datecreated-property-adox.md) 및 [DateModified](./datemodified-property-adox.md) 속성을 사용 하 여 날짜 정보를 반환 합니다.  
  
 이 섹션에는 다음 항목이 포함 되어 있습니다.  
  
-   [보기 개체 속성, 메서드 및 이벤트](./view-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>참고 항목  
 [Views 및 Fields 컬렉션 예제 (VB)](./views-and-fields-collections-example-vb.md)   
 [Views Append 메서드 예제 (VB)](./views-append-method-example-vb.md)   
 [Views 컬렉션, CommandText 속성 예제 (VB)](./views-collection-commandtext-property-example-vb.md)   
 [Views Delete 메서드 예제 (VB)](./views-delete-method-example-vb.md)   
 [Views 컬렉션(ADOX)](./views-collection-adox.md)