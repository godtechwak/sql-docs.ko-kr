---
title: SQL Server, Columnstore 개체 | Microsoft 문서
description: SQL Server에서 columnstore 인덱스 실행을 모니터링하기 위한 카운터를 제공하는 SQLServer:Columnstore 개체에 대해 알아봅니다.
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae663a49-012f-4ffe-a332-f03157843052
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 61f950b5322270ce1b72b1734b92474dfb18b2bb
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505794"
---
# <a name="sql-server-columnstore-object"></a>SQL Server, Columnstore 개체
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **SQLServer:Columnstore** 개체는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 columnstore 인덱스 실행을 모니터링하기 위한 카운터를 제공합니다.  
  
 다음 테이블에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Columnstore** 카운터를 설명합니다.  
  
|Columnstore 카운터|Description|  
|--------------------------|-----------------|  
|**Delta Rowgroups Closed**|닫은 델타 행 그룹의 수입니다.|  
|**Delta Rowgroups Compressed**|압축된 델타 행 그룹의 수입니다.|  
|**Delta Rowgroups Created**|만든 델타 행 그룹의 수입니다.|  
|**Segment Cache Hit Raio**|디스크에서 읽지 않고 columnstore 풀에서 찾은 열 세그먼트의 백분율입니다.|  
|**Segment Cache Hit Ratio Base**|내부 전용입니다.|
|**Segment Reads/Sec**|실행된 물리적 세그먼트 읽기 수입니다.|  
|**Total Delete Buffers Migrated**|튜플 이동기에서 삭제 버퍼를 정리한 횟수입니다.|  
|**Total Merge Policy Evaluations**|columnstore에 대한 병합 정책이 평가된 횟수입니다.|  
|**Total Rowgroups Compressed**|압축된 행 그룹의 총수입니다.|  
|**Total Rowgroups Fit For Merge**|SQL Server를 시작한 이후 MERGE에 적합한 원본 행 그룹의 수입니다.|  
|**Total Rowgroups Merge Compressed**|SQL Server를 시작한 이후 MERGE를 사용하여 만든 압축된 대상 행 그룹의 수입니다.|  
|**Total Source Rowgroups Merged**|SQL Server를 시작한 이후 병합된 원본 행 그룹의 수입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
