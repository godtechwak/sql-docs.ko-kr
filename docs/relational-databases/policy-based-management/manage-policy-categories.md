---
description: 정책 범주 관리
title: 정책 범주 관리 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.policycategories.f1
ms.assetid: d188a819-731f-4029-98aa-780d3299a0ce
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 26b15222f570304f321337a4b3574c3fa2f3b945
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88494016"
---
# <a name="manage-policy-categories"></a>정책 범주 관리
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 전체 [!INCLUDE[tsql](../../includes/tsql-md.md)]인스턴스에 한 범주의 사용 가능한 정책을 임의로 또는 모두 적용하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 SQL Server 인스턴스에 범주 정책을 적용하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 사용할 경우, **데이터베이스 구독 위임** 확인란이 선택되어 있지 않으면 하나 이상의 데이터베이스 또는 테이블과 같은 서버의 각 관련 부분에 정책 범주를 개별적으로 적용해야 합니다.  
  
-   없는 정책 범주를 지정하면 새 정책 범주가 만들어지고 저장 프로시저를 실행할 때 모든 데이터베이스에 대해 구독이 위임됩니다. 이후에 새 범주의 위임된 구독을 제거하면 *target_object* 로 지정한 데이터베이스에 대해서만 구독이 적용됩니다. 위임된 구독 설정을 변경하는 방법은 [sp_syspolicy_update_policy_category&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-update-policy-category-transact-sql.md)를 참조하세요.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 이 저장 프로시저는 현재 저장 프로시저 소유자의 컨텍스트에서 실행됩니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-apply-category-policies-to-a-sql-server-instance"></a>SQL Server 인스턴스에 범주 정책을 적용하려면  
  
1.  **개체 탐색기** 에서 더하기 기호를 클릭하여 범주 정책을 적용할 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  **정책 관리** 를 마우스 오른쪽 단추로 클릭하고 **범주 관리** 를 선택합니다.  
  
     **정책 범주 관리** 대화 상자에 다음 정보가 표시됩니다.  
  
     **이름**  
     정책 범주의 이름입니다.  
  
     **데이터베이스 구독 위임**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 데이터베이스가 정책 범주의 정책을 적용하도록 합니다.  
  
4.  **데이터베이스 구독 위임** 아래의 확인란을 임의로 또는 모두 선택하거나 선택 취소하여 해당 정책 범주를 SQL Server 인스턴스에 적용합니다.  
  
5.  완료되었으면 **확인** 을 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-apply-category-policies-to-a-sql-server-instance"></a>SQL Server 인스턴스에 범주 정책을 적용하려면  
  
1.  **개체 탐색기** 에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행** 을 클릭합니다.  
  
    ```  
    USE msdb;  
    GO  
    -- configures the specified database to subscribe to a policy category that is named 'Table Naming Policies'.  
    EXEC dbo.sp_syspolicy_add_policy_category_subscription @target_type = N'DATABASE'  
    , @target_object = N'AdventureWorks2012'  
    , @policy_category = N'Table Naming Policies';  
    GO  
    ```  
  
 자세한 내용은 [sp_syspolicy_add_policy_category_subscription&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-add-policy-category-subscription-transact-sql.md)을 참조하세요.  
  
  
