---
description: EnvelopeAggregate(geography 데이터 형식)
title: EnvelopeAggregate(geography 데이터 형식) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeAggregate_TSQL
- EnvelopeAggregate
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAggregate method (geography)
ms.assetid: 4947797f-edb8-490f-beca-37df9ec06954
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 9b14db5a616f41049b5cabc845cd822356e34522
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96114990"
---
# <a name="envelopeaggregate-geography-data-type"></a>EnvelopeAggregate(geography 데이터 형식)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

지정된 **geography** 개체 집합에 대한 경계 개체를 반환합니다. 결과 **geography** 개체는 여러 원호 세그먼트를 포함합니다.
  
## <a name="syntax"></a>구문  
  
```  
  
EnvelopeAggregate ( geography_operand )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *geography_operand*  
 봉투 집계 연산을 수행할 **geography** 개체 집합을 보관하는 **geography** 형식 테이블 열입니다.  
  
## <a name="return-types"></a>반환 형식  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 반환 형식: **geography**  
  
## <a name="remarks"></a>설명  
 결과 경계 개체가 반구보다 크면 **FullGlobe** 개체가 반환됩니다. 이 메서드는 정확하지 않습니다.  
  
 메서드가 입력에 다른 SRID가 있을 경우 **null** 을 반환합니다. [공간 참조 식별자 &#40;SRID&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)를 참조하세요.  
  
 이 메서드는 **null** 입력을 무시합니다.  
  
> [!NOTE]  
>  이 메서드는 모든 입력 값이 **null** 인 경우 **null** 을 반환합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 한 도시 안의 **geography** 위치 지점 집합에서 `EnvelopeAggregate`를 수행합니다.  
  
 ```
 USE AdventureWorks2012  
 GO  
 SELECT City,  
 geography::EnvelopeAggregate(SpatialLocation) AS SpatialLocation  
 FROM Person.Address  
 WHERE PostalCode LIKE('981%')  
 GROUP BY City;
 ```  
  
## <a name="see-also"></a>참고 항목  
 [확장 정적 지리 메서드](../../t-sql/spatial-geography/extended-static-geography-methods.md)  
  
  
