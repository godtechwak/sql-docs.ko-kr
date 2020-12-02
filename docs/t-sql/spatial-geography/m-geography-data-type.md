---
description: M(geography 데이터 형식)
title: M(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- M (geography Data Type)
- M_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- M method
ms.assetid: cdba04f0-4e17-48f6-bafb-b1f918c5a501
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 77a79972671854e7e8538de7b943545955f61e89
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88422427"
---
# <a name="m-geography-data-type"></a>M(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **geography** 인스턴스의 **M**(측정값) 값을 반환합니다. 측정값의 의미 체계는 사용자가 정의하지만 일반적으로 linestring을 따라 측정한 거리를 설명합니다. 예를 들어 측정값을 사용하여 길의 이정표를 계속 추적할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.M  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식: **float**  
  
 CLR 유형: **SqlDouble**  
  
## <a name="remarks"></a>설명  
 **geography** 인스턴스가 **지점** 이 아닌 경우 및 해당 값이 설정되지 않은 모든 **Point** 인스턴스의 경우 이 속성의 값은 Null입니다.  
  
 이 속성은 읽기 전용입니다.  
  
 M 값은 어떠한 라이브러리 계산에도 사용되지 않으며 어떠한 라이브러리 계산을 통해서도 얻을 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Z(높이) 값과 M(측정값) 값이 있는 `Point` 인스턴스를 만들고 `M`을 사용하여 인스턴스의 `M` 값을 인출합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100 10.3 12)', 4326);  
SELECT @g.M;  
```  
  
## <a name="see-also"></a>관련 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [Z&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/z-geography-data-type.md)  
  
  
