---
description: 일정에 따라 정책 기반 관리 정책 평가
title: 일정에 따라 정책 기반 관리 정책 평가 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, evaluate policy
ms.assetid: bea09522-ff47-4037-ab55-a98ea7c10099
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 79e16f9a39e235f7ceed5a77e55d03f4c5efed72
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127873"
---
# <a name="evaluate-a-policy-based-management-policy-on-a-schedule"></a>일정에 따라 정책 기반 관리 정책 평가
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 일정에 따라 정책 기반 관리 정책을 평가하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 일정에 따라 정책을 평가하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-evaluate-a-policy-on-a-schedule"></a>일정에 따라 정책을 평가하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 평가하려는 정책 일정이 들어 있는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **정책 관리** 를 확장합니다.  
  
4.  더하기 기호를 클릭하여 **정책** 폴더를 확장합니다.  
  
5.  평가하려는 일정이 지정된 정책을 마우스 오른쪽 단추로 클릭하고 **속성** 을 선택합니다.  
  
6.  **정책 열기** _–policy_name_ 대화 상자의 **평가 모드** 목록에서 **예약 시** 를 선택합니다.  
  
7.  **일정** 에서 **선택** 을 클릭하여 기존 일정을 지정하거나 **새로 만들기** 를 클릭하여 새 일정을 만듭니다.  
  
8.  완료되었으면 **확인** 을 클릭합니다.  
  
  
