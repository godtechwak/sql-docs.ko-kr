---
title: SQL Server XTP 가상 프로세서 | Microsoft 문서
description: 메모리 내 OLTP 엔진의 가상 처리 하위 시스템에 대한 카운터를 포함하는 SQL Server XTP 가상 프로세서 성능 개체에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 0f691b3d-a8fd-4459-ad21-2cfc8574a8c0
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: c0547f8f93b548e7dcf51271e7c796bad52f46ad
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505477"
---
# <a name="sql-server-xtp-phantom-processor"></a>SQL Server XTP 가상 프로세서
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SQL Server XTP 가상 프로세서 성능 개체에는 메모리 내 OLTP 엔진의 가상 처리 하위 시스템과 관련된 카운터가 포함됩니다. 이 구성 요소는 SERIALIZABLE 격리 수준에서 실행되는 트랜잭션에서 가상 행을 검색하고 동시성 시나리오에서 제약 조건 유효성을 검사합니다.  
  
 이 표에서는 **SQL Server XTP 가상 프로세서** 카운터에 대해 설명합니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|**Dusty corner scan retries/sec (Phantom-issued)**|가상 프로세서에 의해 실행된 불량 영역 청소(dusty corner sweeps) 중 발생한 초당 검색 재시도 횟수입니다(평균). 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|  
|**Phantom expired rows removed/sec**|가상 검사에 의해 제거된 만료된 초당 행 수입니다(평균).|  
|**Phantom expired rows touched/sec**|가상 검사에 의해 처리된 만료된 초당 행 수입니다(평균).|  
|**Phantom expiring rows touched/sec**|가상 검사에 의해 처리된 만료되는 초당 행 수입니다(평균).|  
|**Phantom rows touched/sec**|가상 검사에 의해 처리된 초당 행 수입니다(평균).|  
|**Phantom scans started/sec**|초당 시작된 가상 검사 수입니다(평균).|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server XTP&#40;메모리 내 OLTP&#41; 성능 카운터](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
