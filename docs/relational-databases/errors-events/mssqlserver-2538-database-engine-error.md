---
description: MSSQLSERVER_2538
title: MSSQLSERVER_2538 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2538 (Database Engine error)
ms.assetid: 0a0f7d79-f1ba-4749-8804-fb660cca3492
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c4d083a389ffb80760f025cfeaa95f5f3bbac6ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456284"
---
# <a name="mssqlserver_2538"></a>MSSQLSERVER_2538
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|2538|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|DBCC_ALLOCATION_SUMMARY_PER_FILE|  
|메시지 텍스트|파일 FILE. 익스텐트 수 = EXTENTS, 사용된 페이지 = USED_PAGES, 예약된 페이지 = RESERVED_PAGES.|  
  
## <a name="explanation"></a>설명  
이 정보는 DBCC CHECKALLOC 명령에 대한 출력의 일부로, 지정된 데이터베이스에 대해 할당된 익스텐트, 사용된 페이지 및 예약된 페이지를 파일별로 요약하여 보여 줍니다.  
  
## <a name="user-action"></a>사용자 동작  
None  
  
