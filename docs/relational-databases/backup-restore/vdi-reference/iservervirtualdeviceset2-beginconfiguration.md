---
title: IServerVirtualDeviceSet2::BeginConfiguration
titlesuffix: SQL Server VDI reference
description: 이 문서에서는 IServerVirtualDeviceSet2::BeginConfiguration 명령에 대한 참조를 제공합니다.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: d1a2bd52e923f64bac8b1865cee5e18aa2f6345e
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125352"
---
# <a name="iservervirtualdeviceset2beginconfiguration-vdi"></a>IServerVirtualDeviceSet2::BeginConfiguration (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

서버는 **BeginConfiguration** 함수를 호출하여 가상 디바이스 세트의 구성을 시작합니다.

## <a name="syntax"></a>구문

```c
HRESULT IServerVirtualDeviceSet2::BeginConfiguration (
   DWORD   dwFeatures,
   DWORD   dwAlignment,
   DWORD   dwBlockSize,
   DWORD   dwMaxTransferSize,
   DWORD   dwTimeout
);
```

## <a name="parameters"></a>매개 변수

*dwFeatures* 수정된 기능 마스크입니다. VDF_WriteMedia 및/또는 VDF_ReadMedia.

*dwAlignment* 최종 맞춤입니다. 0인 경우 기본값은 dwBlockSize입니다. dwBlockSize 이상, 64KB 미만인 2의 거듭제곱이어야 합니다.

*dwBlockSize* 최소 전송 단위(바이트)입니다. 512 이상, 64KB 미만인 2의 거듭제곱이어야 합니다.

*dwMaxTransferSize* 시도될 가장 큰 전송입니다. 64KB의 배수여야 합니다.

*dwTimeout* 주 클라이언트가 제공할 버퍼 영역의 선언을 완료할 때까지 대기하는 시간(밀리초)입니다.

## <a name="return-value"></a>Return Value

|Return Value | 설명 |
|---|---|
| NOERROR | 가상 디바이스 세트가 구성 가능 상태입니다. |
| VD_E_ABORT | SignalAbort가 호출되었습니다. |
| VD_E_PROTOCOL | 가상 디바이스 세트가 연결됨 상태가 아닙니다. |

## <a name="remarks"></a>설명

이 함수가 호출된 후에는 가상 디바이스 세트가 구성 가능 상태로 전환되며 이 상태에서 버퍼 레이아웃이 결정됩니다.
기본 구성이 설정되면(매개 변수별로) 가상 디바이스 세트의 수명 동안 이러한 값이 고정된 상태로 유지됩니다. 가상 디바이스 세트에 대한 맞춤 속성은 데이터 버퍼의 맞춤을 제어하는 데 사용됩니다. 이 값은 버퍼 단위로 재정의될 수 있는 최소 맞춤 값을 설정합니다.

## <a name="next-steps"></a>다음 단계

자세한 내용은 [SQL Server 가상 디바이스 인터페이스 참조 개요](reference-virtual-device-interface.md)를 참조하세요.