---
description: STGeomFromWKB(geometry 데이터 형식)
title: STGeomFromWKB(geometry 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STGeomFromWKB (geometry Data Type)
- STGeomFromWKB_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STGeomFromWKB (geometry Data Type)
ms.assetid: 6546ddb0-4a5f-46e5-ba04-8007486c95ec
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: dbd382664925059128b21a5a1dce048d7703fc2a
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88479380"
---
# <a name="stgeomfromwkb-geometry-data-type"></a>STGeomFromWKB(geometry 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

OGC(Open Geospatial Consortium) WKB(Well-Known Binary) 표현에서 **geometry** 인스턴스를 반환합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
STGeomFromWKB ( 'WKB_geometry' , SRID )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *WKB_geometry*  
 반환하려는 **geometry** 인스턴스의 WKB 표현입니다. *WKB_geometry* 은 **varbinary(max)** 식입니다.  
  
 *SRID*  
 반환하려는 **geometry** 인스턴스의 SRID(Spatial Reference ID)를 나타내는 **int** 식입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geometry**  
  
 CLR 반환 형식: **SqlGeometry**  
  
## <a name="remarks"></a>설명  
 `STGeomFromText()`에 의해 반환되는 **geometry** 인스턴스의 OGC 형식은 해당 WKB 입력으로 설정됩니다.  
  
 이 메서드는 입력이 잘못된 경우 **FormatException** 을 throw합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `STGeomFromWKB()`를 사용하여 **geometry** 인스턴스를 만듭니다.  
  
```  
DECLARE @g geometry;   
SET @g = geometry::STGeomFromWKB(0x010200000003000000000000000000594000000000000059400000000000003440000000000080664000000000008066400000000000806640, 0);  
SELECT @g.STAsText();  
```  
  
## <a name="see-also"></a>참고 항목  
 [OGC 정적 기하 도형 메서드](../../t-sql/spatial-geometry/ogc-static-geometry-methods.md)  
  
  

