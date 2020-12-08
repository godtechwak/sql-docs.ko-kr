---
title: SQL Server, Database Replica | Microsoft 문서
description: Always On 가용성 그룹의 보조 데이터베이스에 대한 성능 카운터를 포함하는 SQLServer:Database Replica 성능 개체에 대해 알아봅니다.
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- SQLServer:Database Replica
- performance counters [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], performance counters
ms.assetid: a5f6bdce-2b13-4924-aaeb-b50b57d624d8
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 176f7b9ba860e6ca7f72e35f6c6a87622948fc70
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505757"
---
# <a name="sql-server-database-replica"></a>SQL Server, 데이터베이스 복제본

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **SQLServer:Database Replica** 성능 개체는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 Always On 가용성 그룹의 보조 데이터베이스에 대한 정보를 보고하는 성능 카운터를 포함합니다. 이 개체는 보조 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서만 유효합니다.  
  
|카운터 이름|Description|표시 대상...|  
|------------------|-----------------|--------------|  
|**File Bytes Received/sec**|마지막 1초 동안 보조 데이터베이스에 대해 보조 복제본에서 받은 FILESTREAM 데이터의 양입니다.|보조 복제본|  
|**Log Apply Pending Queue**|데이터베이스 복제본에 적용되기를 기다리고 있는 로그 블록 수입니다.|보조 복제본|
|**Log Apply Ready Queue**|데이터베이스 복제본에 적용되기를 기다리고 있고 준비를 마친 로그 블록 수입니다.|보조 복제본|
|**Log Bytes Received/sec**|마지막 1초 동안 데이터베이스에 대해 보조 복제본에서 받은 로그 레코드의 양입니다.|보조 복제본|  
|**Log remaining for undo**|실행 취소 단계를 완료하기까지 남은 로그의 양(킬로바이트)입니다.|보조 복제본|  
|**Log Send Queue**|주 데이터베이스의 로그 파일에 있는 로그 레코드 중 보조 복제본으로 전송되지 않은 레코드의 양(킬로바이트)입니다. 이 값은 주 복제본에서 보조 복제본으로 전송됩니다. 보조 복제본으로 전송되는 FILESTREAM 파일은 큐 크기에 포함되지 않습니다.|보조 복제본|  
|**Mirrored Write Transactions/sec**|주 데이터베이스에 기록된 다음 마지막 1초 동안 로그가 보조 데이터베이스에 전송될 때까지 커밋을 기다린 트랜잭션 수입니다.|주 복제본|  
|**Recovery Queue**|다시 실행되지 않은 보조 복제본의 로그 파일에 있는 로그 레코드의 양입니다.|보조 복제본|  
|**초당 차단된 다시 실행**|데이터베이스 독자가 보유한 잠금에서 다시 실행 스레드가 차단되는 횟수입니다.|보조 복제본|  
|**Redo Bytes Remaining**|되돌리기 단계를 완료하기 위해 다시 실행할 남은 로그 양(킬로바이트)입니다.|보조 복제본|  
|**Redone Bytes/sec**|마지막 1초 동안 보조 데이터베이스에서 다시 실행된 로그 레코드의 양입니다.|보조 복제본|  
|**Total Log requiring undo**|실행 취소해야 하는 로그의 총 크기(KB)입니다.|보조 복제본|  
|**Transaction Delay**|모든 현재 트랜잭션 대한 종결되지 않은 커밋 승인을 기다리는 데 걸리는 시간(밀리초)입니다. *미러된 쓰기 트랜잭션/초* 로 나누어 *평균 Transaction Delay* 를 가져옵니다. 자세한 내용은 [SQL Server 2012 AlwaysOn – 파트 12 – 성능 측면 및 성능 모니터링 II](/archive/blogs/saponsqlserver/sql-server-2012-alwayson-part-12-performance-aspects-and-performance-monitoring-ii)를 참조하세요.|주 복제본|  
  
## <a name="see-also"></a>참고 항목
  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, 가용성 복제본](../../relational-databases/performance-monitor/sql-server-availability-replica.md)   
 [SQL Server, Databases 개체](../../relational-databases/performance-monitor/sql-server-databases-object.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
