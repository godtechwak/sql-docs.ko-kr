---
description: STCrosses(geometry 데이터 형식)
title: STCrosses(geometry 데이터 형식) | Mrcrosoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STCrosses (geometry Data Type)
- STCrosses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCrosses (geometry Data Type)
ms.assetid: 3e3fc065-555a-4bee-8b71-e92f3dc62a4f
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: b7294db9b86f9a356fa7834b89642ec0b1653866
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88458942"
---
# <a name="stcrosses-geometry-data-type"></a>STCrosses(geometry 데이터 형식)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

**geometry** 인스턴스가 다른 **geometry** 인스턴스와 교차하면 1을 반환합니다. 그렇지 않으면 0을 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STCrosses ( other_geometry )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *other_geometry*  
 `STCrosses()`를 호출할 인스턴스와 비교할 다른 **geometry** 인스턴스입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>설명  
 다음 조건이 모두 true이면 두 **geometry** 인스턴스는 교차합니다.  
  
-   두 **geometry** 인스턴스가 교차하여 기하 도형의 차원이 원본 **geometry** 인스턴스의 최대 차원보다 작습니다.  
  
-   교차 집합은 두 원본 **geometry** 인스턴스 내에 있습니다.  
  
 이 메서드는 **geometry** 인스턴스의 SRID(spatial Reference ID)가 일치하지 않으면 항상 Null을 반환합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `STCrosses()`를 사용하여 두 `geometry` 인스턴스가 교차하는지 테스트합니다.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0)', 0);  
SET @h = geometry::STGeomFromText('LINESTRING(0 0, 2 2)', 0);  
SELECT @g.STCrosses(@h);  
```  
  
## <a name="see-also"></a>참고 항목  
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

