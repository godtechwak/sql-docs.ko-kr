---
description: sys.dm_os_dispatcher_pools(Transact-SQL)
title: sys.dm_os_dispatcher_pools (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_dispatcher_pools_TSQL
- dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], views
- sys.dm_os_dispatcher_pools DMV
ms.assetid: b9edbc83-c6bc-4753-9bb5-a454cfe7d6bf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 352fe048404c452cc7f6012a166e395f4731f38a
ms.sourcegitcommit: 2991ad5324601c8618739915aec9b184a8a49c74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2020
ms.locfileid: "97322070"
---
# <a name="sysdm_os_dispatcher_pools-transact-sql"></a>sys.dm_os_dispatcher_pools(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  세션 발송자 풀에 대한 정보를 반환합니다. 발송자 풀은 백그라운드 처리를 수행하기 위해 시스템 구성 요소에서 사용하는 스레드 풀입니다.  
  
> [!NOTE]  
>  또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] **sys.dm_pdw_nodes_os_dispatcher_pools** 이름을 사용 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|dispatcher_pool_address|**varbinary(8)**|디스패처 풀의 주소입니다. dispatcher_pool_address 고유 합니다. Null을 허용하지 않습니다.|  
|형식|**nvarchar(256)**|발송자 풀의 유형입니다. Null을 허용하지 않습니다. 다음과 같은 두 가지 유형의 발송자 풀이 있습니다.<br /><br /> DISP_POOL_XE_ENGINE<br /><br /> DISP_POOL_XE_SESSION<br /><br /> 전체 목록에 대 한 DMV 쿼리|  
|name|**nvarchar(256)**|발송자 풀의 이름입니다. Null을 허용하지 않습니다.|  
|dispatcher_count|**int**|활성 발송자 스레드의 수입니다. Null을 허용하지 않습니다.|  
|dispatcher_ideal_count|**int**|발송자 풀이 증가하여 사용할 수 있게 되는 발송자 스레드의 수입니다. Null을 허용하지 않습니다.|  
|dispatcher_timeout_ms|**int**|발송자가 종료되기 전에 새로운 작업을 기다리는 시간(밀리초)입니다. Null을 허용하지 않습니다.|  
|dispatcher_waiting_count|**int**|유휴 발송자 스레드의 수입니다. Null을 허용하지 않습니다.|  
|queue_length|**int**|발송자 풀에서 처리되기 위해 대기 중인 작업 항목의 수입니다. Null을 허용하지 않습니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] , [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
SQL Database Basic, S0 및 S1 서비스 목적과 탄력적 풀의 데이터베이스에 대해서는 `Server admin` 또는 `Azure Active Directory admin` 계정이 필요 합니다. 다른 모든 SQL Database 서비스 목표에서 `VIEW DATABASE STATE` 사용 권한은 데이터베이스에서 필요 합니다.   

## <a name="see-also"></a>참고 항목  
  
  


