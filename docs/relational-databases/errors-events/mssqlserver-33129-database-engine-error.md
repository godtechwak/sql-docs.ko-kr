---
description: MSSQLSERVER_33129
title: MSSQLSERVER_33129 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 33129 (Database Engine error)
ms.assetid: 83b5f368-f1a1-4a40-9bb6-c77e2dec690f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 16340b6800ded7be2642f70496a09a16eb360274
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456226"
---
# <a name="mssqlserver_33129"></a>MSSQLSERVER_33129
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|33129|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SEC_CANNOT_DISABLE_WIN_GROUP|  
|메시지 텍스트|ALTER_LOGIN에 DISABLE 인수를 사용하여 Windows 그룹에 대한 액세스를 거부할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
이 메시지는 Windows 그룹의 로그인을 사용하지 않도록 설정할 때 발생합니다.  
  
## <a name="user-action"></a>사용자 동작  
Windows 그룹의 로그인은 사용하지 않도록 설정할 수 없습니다. Windows 그룹에 부여된 액세스 권한을 임시로 제거하려면 Windows 그룹의 로그인에 대한 CONNECT 권한을 취소합니다. 그래도 Windows 사용자는 자신의 개별 로그인이나 다른 Windows 그룹을 통해 액세스할 수 있습니다. 다음 예에서는 WESTCOAST 도메인의 Accounting 그룹에 대한 연결 권한을 취소합니다.  
  
```Transact-SQL  
REVOKE CONNECT TO [WESTCOAST\Accounting];  
```  
  
