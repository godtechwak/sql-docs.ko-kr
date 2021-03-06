---
description: 데이터 형식 지원
title: 데이터 형식 지원 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ab0fd163713a7f6657d8ce446336f5c35a3dd00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456640"
---
# <a name="data-type-support"></a>데이터 형식 지원
ODBC 드라이버는 SQL_CHAR 및 SQL_VARCHAR 중 하나 이상을 지원 해야 합니다. 다른 데이터 형식에 대 한 지원은 드라이버 또는 데이터 원본의 SQL-92 규칙 수준에 따라 결정 됩니다. 응용 프로그램은 **SQLGetTypeInfo** 를 호출 하 여 드라이버에서 지 원하는 데이터 형식을 확인 해야 합니다.  
  
 데이터 형식에 대 한 자세한 내용은 [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)을 참조 하세요.
