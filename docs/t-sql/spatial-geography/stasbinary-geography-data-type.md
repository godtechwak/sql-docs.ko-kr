---
description: STAsBinary(geography 데이터 형식)
title: STAsBinary(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STAsBinary_TSQL
- STAsBinary (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STAsBinary method
ms.assetid: 99602a62-265d-4aa4-a8dc-92992ca55ba4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7ae9c800cffd7df80ba8447c2e16de745a0009bc
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88359449"
---
# <a name="stasbinary-geography-data-type"></a>STAsBinary(geography 데이터 형식)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  **geography** 인스턴스의 OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현을 반환합니다.  
  
 이 **geography** 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STAsBinary ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **varbinary(max)**  
  
 CLR 반환 형식: **SqlBytes**  
  
## <a name="remarks"></a>설명  
 **geography** 인스턴스의 OGC 형식은 [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)을 호출하여 확인할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `STAsBinary()`를 사용하여 텍스트에서 `LineString``geography` 인스턴스((-122.360, 47.656) - (-122.343, 47.656))를 만듭니다. 그런 다음 WKB로 결과를 반환합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING( -122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsBinary();  
```  
  
## <a name="see-also"></a>참고 항목  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
