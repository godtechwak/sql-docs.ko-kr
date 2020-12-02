---
description: STMPointFromText(geography 데이터 형식)
title: STMPointFromText(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STMPointFromText (geography Data Type)
- STMPointFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STMPointFromText method
ms.assetid: fe91a9f5-8de6-464e-88db-00650eae79b0
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: d7b06ff31cd94422abfbbc559e569cfb2f610eae
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88467436"
---
# <a name="stmpointfromtext-geography-data-type"></a>STMPointFromText(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

인스턴스에서 얻어진 Z(높이) 값 및 M(측정값) 값을 사용하여 보강된 OGC(Open Geospatial Consortium) WKT(Well-Known Text) 표현의 **geography** 인스턴스를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STMPointFromText ( 'multipoint_tagged_text', SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *multipoint_tagged_text*  
 반환할 **geographyMultiPoint** 인스턴스의 WKT 표현입니다. *multipoint_tagged_text* 는 **nvarchar(max)** 식입니다.  
  
 *SRID*  
 반환할 **geographyMultiPoint** 인스턴스의 SRID(Spatial Reference ID)를 나타내는 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
 CLR 반환 형식: **SqlGeography**  
  
 OGC 형식: **MultiPoint**  
  
## <a name="remarks"></a>설명  
 이 메서드는 입력이 잘못된 경우 **FormatException** 을 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STMPointFromText()`를 사용하여 `geography` 인스턴스를 만듭니다.  
  
```  
DECLARE @g geography;   
SET @g = geography::STMPointFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>참고 항목  
 [OGC 정적 지리 메서드](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
