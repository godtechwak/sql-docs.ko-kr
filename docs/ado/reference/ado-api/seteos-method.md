---
description: SetEOS 메서드
title: SetEOS 메서드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SetEOS
- _Stream::SetEOS
helpviewer_keywords:
- SetEOS method [ADO]
ms.assetid: 707c18ca-6a56-4970-bbd6-ae1fb86a0b8a
author: rothja
ms.author: jroth
ms.openlocfilehash: 3ebf47bdae6a879a3afe699be36081eb136b700e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989134"
---
# <a name="seteos-method"></a>SetEOS 메서드
스트림의 끝 위치를 설정 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
Stream.SetEOS  
```  
  
## <a name="remarks"></a>설명  
 **SetEOS** 는 현재 [위치](./position-property-ado.md) 를 스트림의 끝으로 만들어 [EOS](./eos-property.md) 속성의 값을 업데이트 합니다. 현재 위치 다음에 나오는 모든 바이트 또는 문자는 잘립니다.  
  
 [Write](./write-method.md), [WriteText](./writetext-method.md)및 [CopyTo](./copyto-method-ado.md) 는 기존 **스트림** 개체의 추가 값을 자르지 않으므로 **SetEOS**를 사용 하 여 새 스트림 끝 위치를 설정 하 여 이러한 바이트 또는 문자를 자를 수 있습니다.  
  
> [!CAUTION]
>  **Eos** 를 스트림의 실제 끝 앞의 위치로 설정 하면 새 **eos** 위치 이후의 모든 데이터가 손실 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [스트림 개체(ADO)](./stream-object-ado.md)