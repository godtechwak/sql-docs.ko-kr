---
description: 수동 커밋 모드
title: 수동 커밋 모드 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb576166242078707846e005b958143812fd5901
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499837"
---
# <a name="manual-commit-mode"></a>수동 커밋 모드
*수동 커밋 모드에서* 응용 프로그램은 **sqlendtran** 을 호출 하 여 트랜잭션을 명시적으로 완료 하 여 커밋하거나 롤백합니다. 이는 대부분의 관계형 데이터베이스에 대 한 정상적인 트랜잭션 모드입니다.  
  
 ODBC의 트랜잭션은 명시적으로 시작할 필요가 없습니다. 대신 응용 프로그램이 데이터베이스에서 작동을 시작할 때마다 트랜잭션이 암시적으로 시작 됩니다. 데이터 원본에 명시적 트랜잭션 시작이 필요한 경우에는 응용 프로그램이 트랜잭션을 필요로 하는 문을 실행할 때마다 드라이버에서 제공 해야 하며, 현재 트랜잭션이 없습니다.
