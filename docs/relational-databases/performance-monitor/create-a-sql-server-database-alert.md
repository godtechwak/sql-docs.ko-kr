---
title: SQL Server 데이터베이스 경고 만들기 | Microsoft 문서
description: 시스템 모니터를 사용하여 시스템 모니터 카운터의 임계값에 도달했을 때 발생하는 SQL Server 데이터베이스 경고를 만들 수 있습니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- database performance [SQL Server], alerts
- alerts [SQL Server], creating
- thresholds [SQL Server]
- database alerts [SQL Server]
- tuning databases [SQL Server], alerts
- monitoring performance [SQL Server], alerts
- monitoring server performance [SQL Server], alerts
- database monitoring [SQL Server], alerts
- server performance [SQL Server], alerts
ms.assetid: 0511136a-1b6b-4095-aa45-39e77b67aba2
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 512c902e0b35e15b65866464500b4928e105d4ad
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506041"
---
# <a name="create-a-sql-server-database-alert"></a>SQL Server 데이터베이스 경고 만들기
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  시스템 모니터를 사용하여 시스템 모니터 카운터의 임계값에 도달했을 때 발생하는 경고를 만들 수 있습니다. 시스템 모니터는 경고에 대한 응답으로 경고 조건을 처리하기 위해 쓰여진 사용자 지정 애플리케이션과 같은 애플리케이션을 시작합니다. 예를 들어 교착 상태 횟수가 지정한 값을 넘어설 때 발생할 경고를 만들 수 있습니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 경고를 정의할 수도 있습니다. 자세한 내용은 [경고](../../ssms/agent/alerts.md)를 참조하세요.  
  
 시스템 모니터를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 경고를 설정하는 방법은 [SQL Server 데이터베이스 경고 설정&#40;Windows&#41;](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [sp_add_alert&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sys.sysperfinfo&#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  
