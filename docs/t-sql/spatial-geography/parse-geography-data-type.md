---
description: Parse(geography 데이터 형식)
title: Parse(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- Parse method
- Parse (geography Data Type)
ms.assetid: 21c402fa-fd0f-4d09-a097-49cee0316d4e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9ba373a279750e7399881edcc072dc3a086ec5e2
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88360009"
---
# <a name="parse-geography-data-type"></a>Parse(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 **geography** 인스턴스를 반환합니다. SRID(Spatial Reference ID) 4326을 매개 변수로 가정한다는 점을 제외하고 Parse()는 [STGeomFromText](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)와 동일합니다. 입력은 Z(높이) 값과 M(측정값) 값을 선택적으로 포함할 수 있습니다.
  
이 **geography** 데이터 형식 메서드는 **FullGlobe** 인스턴스 또는 반구보다 큰 공간 인스턴스를 지원합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
Parse ( 'geography_tagged_text' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *geography_tagged_text*  
 반환할 **geography** 인스턴스의 WKT 표현입니다. *geography_tagged_text* 는 **nvarchar** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
## <a name="remarks"></a>설명  
 `Parse()`에 의해 반환되는 **geography** 인스턴스의 OGC 형식은 해당 WKT 입력으로 설정됩니다.  
  
 문자열 'Null'은 Null **geography** 인스턴스로 해석됩니다.  
  
 이 메서드는 입력에 대척점 끝이 있을 경우 **ArgumentException** 을 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Parse()`를 사용하여 `geography` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geography;   
SET @g = geography::Parse('LINESTRING(-122.360 47.656, -122.343 47.656)');  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [확장 정적 지리 메서드](../../t-sql/spatial-geography/extended-static-geography-methods.md)   
 [STGeomFromText&#40;geography 데이터 형식&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
  
  
