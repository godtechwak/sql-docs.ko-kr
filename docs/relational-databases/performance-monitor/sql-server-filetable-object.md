---
title: SQL Server, FileTable 개체 | Microsoft 문서
description: FileTable 및 트랜잭션되지 않은 액세스와 관련된 통계에 대한 카운터를 제공하는 SQLServer:FileTable 성능 개체에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:FileTable
ms.assetid: 325f5e58-1095-450f-9321-dfacfe6fd55f
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 310bbb694eb3751d16543c5bc108ccdf2a880b02
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505724"
---
# <a name="sql-server-filetable-object"></a>SQL Server, FileTable 개체
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
**SQLServer:FileTable** 성능 개체는 FileTable 및 트랜잭션되지 않은 액세스와 관련된 통계에 대한 카운터를 제공합니다.

다음 표에서는 SQL Server **FileTable** 성능 개체에 대해 설명합니다.

|**SQL Server FileTable 카운터**|Description|  
|-------------|-----------------|  
|**Avg time delete FileTable item**|FileTable 항목을 삭제하는 데 걸리는 평균 시간(밀리초)입니다.|
|**Avg time FileTable enumeration**|FileTable 열거형 요청에 걸리는 평균 시간(밀리초)입니다.|
|**Avg time FileTable handle kill**|FileTable 핸들을 중지하는 데 걸리는 평균 시간(밀리초)입니다.|
|**Avg time move FileTable item**|FileTable 항목을 이동하는 데 걸리는 평균 시간(밀리초)입니다.|
|**Avg time per file I/O request**|들어오는 파일 I/O 요청을 처리하는 데 걸리는 평균 시간(밀리초)입니다.|
|**Avg time per file I/O response**|나가는 파일 I/O 응답을 처리하는 데 걸리는 평균 시간(밀리초)입니다.|
|**Avg time rename FileTable item**|FileTable 항목의 이름을 바꾸는 데 걸리는 평균 시간(밀리초)입니다.|
|**Avg time to get FileTable item**|FileTable 항목을 검색하는 데 걸리는 평균 시간(밀리초)입니다.|
|**Avg time update FileTable item**|FileTable 항목을 업데이트하는 데 걸리는 평균 시간(밀리초)입니다.|
|**FileTable db operations/sec**|초당 FileTable 저장소 구성 요소에 의해 처리된 총 데이터베이스 작업 이벤트 수입니다.|
|**FileTable enumeration reqs/sec**|초당 총 FileTable 열거형 요청 수입니다.|
|**FileTable file I/O requests/sec**|초당 총 들어오는 FileTable 파일 I/O 요청 수입니다.|
|**FileTable file I/O response/sec**|초당 총 나가는 파일 I/O 응답 수입니다.|
|**FileTable item delete reqs/sec**|초당 총 FileTable 항목 삭제 요청 수입니다.|
|**FileTable item get requests/sec**|초당 총 FileTable 항목 검색 요청 수입니다.|
|**FileTable item move reqs/sec**|초당 총 FileTable 항목 이동 요청 수입니다.|
|**FileTable item rename reqs/sec**|초당 총 FileTable 항목 이름 바꾸기 요청 수입니다.|
|**FileTable item update reqs/sec**|초당 총 FileTable 항목 업데이트 요청 수입니다.|
|**FileTable kill handle ops/sec**|초당 총 FileTable 핸들 중지 작업 수입니다.|
|**FileTable table operations/sec**|초당 FileTable 저장소 구성 요소에 의해 처리된 총 테이블 작업 이벤트 수입니다.|
|**Time delete FileTable item BASE**|내부 전용입니다.|
|**Time FileTable enumeration BASE**|내부 전용입니다.|
|**Time FileTable handle kill BASE**|내부 전용입니다.|
|**Time move FileTable item BASE**|내부 전용입니다.|
|**Time per file I/O request BASE**|내부 전용입니다.|
|**Time per file I/O response BASE**|내부 전용입니다.|
|**Time rename FileTable item BASE**|내부 전용입니다.|
|**Time to get FileTable item BASE**|내부 전용입니다.|
|**Time update FileTable item BASE**|내부 전용입니다.| 
 
## <a name="see-also"></a>참고 항목  
[리소스 사용 모니터링(시스템 모니터)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
