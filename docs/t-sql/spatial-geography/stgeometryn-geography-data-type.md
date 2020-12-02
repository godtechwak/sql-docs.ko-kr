---
description: STGeometryN(geography 데이터 형식)
title: STGeometryN(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeometryN (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STGeometryN method
ms.assetid: 53755f69-cd50-475b-b3b8-a1a9157cf03a
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 812a5e63f21de77028c1f00a08f1819c5a07be13
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88445249"
---
# <a name="stgeometryn-geography-data-type"></a>STGeometryN(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **GeometryCollection** 또는 해당 하위 유형 중 하나의 지정된 **geography** 요소를 반환합니다. **MultiPoint** 또는 **MultiLineString** 과 같은 **GeometryCollection** 의 하위 형식에 STGeometryN()을 사용하면 이 메소드는 N=1을 사용하여 호출할 경우 **geography** 를 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
.STGeometryN ( expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *expression*  
 1과 **GeometryCollection** 에 있는 **geography** 인스턴스 수 사이의 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>설명  
 이 메서드는 매개 변수가 [STNumGeometries()](../../t-sql/spatial-geography/stnumgeometries-geography-data-type.md)의 결과보다 크면 Null을 반환하고 *expression* 매개 변수가 1보다 작으면 **ArgumentOutOfRangeException** 을 throw합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `MultiPoint``geography` 인스턴스를 만들고 `STGeometryN()`을 사용하여 **GeometryCollection** 의 두 번째 `geography` 인스턴스를 찾습니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STGeometryN(2).ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [Geography 인스턴스의 OGC 메서드](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)  
  
  
