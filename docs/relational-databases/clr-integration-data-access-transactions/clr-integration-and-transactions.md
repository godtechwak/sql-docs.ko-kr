---
title: CLR 통합 및 트랜잭션 | Microsoft Docs
description: CLR 통합 및 트랜잭션의 경우, 트랜잭션과 ADO.NET는 함께 작동 하 여 관리 되는 응용 프로그램에서 로컬 및 분산 트랜잭션의 사용을 확장 하 고 간소화 합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- managed code [SQL Server], transactions
- common language runtime [SQL Server], transactions
- System.Transactions namespace
- transactions [CLR integration]
ms.assetid: 381d206e-06e2-48d0-8206-295fcf06ac98
author: rothja
ms.author: jroth
ms.openlocfilehash: bd65fce2f2a2bdf2ce25f4811063f7f9d56d2e15
ms.sourcegitcommit: 36fe62a3ccf34979bfde3e192cfa778505add465
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94521140"
---
# <a name="clr-integration-and-transactions"></a>CLR 통합 및 트랜잭션
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **System.Transactions** 네임스페이스는 이미 통합된 ADO.NET 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR(공용 언어 런타임)과 완전히 통합되는 트랜잭션 프레임워크를 제공합니다. **System.object** 와 ADO.NET는 함께 작동 하 여 관리 되는 응용 프로그램에서 로컬 및 분산 트랜잭션의 사용을 확장 하 고 간소화 합니다.  
  
> [!NOTE]  
>  CLR UDP(사용자 정의 프로시저)는 해당 프로시저가 실행되는 서버에 대한 연결(루프백 연결)을 설정할 수 없으며 동일한 트랜잭션에 참여할 수도 없습니다. 이러한 작업을 시도하면 연결 시도가 차단되고 제어가 다시 UDP로 전달되지 않습니다. 이 경우 UDP에서 시간 초과 오류(메시지 1206)가 발생합니다.  
  
 트랜잭션 및 .NET Framework에 대한 자세한 내용은 .NET Framework SDK의 "트랜잭션 수행" 및 "트랜잭션 이용"을 참조하십시오.  
  
## <a name="in-this-section"></a>섹션 내용  
 [트랜잭션 승격](../../relational-databases/clr-integration-data-access-transactions/transaction-promotion.md)  
 트랜잭션을 승격하는 기능과 이 기능을 사용하는 방법에 대해 설명합니다.  
  
 [현재 트랜잭션 액세스](../../relational-databases/clr-integration-data-access-transactions/accessing-the-current-transaction.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 현재 in-process으로 실행 중인 트랜잭션에 액세스하는 방법에 대해 설명합니다.  
  
 [System.Transactions 사용](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)  
 관리 되는 응용 프로그램에서 **시스템의 트랜잭션** API (응용 프로그래밍 인터페이스)를 사용 하는 방법을 설명 합니다.  
  
 [트랜잭션 수명](../../relational-databases/clr-integration-data-access-transactions/transaction-lifetimes.md)  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저에서 시작된 트랜잭션과 CLR 애플리케이션에서 시작된 트랜잭션의 수명 차이에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CLR 데이터베이스 개체에서 데이터 액세스](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
