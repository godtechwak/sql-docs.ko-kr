---
description: STAsText(geography 데이터 형식)
title: STAsText(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STAsText (geography Data Type)
- STAsText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STAsText method
ms.assetid: d3d2635d-ca6c-4205-9d6c-eb939ee314fd
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: f89f2c2889d880388f74b563abc9aefe1eb28c82
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88422317"
---
# <a name="stastext-geography-data-type"></a>STAsText(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **geography** 인스턴스의 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현을 반환합니다. 이 텍스트에는 인스턴스에서 얻어진 Z(높이) 값 또는 M(측정값) 값이 포함되지 않습니다.  
  
 이 **geography** 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STAsText ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **nvarchar(max)**  
  
 CLR 반환 형식: **SqlChars**  
  
## <a name="remarks"></a>설명  
 **geography** 인스턴스의 OGC 형식은 [STGeometryType()](../../t-sql/spatial-geography/stgeometrytype-geography-data-type.md)을 호출하여 확인할 수 있습니다.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서는 서버에서 반환될 수 있는 결과 집합이 **FullGlobe** 인스턴스까지 확장되었습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `STAsText()`를 사용하여 텍스트에서 `LineString``geography` 인스턴스((-122.360, 47.656) - (-122.343, 47.656))를 만듭니다. 그런 다음 텍스트로 결과를 반환합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>참고 항목  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
