---
title: SQL Server XTP 가비지 수집 | Microsoft 문서
description: 메모리 내 OLTP 엔진의 가비지 수집기와 관련된 카운터를 포함하는 SQL Server XTP 가비지 수집 성능 개체에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 64ae91e5-b420-44b4-af1a-f8bca83d7f41
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 48e4b2864465e095220ab238d8288c6e12639dec
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505515"
---
# <a name="sql-server-xtp-garbage-collection"></a>SQL Server XTP 가비지 수집
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SQL Server XTP 가비지 수집 성능 개체에는 메모리 내 OLTP 엔진의 가비지 수집기와 관련된 카운터가 포함됩니다.  
  
 이 표에서는 **SQL Server XTP 가비지 수집** 카운터에 대해 설명합니다.  
  
|카운터|Description|  
|-------------|-----------------|  
|**Dusty corner scan retries/sec (GC-issued)**|가비지 수집기에 의해 실행된 불량 영역 청소(dusty corner sweeps) 중 발생한 초당 검색 재시도 횟수입니다(평균). 이 카운터는 사용자용이 아닌 매우 낮은 수준의 카운터입니다.|  
|**Main GC work items/sec**|기본 GC 스레드에서 처리되는 작업 항목 수입니다.|  
|**Parallel GC work item/sec**|병렬 스레드가 GC 작업 항목을 실행한 횟수입니다.|  
|**Rows processed/sec**|가비지 수집기에서 처리된 초당 행 수입니다(평균).|  
|**Rows processed/sec (first in bucket and removed)**|처음에 해당 해시 버킷에 포함되었고 즉시 제거할 수 있었던 가비지 수집기에서 처리된 초당 행 수입니다(평균).|  
|**Rows processed/sec (first in bucket)**|처음에 해당 해시 버킷에 포함되었던 가비지 수집기에서 처리된 초당 행 수입니다(평균).|  
|**Rows processed/sec (marked for unlink)**|이미 연결 해제로 표시된 가비지 수집기에서 처리된 초당 행 수입니다(평균).|  
|**Rows processed/sec (no sweep needed)**|불량 영역 청소(dusty corner sweep)가 필요하지 않은 가비지 수집기에 의해 처리된 초당 행 수입니다(평균).|  
|**Sweep expired rows removed/sec**|불량 영역 청소(dusty corner sweeps) 중 제거된 만료된 초당 행 수입니다(평균).|  
|**Sweep expired rows touched/sec**|불량 영역 청소(dusty corner sweeps) 중 처리된 만료된 초당 행 수입니다(평균).|  
|**Sweep expiring rows touched/sec**|불량 영역 청소(dusty corner sweeps) 중 처리된 만료되는 초당 행 수입니다(평균).|  
|**Sweep rows touched/sec**|불량 영역 청소(dusty corner sweeps) 중 처리된 초당 행 수입니다(평균).|  
|**Sweep scans started/sec**|시작된 초당 불량 영역 청소(dusty corner sweeps) 검사 수입니다(평균).|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server XTP&#40;메모리 내 OLTP&#41; 성능 카운터](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
