---
description: 값 목록 인수
title: 값 목록 인수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fd2f2e970ea94635cda0b43b741abfda1130645b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421417"
---
# <a name="value-list-arguments"></a>값 목록 인수
값 목록 인수는 일치에 사용할 쉼표로 구분 된 값 목록으로 구성 됩니다. ODBC 카탈로그 함수에는 값 목록 인수가 하나 뿐입니다. **Sqltables**의 *TableType* 인수입니다. *TableType* 를 null 포인터로 설정 하는 것은 값 목록에서 가능한 모든 멤버를 열거 하는 SQL_ALL_TABLE_TYPES로 설정 된 것과 동일 합니다. 이 인수는 SQL_ATTR_METADATA_ID statement 특성의 영향을 받지 않습니다. 자세한 내용은 [Sqltables](../../../odbc/reference/syntax/sqltables-function.md) 함수 설명을 참조 하세요.
