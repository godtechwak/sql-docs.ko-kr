---
description: SQLGetFunctions(커서 라이브러리)
title: SQLGetFunctions (커서 라이브러리) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac307fbc1dcd2b10777ebe2e92f48f053ffcbd6c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499976"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions(커서 라이브러리)
> [!IMPORTANT]  
>  이 기능은 이후 버전의 Windows에서 제거 될 예정입니다. 새 개발 작업에서는이 기능을 사용 하지 않도록 하 고 현재이 기능을 사용 하는 응용 프로그램은 수정 하십시오. 드라이버의 커서 기능을 사용 하는 것이 좋습니다.  
  
 이 항목에서는 커서 라이브러리에서 **SQLGetFunctions** 함수를 사용 하는 방법을 설명 합니다. **SQLGetFunctions**에 대 한 일반 정보는 [SQLGetFunctions 함수](../../../odbc/reference/syntax/sqlgetfunctions-function.md)를 참조 하세요.  
  
 **SQLGetFunctions**를 호출 하면 커서 라이브러리는 드라이버에서 지 원하는 함수 외에 **sqlextendedfetch**, **Sqlextendedfetch**, **SQLSetPos**및 **SQLSetScrollOptions**를 지원 한다는 것을 반환 합니다.
