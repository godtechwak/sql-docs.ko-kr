---
description: STInteriorRingN(geometry 데이터 형식)
title: STInteriorRingN(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STInteriorRingN_TSQL
- STInteriorRingN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STInteriorRingN (geometry Data Type)
ms.assetid: 47310f9f-2cdb-41e0-a6da-7c3cfbf139ac
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 52d1f15affc8f253303bb636c4b94f280e8a3319
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88479276"
---
# <a name="stinteriorringn-geometry-data-type"></a>STInteriorRingN(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**Polygongeometry** 인스턴스의 지정된 내부 링을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STInteriorRingN ( expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *expression*  
 1과 **geometry** 인스턴스에 있는 내부 링 개수 사이의 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 OGC(Open Geospatial Consortium) 형식: **LineString**  
  
## <a name="remarks"></a>설명  
 이 메서드는 **geometry** 인스턴스가 다각형이 아니면 **Null** 을 반환합니다. 또한 이 메서드는 식이 링 개수보다 크면 **ArgumentOutOfRangeException** 을 throw합니다. 링 개수는 `STNumInteriorRing``()`를 사용하여 반환할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `Polygon` 인스턴스를 만들고 `STInteriorRingN()`을 사용하여 다각형의 내부 링을 **LineString** 으로 반환합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POLYGON((0 0, 3 0, 3 3, 0 3, 0 0),(2 2, 2 1, 1 1, 1 2, 2 2))', 0);  
SELECT @g.STInteriorRingN(1).ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

