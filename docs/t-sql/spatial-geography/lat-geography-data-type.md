---
description: Lat(geography 데이터 형식)
title: Lat(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Lat
- Lat_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Lat method
ms.assetid: 051d66bc-04de-4c58-861c-760dc5b859b5
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e6aff42dafc123d19fd8a2ea9a2ffa637cc54ee3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422367"
---
# <a name="lat-geography-data-type"></a>Lat(geography 데이터 형식)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **geography** 인스턴스의 위도 속성을 반환합니다.  
  
## <a name="syntax"></a>구문  
  
```  
.Lat  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 형식: **float**  
  
 CLR 유형: **SqlDouble**  
  
## <a name="remarks"></a>설명  
 OpenGIS 모델에서 하나의 점으로 구성된 **geography** 인스턴스에 대해서만 Lat가 정의됩니다. **geography** 인스턴스에 둘 이상의 지점이 포함되어 있는 경우 이 속성은 NULL을 반환합니다. 이 속성은 정확하며 읽기 전용입니다.  
  
## <a name="examples"></a>예제  
 이 예에서는 지점을 만들고 지점의 위도를 반환합니다.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Lat;  
```  
  
## <a name="see-also"></a>참고 항목  
 [지리 인스턴스의 확장 메서드](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
