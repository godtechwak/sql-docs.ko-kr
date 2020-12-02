---
description: 데이터베이스 메일 프로필 만들기
title: 데이터베이스 메일 프로필 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], public profiles
- profiles [SQL Server], Database Mail
- public profiles [Database Mail]
ms.assetid: 58ae749d-6ada-4f9c-bf00-de7c7a992a2d
author: stevestein
ms.author: sstein
ms.openlocfilehash: f3ee012fe4bcd7fa1cd98c51f537035fc6148938
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96125250"
---
# <a name="create-a-database-mail-profile"></a>데이터베이스 메일 프로필 만들기
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  **데이터베이스 메일 구성 마법사** 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 데이터베이스 메일 퍼블릭 프로필 및 프라이빗 프로필을 만들 수 있습니다. 메일 프로필에 대한 자세한 내용은 [데이터베이스 메일 프로필](database-mail-configuration-objects.md)을 참조하세요.
  
-   **시작하기 전 주의 사항:** [필수 구성 요소](#Prerequisites), [보안](#Security)  
  
-   **To Create a Database Mail private profile using:**  [Database Mail Configuration Wizard](#SSMSProcedure), [Transact-SQL](#PrivateProfile)  
  
-   **데이터베이스 메일 공용 프로필을 만드는 데 사용되는 도구:**  [데이터베이스 메일 구성 마법사](#SSMSProcedure), [Transact-SQL](#PublicProfile)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> 필수 조건  
 프로필에 대한 데이터베이스 메일 계정을 하나 이상 만듭니다. 데이터베이스 메일 계정을 만드는 방법은 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)를 참조하세요.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
 공개 프로필을 사용하여 **msdb** 데이터베이스에 액세스할 수 있는 모든 사용자는 해당 프로필을 사용하여 메일을 보낼 수 있습니다. 프라이빗 프로필은 사용자 또는 역할에 의해 사용될 수 있습니다. 프로필에 대한 액세스 권한을 역할에 부여하면 보다 쉽게 유지 관리되는 아키텍처가 생성됩니다. 메일을 보내려면 **msdb** 데이터베이스에서 **DatabaseMailUserRole** 의 멤버여야 하며 적어도 하나 이상의 데이터베이스 메일 프로필에 액세스할 수 있어야 합니다.  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 프로필 계정을 만들고 저장 프로시저를 실행하는 사용자는 sysadmin 고정 서버 역할의 멤버여야 합니다.  
  
##  <a name="using-database-mail-configuration-wizard"></a><a name="SSMSProcedure"></a> 데이터베이스 메일 구성 마법사 사용  
 **데이터베이스 메일 프로필을 만들려면**  
  
-   개체 탐색기에서 데이터베이스 메일을 구성할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결한 다음 서버 트리를 확장합니다.  
  
-   **관리** 노드를 확장합니다.  
  
-   데이터베이스 메일을 두 번 클릭하여 데이터베이스 메일 구성 마법사를 엽니다.  
  
-   **구성 태스크 선택** 페이지에서 **데이터베이스 메일 계정 및 프로필 관리** 옵션을 선택하고 **다음** 을 클릭합니다.  
  
-   **프로필 및 계정 관리** 페이지에서 **새 프로필 만들기** 옵션을 선택하고 **다음** 을 클릭합니다.  
  
-   **새 프로필** 페이지에서 프로필 이름과 설명을 지정하고, 프로필에 포함할 계정을 추가하고, **다음** 을 클릭합니다.  
  
-   **마법사 완료** 페이지에서 수행할 동작을 검토하고 **마침** 을 클릭하여 새 프로필 만들기를 완료합니다.  
  
-   **데이터베이스 메일 프라이빗 프로필을 구성하려면**  
  
    -   데이터베이스 메일 구성 마법사를 엽니다.  
  
    -   **구성 태스크 선택** 페이지에서 **데이터베이스 메일 계정 및 프로필 관리** 옵션을 선택하고 **다음** 을 클릭합니다.  
  
    -   **프로필 및 계정 관리** 페이지에서 **프로필 보안 관리** 옵션을 선택하고 **다음** 을 클릭합니다.  
  
    -   **프라이빗 프로필** 탭에서 구성하려는 프로필에 대한 확인란을 선택하고 **다음** 을 클릭합니다.  
  
    -   **마법사 완료** 페이지에서 수행할 동작을 검토하고 **마침** 을 클릭하여 프로필 구성을 완료합니다.  
  
-   **데이터베이스 메일 공개 프로필을 구성하려면**  
  
    -   데이터베이스 메일 구성 마법사를 엽니다.  
  
    -   **구성 태스크 선택** 페이지에서 **데이터베이스 메일 계정 및 프로필 관리** 옵션을 선택하고 **다음** 을 클릭합니다.  
  
    -   **프로필 및 계정 관리** 페이지에서 **프로필 보안 관리** 옵션을 선택하고 **다음** 을 클릭합니다.  
  
    -   **공개 프로필** 탭에서 구성하려는 프로필에 대한 확인란을 선택하고 **다음** 을 클릭합니다.  
  
    -   **마법사 완료** 페이지에서 수행할 동작을 검토하고 **마침** 을 클릭하여 프로필 구성을 완료합니다.  
  
## <a name="using-transact-sql"></a>Transact-SQL 사용  
  
###  <a name="to-create-a-database-mail-private-profile"></a><a name="PrivateProfile"></a> 데이터베이스 메일 프라이빗 프로필을 만들려면  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
-   새 프로필을 만들려면 시스템 저장 프로시저 [sysmail_add_profile_sp&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md)를 다음과 같이 실행합니다.  
  
     **EXECUTEmsdb.dbo.sysmail_add_profile_sp**  
  
     *\@profile_name* = '*프로필 이름*'  
  
     *\@description* = '*설명*'  
  
     여기서 *\@profile_name* 은 프로필의 이름이고 *\@description* 은 프로필에 대한 설명입니다. 이 매개 변수는 선택 사항입니다.  
  
-   각 계정에 대해 저장 프로시저 [sysmail_add_profileaccount_sp&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md)를 다음과 같이 실행합니다.  
  
     **EXECUTEmsdb.dbo.sysmail_add_profileaccount_sp**  
  
     *\@profile_name* = '*프로필 이름*'  
  
     *\@account_name* = '*계정 이름*'  
  
     *\@sequence_number* = '*프로필 내 계정의 시퀀스 번호.* '  
  
     여기서 *\@profile_name* 은 프로필의 이름이고, *\@account_name* 은 프로필에 추가할 계정의 이름이며, *\@sequence_number* 는 프로필에서 계정이 사용되는 순서를 결정합니다.  
  
-   이 프로필을 사용하여 메일을 보내는 각 데이터베이스 역할 또는 사용자에게 프로필에 대한 액세스 권한을 부여합니다. 이렇게 하려면 저장 프로시저 [sysmail_add_principalprofile_sp&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql.md)를 다음과 같이 실행합니다.  
  
     **EXECUTEmsdb.sysmail_add_principalprofile_sp**  
  
     *\@profile_name* = '*프로필 이름*'  
  
     *\@principal_name* = '*데이터베이스 사용자 또는 역할의 이름*'  
  
     *\@is_default* = '*기본 프로필 상태* '  
  
     여기서 *\@profile_name* 은 프로필의 이름이고, *\@principal_name* 은 데이터베이스 사용자 또는 역할의 이름이며, *\@is_default* 는 이 프로필이 데이터베이스 사용자 또는 역할에 대한 기본값인지 여부를 결정합니다.  
  
 다음 예에서는 데이터베이스 메일 계정을 만들고, 데이터베이스 메일 프라이빗 프로필을 만든 다음 프로필에 계정을 추가하며, **msdb** 데이터베이스의 **DBMailUsers** 데이터베이스 역할에 해당 프로필에 대한 액세스 권한을 부여합니다.  
  
```  
-- Create a Database Mail account  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @replyto_address = 'danw@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
  
-- Create a Database Mail profile  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @description = 'Profile used for administrative mail.' ;  
  
-- Add the account to the profile  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @account_name = 'AdventureWorks Administrator',  
    @sequence_number =1 ;  
  
-- Grant access to the profile to the DBMailUsers role  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @principal_name = 'ApplicationUser',  
    @is_default = 1 ;  
```  
  
###  <a name="to-create-a-database-mail-public-profile"></a><a name="PublicProfile"></a> 데이터베이스 메일 공개 프로필을 만들려면  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
-   새 프로필을 만들려면 시스템 저장 프로시저 [sysmail_add_profile_sp&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profile-sp-transact-sql.md)를 다음과 같이 실행합니다.  
  
     **EXECUTEmsdb.dbo.sysmail_add_profile_sp**  
  
     *\@profile_name* = '*프로필 이름*'  
  
     *\@description* = '*설명*'  
  
     여기서 *\@profile_name* 은 프로필의 이름이고 *\@description* 은 프로필에 대한 설명입니다. 이 매개 변수는 선택 사항입니다.  
  
-   각 계정에 대해 저장 프로시저 [sysmail_add_profileaccount_sp&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md)를 다음과 같이 실행합니다.  
  
     **EXECUTEmsdb.dbo.sysmail_add_profileaccount_sp**  
  
     *\@profile_name* = '*프로필 이름*'  
  
     *\@account_name* = '*계정 이름*'  
  
     *\@sequence_number* = '*프로필 내 계정의 시퀀스 번호.* '  
  
     여기서 *\@profile_name* 은 프로필의 이름이고, *\@account_name* 은 프로필에 추가할 계정의 이름이며, *\@sequence_number* 는 프로필에서 계정이 사용되는 순서를 결정합니다.  
  
-   공용 액세스를 허용하려면 저장 프로시저 [sysmail_add_principalprofile_sp&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql.md)를 다음과 같이 실행합니다.  
  
     **EXECUTEmsdb.sysmail_add_principalprofile_sp**  
  
     *\@profile_name* = '*프로필 이름*'  
  
     *\@ principal_name* = '**public** 또는 **0**'  
  
     *\@is_default* = '*기본 프로필 상태* '  
  
     여기서 *\@profile_name* 은 프로필의 이름이고, *\@principal_name* 은 이 프로필이 공용 프로필임을 나타내며, *\@is_default* 는 이 프로필이 데이터베이스 사용자 또는 역할에 대한 기본값인지 여부를 결정합니다.  
  
 다음 예에서는 데이터베이스 메일 계정을 만들고, 데이터베이스 메일 프라이빗 프로필을 만든 다음 프로필에 계정을 추가하며, 프로필에 대한 퍼블릭 액세스 권한을 부여합니다.  
  
```  
-- Create a Database Mail account  
  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Public Account',  
    @description = 'Mail account for use by all database users.',  
    @email_address = 'db_users@Adventure-Works.com',  
    @replyto_address = 'danw@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
  
-- Create a Database Mail profile  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @description = 'Profile used for administrative mail.' ;  
  
-- Add the account to the profile  
  
EXECUTE msdb.dbo.sysmail_add_profileaccount_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @account_name = 'AdventureWorks Public Account',  
    @sequence_number =1 ;  
  
-- Grant access to the profile to all users in the msdb database  
  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @profile_name = 'AdventureWorks Public Profile',  
    @principal_name = 'public',  
    @is_default = 1 ;  
```  
  
  
