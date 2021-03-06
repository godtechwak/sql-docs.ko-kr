---
title: CLR 사용자 정의 함수 | Microsoft Docs
description: SQL Server CLR 통합을 사용 하면 모든 .NET Framework 프로그래밍 언어로 사용자 정의 스칼라 반환, 테이블 반환 및 집계 함수를 만들 수 있습니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- building database objects [CLR integration], user-defined functions
- functions [CLR integration]
- common language runtime [SQL Server], user-defined functions
- database objects [CLR integration], user-defined functions
- user-defined functions [CLR integration]
ms.assetid: 6f7491f1-9a46-4146-ae09-056248634de2
author: rothja
ms.author: jroth
ms.openlocfilehash: fe481b1a49f8eba69bbf913e49f398c86244b952
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727863"
---
# <a name="clr-user-defined-functions"></a>CLR 사용자 정의 함수
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  사용자 정의 함수는 매개 변수를 사용하여 계산이나 다른 동작을 수행한 다음 결과를 반환하는 루틴입니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#과 같은 모든 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 프로그래밍 언어를 사용하여 사용자 정의 함수를 작성할 수 있습니다.  
  
 함수에는 단일 값을 반환하는 스칼라 반환 함수와 행 집합을 반환하는 테이블 반환 함수의 두 가지 유형이 있습니다.  
  
 다음 표에서는 이 섹션에서 다루는 항목을 나열합니다.  
  
 [CLR 스칼라 반환 함수](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-scalar-valued-functions.md)  
 스칼라 반환 함수의 구현 요구 사항과 예를 다룹니다.  
  
 [CLR 테이블 반환 함수](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)  
 TVF(테이블 반환 함수)를 구현하고 사용하는 방법과 [!INCLUDE[tsql](../../includes/tsql-md.md)] 및 CLR(공용 언어 런타임) TVF 간의 차이점을 설명합니다.  
  
 [CLR 사용자 정의 집계](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)  
 사용자 정의 집계를 구현하고 사용하는 방법을 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [사용자 정의 함수](../../relational-databases/user-defined-functions/user-defined-functions.md)  
  
  
