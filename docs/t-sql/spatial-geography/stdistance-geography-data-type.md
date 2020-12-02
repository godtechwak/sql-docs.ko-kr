---
description: STDistance(geography 데이터 형식)
title: STDistance(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STDistance_TSQL
- STDistance (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STDistance method
ms.assetid: 063d8722-e019-4d3d-8fcf-dbf5325823e7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a20279a70d2e68e1cb4b34eb36ffe7de633518a4
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88416999"
---
# <a name="stdistance-geography-data-type"></a>STDistance(geography 데이터 형식)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

  **geography** 인스턴스의 점 및 다른 **geography** 인스턴스의 점 간 최단 길이를 반환합니다.  
  
> [!NOTE]  
>  `STDistance()`는 두 geography 형식 사이의 최단 **LineString** 을 반환합니다. 이 길이는 측지 거리와 거의 같습니다. 일반 지구 모델에서 `STDistance()`와 정확한 측지 거리 간의 편차는 .25%를 넘지 않으므로 geodesic 형식에서 길이와 거리의 미세한 차이로 인한 혼동이 발생하지 않습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STDistance ( other_geography )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *other_geography*  
 STDistance()를 호출할 인스턴스 간 거리를 측정할 다른 **geography** 인스턴스입니다. *other_geography* 가 빈 집합이면 STDistance()는 null을 반환합니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **float**  
  
 CLR 반환 형식: **SqlDouble**  
  
## <a name="remarks"></a>설명  
 결과는 공간 데이터의 [SRID&#40;Spatial Reference Identifier&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)에서 정의한 측정 단위로 표현됩니다.
STDistance()는 **geography** 인스턴스의 SRID(Spatial Reference ID)가 일치하지 않으면 항상 *null* 을 반환합니다.  
  
> [!NOTE]  
>  면적 또는 거리를 계산하는 **geography** 데이터 형식에 대한 메서드는 메서드에서 사용되는 인스턴스의 SRID에 따라 다른 결과를 반환합니다. SRID에 대한 자세한 내용은 [Spatial Reference Identifiers&#40;SRIDs&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)를 참조하세요.  
  
## <a name="examples"></a>예제  
 다음 예에서는 두 **geography** 인스턴스 간의 거리를 찾습니다.  
  
```  
DECLARE @g geography;  
DECLARE @h geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SET @h = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.STDistance(@h);  
```  
  
## <a name="see-also"></a>참고 항목  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
