---
description: STArea(geography 데이터 형식)
title: STArea(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STArea (geography Data Type)
- STArea_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STArea method
ms.assetid: cfc0b0e0-7fde-431a-863f-d13f3b1b1bef
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: a8581700ea3145840684cce1e18e24c2f2e1cd3e
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88359739"
---
# <a name="starea-geography-data-type"></a>STArea(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geography** 인스턴스의 전체 표면을 반환합니다. STArea()의 결과는 **geography** 인스턴스의 Spatial Reference Identifier에 사용되는 측정 단위의 제곱입니다. 예를 들어 인스턴스의 SRID가 4326이면 STArea()는 제곱 미터로 결과를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STArea ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **float**  
  
CLR 반환 형식: **SqlDouble**  
  
## <a name="remarks"></a>설명  
STArea()는 **geography** 인스턴스가 0 및 1차원 도형만 포함하거나 비어 있으면 0을 반환합니다.  
  
> [!NOTE]  
>  메트릭 반환 값을 생성하는 **geography** 데이터 형식에 대한 메서드 결과는 메서드에서 사용되는 인스턴스의 SRID에 따라 달라집니다. SRID에 대한 자세한 내용은 [공간 참조 식별자 &#40;SRID&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)를 참조하세요.  
  
## <a name="examples"></a>예제  
다음 예에서는 `STArea()`를 사용하여 `Polygon geography` 인스턴스를 만들고 다각형의 영역을 계산합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POLYGON((-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326);  
SELECT @g.STArea();  
```  
  
## <a name="see-also"></a>참고 항목  
[Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
