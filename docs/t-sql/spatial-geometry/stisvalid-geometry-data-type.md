---
description: STIsValid(geometry 데이터 형식)
title: STIsValid(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STIsValid (geometry Data Type)
- STIsValid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STIsValid (geometry Data Type)
ms.assetid: 6da39bea-0f67-4660-98fc-d7214f9b2138
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 65e86550626b1461cb8b0abc5e7fb354e6b4e3a4
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88472431"
---
# <a name="stisvalid-geometry-data-type"></a>STIsValid(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

**geometry** 인스턴스가 해당 OGC(Open Geospatial Consortium) 형식을 기반으로 올바르게 형식이 지정되었으면 True를 반환합니다. **geometry** 인스턴스의 형식이 잘못되었으면 False를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
.STIsValid ( )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **bit**  
  
 CLR 반환 형식: **SqlBoolean**  
  
## <a name="remarks"></a>설명  
 **geometry** 인스턴스의 OGC 형식은 [STGeometryType()](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)을 호출하여 확인할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 올바른 **geometry** 인스턴스만 생성하지만 잘못된 인스턴스도 스토리지하고 검색할 수 있도록 합니다. 잘못된 인스턴스의 동일한 점 집합을 나타내는 올바른 인스턴스는 `MakeValid()` 메서드를 사용하여 검색할 수 있습니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `geometry` 인스턴스를 만들고 `STIsValid()`를 사용하여 인스턴스가 올바른지 테스트합니다.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STIsValid();  
```  
  
## <a name="see-also"></a>관련 항목  
 [STGeometryType&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/stgeometrytype-geometry-data-type.md)   
 [MakeValid&#40;geometry 데이터 형식&#41;](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)   
 [geometry 인스턴스의 OGC 메서드](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

