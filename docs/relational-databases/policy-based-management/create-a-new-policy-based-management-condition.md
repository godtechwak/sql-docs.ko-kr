---
description: 새로운 정책 기반 관리 조건 만들기
title: 새로운 정책 기반 관리 조건 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, creating policy conditions
ms.assetid: 8a612f7e-6c70-49db-a4de-48431e097cc5
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 76c60d4561eacda47648d2cac710e64c2ccc1f4e
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127908"
---
# <a name="create-a-new-policy-based-management-condition"></a>새로운 정책 기반 관리 조건 만들기
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 을 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 정책 기반 관리 조건을 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 조건을 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-condition"></a>조건을 만들려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 정책 기반 관리 조건을 만들려는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **정책 관리** 를 확장합니다.  
  
4.  더하기 기호를 클릭하여 **패싯** 폴더를 확장합니다.  
  
5.  새 조건을 만들려는 패싯을 마우스 오른쪽 단추로 클릭하고 **새 조건** 을 선택합니다.  
  
6.  **새 조건 만들기** 대화 상자의 **이름** 상자에 새 조건의 이름을 입력합니다.  
  
7.  **패싯** 목록에서 올바른 패싯을 확인하거나 다른 패싯을 선택합니다.  
  
8.  **식** 의 **필드** 상자에서 패싯 속성과 관련 연산자 및 값을 선택하여 조건 식을 생성합니다. 여러 식을 추가할 때 **And** 또는 **Or** 를 사용하여 식을 조인할 수 있습니다. 이 대화 상자에서 사용할 수 있는 옵션에 대한 자세한 내용은 [새 조건 만들기 또는 조건 열기 대화 상자, 일반 페이지](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-general-page.md), [새 조건 만들기 또는 조건 열기 대화 상자, 설명 페이지](../../relational-databases/policy-based-management/create-new-condition-or-open-condition-dialog-box-description-page.md) 및 [고급 편집&#40;조건&#41; 대화 상자](../../relational-databases/policy-based-management/advanced-edit-condition-dialog-box.md)를 참조하세요.  
  
9. 완료되었으면 **확인** 을 클릭합니다.  
  
  
