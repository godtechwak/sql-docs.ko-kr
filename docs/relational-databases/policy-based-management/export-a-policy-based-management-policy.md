---
description: 정책 기반 관리 정책 내보내기
title: 정책 기반 관리 정책 내보내기 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, export policy
ms.assetid: f0001b33-9078-4432-8460-496736fb325a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 62fff3bda286f50b2220dbb1ea4732547e98829f
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127860"
---
# <a name="export-a-policy-based-management-policy"></a>정책 기반 관리 정책 내보내기
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 정책 기반 관리 정책을 내보내는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 정책을 내보내려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-export-a-policy"></a>정책을 내보내려면  
  
1.  개체 탐색기에서 더하기 기호를 클릭하여 내보내려는 정책 기반 관리 정책이 들어 있는 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **정책 관리** 를 확장합니다.  
  
4.  더하기 기호를 클릭하여 **정책** 폴더를 확장합니다.  
  
5.  내보내려는 정책을 마우스 오른쪽 단추로 클릭하고 **정책 내보내기** 를 선택합니다.  
  
6.  **정책 내보내기** 대화 상자의 주소 표시줄에 파일의 경로와 이름을 입력합니다. 또는 이 대화 상자의 탐색 창에서 파일에 적합한 위치를 찾은 다음 **파일 이름** 상자에 XML 파일의 이름을 입력합니다.  
  
7.  완료되면 **저장** 을 클릭합니다.  

