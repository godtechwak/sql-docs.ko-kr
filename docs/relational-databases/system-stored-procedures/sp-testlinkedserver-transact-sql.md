---
description: sp_testlinkedserver(Transact-SQL)
title: sp_testlinkedserver (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_testlinkedserver
- sp_testlinkedserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_testlinkedserver
ms.assetid: e63ca7d4-47d6-455e-9aac-421f9683dadc
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 483b717511d70028bd8af4fc4649f210bbb972b1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534829"
---
# <a name="sp_testlinkedserver-transact-sql"></a>sp_testlinkedserver(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  연결된 서버와의 연결을 테스트합니다. 테스트가 실패하는 경우 절차에서 오류 이유와 함께 예외가 발생합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_testlinkedserver [ @servername ] = servername  
```  
  
## <a name="arguments"></a>인수  
`[ @servername = ]servername` 연결 된 서버의 이름입니다. *servername* 은 **sysname**이며 기본값은 없습니다.  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 사용 권한이 선택되어 있지 않지만 호출자는 적절한 로그인 매핑이 있어야 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `SEATTLESales`라는 연결된 서버를 만든 다음 연결을 테스트합니다.  
  
```  
USE master;  
GO  
EXEC sp_addlinkedserver   
    'SEATTLESales',  
    N'SQL Server';  
GO  
sp_testlinkedserver SEATTLESales;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_addlinkedserver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)  
  
  
