---
description: '&#x40;&#x40;PACK_RECEIVED (Transact-SQL)'
title: '@@PACK_RECEIVED(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@PACK_RECEIVED_TSQL'
- '@@PACK_RECEIVED'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@PACK_RECEIVED function'
- number of packets read
- packets [SQL Server], number read
ms.assetid: 5c0b3d36-bfad-4f0b-abb8-e8f6391b32cd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7b3bb37af363727d1eb41922979ee6f78a9fd008
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124630"
---
# <a name="x40x40pack_received-transact-sql"></a>&#x40;&#x40;PACK_RECEIVED (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  마지막으로 시작한 이후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 네트워크에서 읽은 입력 패킷 수를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
@@PACK_RECEIVED  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 **integer**  
  
## <a name="remarks"></a>설명  
 보낸 패킷과 받은 패킷을 포함하여 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통계가 들어 있는 보고서를 표시하려면 **sp_monitor** 를 실행합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `@@PACK_RECEIVED`의 사용법을 보여 줍니다.  
  
```sql  
SELECT @@PACK_RECEIVED AS 'Packets Received';   
```  
  
 결과 집합의 예는 다음과 같습니다.  
  
```  
Packets Received  
----------------  
128  
```  
  
## <a name="see-also"></a>관련 항목  
 [@@PACK_SENT](../../t-sql/functions/pack-sent-transact-sql.md)   
 [sp_monitor](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [시스템 통계 함수](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
