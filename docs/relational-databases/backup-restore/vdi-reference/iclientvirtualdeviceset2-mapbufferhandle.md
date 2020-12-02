---
title: IClientVirtualDeviceSet2::MapBufferHandle
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IClientVirtualDeviceSet2::MapBufferHandle 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 70f6d117fd7a0349f2da2e03ff2603eaf55898fe
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128965"
---
# <a name="iclientvirtualdeviceset2mapbufferhandle-vdi"></a>IClientVirtualDeviceSet2::MapBufferHandle (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

**MapBufferHandle** 함수는 일부 다른 프로세스에서 가져온 버퍼 핸들에서 유효한 버퍼 주소를 가져오는 데 사용됩니다.

## <a name="syntax"></a>구문

```c
HRESULT IClientVirtualDeviceSet2::MapBufferHandle (
   DWORD      dwBuffer,
   BYTE**      ppBuffer
);
```

## <a name="parameters"></a>매개 변수

*dwBuffer* IClientVirtualDeviceSet2::GetBufferHandle에서 반환되는 핸들입니다.

*ppBuffer* 현재 프로세스에서 유효한 버퍼의 주소입니다.

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 함수가 성공했습니다. |
| VD_E_PROTOCOL | 가상 디바이스 세트가 현재 열려 있지 않습니다. |
| VD_E_INVALID | ppBuffer가 잘못된 핸들입니다. |

## <a name="remarks"></a>설명

핸들을 제대로 전달하기 위해 주의해야 합니다. 핸들은 단일 가상 디바이스 세트에 대해 로컬입니다. 핸들을 공유하는 파트너 프로세스는 버퍼 핸들이 원래 버퍼를 가져온 가상 디바이스 세트의 범위 내에서만 사용되는지 확인해야 합니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.