---
description: STGeomCollFromWKB(geography 데이터 형식)
title: STGeomCollFromWK (geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomCollFromWKB (geography Data Type)
- STGeomCollFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMGeomCollFromWKB method
ms.assetid: bbed028c-9cd6-4236-b5e5-8e914a21f2e4
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9baf6072500531d5500aca1cc00e771d1650c9dc
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88445294"
---
# <a name="stgeomcollfromwkb-geography-data-type"></a>STGeomCollFromWKB(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현의 **GeometryCollection** 인스턴스를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STGeomCollFromWKB ( 'WKB_geometrycollection' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *WKB_geometrycollection*  
 반환할 **GeometryCollection** 인스턴스의 WKB 표현입니다. *WKB_geometrycollection* 은 **varbinary(max)** 식입니다.  
  
 *SRID*  
 반환할 **GeometryCollection** 인스턴스의 SRID(spatial reference ID)를 나타내는 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>설명  
 STGeomCollFromWKB()가 반환한 **geography** 인스턴스의 OGC 형식은 해당 WKB 입력에 따라 **GeometryCollection**, **MultiPolygon**, **MultiLineString** 또는 **MultiPoint** 로 설정됩니다.  
  
 이 메서드는 입력이 잘못된 경우 **FormatException** 예외를 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STGeomCollFromWKB()`를 사용하여 `geography` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomCollFromWKB(0x01070000000200000001010000007593180456965EC017D9CEF753D34740010200000002000000D7A3703D0A975EC08716D9CEF7D34740CBA145B6F3955EC08716D9CEF7D34740, 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [OGC 정적 지리 메서드](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
