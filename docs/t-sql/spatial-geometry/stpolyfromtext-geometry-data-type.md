---
description: STPolyFromText(geometry 데이터 형식)
title: STPolyFromText(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPolyFromText_TSQL
- STPolyFromText (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPolyFromText (geometry Data Type)
ms.assetid: a7c1c9f0-1dd5-493b-b206-83bbfa33452b
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 0e2ce076523c0707c8764d9a21f38abdbf41e0a7
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88359719"
---
# <a name="stpolyfromtext-geometry-data-type"></a>STPolyFromText(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

인스턴스에서 얻어진 Z(높이) 값 및 M(측정값) 값을 사용하여 보강된 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 **geometry** 인스턴스를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STPolyFromText ( 'polygon_tagged_text' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *polygon_tagged_text*  
 반환하려는 **geometryPolygon** 인스턴스의 WKT 표현입니다. *polygon_tagged_text* 는 **nvarchar(max)** 식입니다.  
  
 *SRID*  
 반환하려는 **geometryPolygon** 인스턴스의 SRID(spatial reference ID)를 나타내는 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
 OGC 형식: **Polygon**  
  
## <a name="remarks"></a>설명  
 이 메서드는 입력이 잘못된 경우 **FormatException** 을 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STPolyFromText()`를 사용하여 `geometry` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STPolyFromText('POLYGON ((5 5, 10 5, 10 10, 5 5))', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [OGC 정적 기하 도형 메서드](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

