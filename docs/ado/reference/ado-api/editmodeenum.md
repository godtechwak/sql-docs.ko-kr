---
description: EditModeEnum
title: EditModeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EditModeEnum
helpviewer_keywords:
- EditModeEnum enumeration [ADO]
ms.assetid: 45d54b6e-db2c-4553-9fd0-528147d6da2f
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e10479aca06eab4a7aa5215f0016dd1f82eab1c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973854"
---
# <a name="editmodeenum"></a>EditModeEnum
레코드의 편집 상태를 지정 합니다.  
  
|상수|값|설명|  
|--------------|-----------|-----------------|  
|**adEditNone**|0|진행 중인 편집 작업이 없음을 나타냅니다.|  
|**adEditInProgress**|1|현재 레코드의 데이터가 수정 되었지만 저장 되지 않았음을 나타냅니다.|  
|**adEditAdd**|2|는 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) 메서드를 호출 했 고 복사 버퍼의 현재 레코드는 데이터베이스에 저장 되지 않은 새 레코드 임을 나타냅니다.|  
|**adEditDelete**|4|현재 레코드가 삭제 되었음을 나타냅니다.|  
  
## <a name="adowfc-equivalent"></a>ADO/WFC 동급  
 Package: **com.ms.wfc.data**  
  
|상수|  
|--------------|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
|AdoEnums|  
  
## <a name="applies-to"></a>적용 대상  
 [EditMode 속성](../../../ado/reference/ado-api/editmode-property.md)
