---
description: catalog.get_project(SSISDB 데이터베이스)
title: catalog.get_project(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: f263c9e4-a7db-4888-a458-70ae99b1f729
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d26de0736fc41d3b39f0f6c3e149b044c538ba41
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129773"
---
# <a name="catalogget_project-ssisdb-database"></a>catalog.get_project(SSISDB 데이터베이스)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 배포된 프로젝트의 이진 스트림을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.get_project [ @folder_name = ] folder_name , [ @project_name = ] project_name   
```  
  
## <a name="arguments"></a>인수  
 [ @folder_name = ] *folder_name*  
 프로젝트가 있는 폴더의 이름입니다. *folder_name* 은 **nvarchar(128)** 입니다.  
  
 [ @project_name = ] *project_name*  
 프로젝트의 이름입니다. *project_name* 은 **nvarchar(128)** 입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공)  
  
## <a name="result-sets"></a>결과 집합  
 프로젝트의 이진 스트림은 **varbinary(MAX)** 로 반환됩니다. 폴더 또는 프로젝트가 없으면 아무 결과도 반환되지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   프로젝트에 대한 READ 권한  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
 다음 목록에서는 get_project 저장 프로시저에서 오류가 발생하는 몇 가지 조건을 설명합니다.  
  
-   프로젝트가 없는 경우  
  
-   폴더가 없는 경우  
  
-   사용자에게 적절한 권한이 없는 경우  
  
  
