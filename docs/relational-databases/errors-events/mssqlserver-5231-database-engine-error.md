---
description: MSSQLSERVER_5231
title: MSSQLSERVER_5231 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5231 (Database Engine error)
ms.assetid: 6954ae84-ed0b-4f4c-9d0a-e73f3d71476c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 634b525a3daa2b5ac83a759c89c8edd52eb5ca6d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471045"
---
# <a name="mssqlserver_5231"></a>MSSQLSERVER_5231
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|5231|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC4_DEADLOCK_SKIPPED_OBJECT|  
|메시지 텍스트|개체 ID O_ID(개체 'NAME'): 확인을 위해 이 개체를 잠그는 동안 교착 상태가 발생했습니다. 이 개체를 건너뛰었으므로 처리되지 않습니다.|  
  
## <a name="explanation"></a>설명  
DBCC가 개체를 잠그려고 할 때 교착 상태가 발생하여 DBCC 실행이 중지되었습니다. 개체가 처리되지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
None  
  
