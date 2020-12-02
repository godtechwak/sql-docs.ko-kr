---
description: catalog.create_folder(SSISDB 데이터베이스)
title: catalog.create_folder(SSISDB 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: 06fb3549-e970-4ca2-a61f-59affb9c6dcc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9c0c28c81f607f5ab7ddc71d84ae52ea848d9334
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129859"
---
# <a name="catalogcreate_folder-ssisdb-database"></a>catalog.create_folder(SSISDB 데이터베이스)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 폴더를 만듭니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.create_folder [ @folder_name = ] folder_name, [ @folder_id = ] folder_id OUTPUT  
```  
  
## <a name="arguments"></a>인수  
 [@folder_name =] *folder_name*  
 새 폴더의 이름입니다. *folder_name* 은 **nvarchar(128)** 입니다.  
  
 [@folder_name =] *folder_id*  
 폴더의 고유 식별자(ID)입니다. *folder_id* 는 **bigint** 입니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 폴더 식별자가 반환됩니다.  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한 중 하나가 필요합니다.  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
-   **sysadmin** 서버 역할에 대한 멤버 자격  
  
## <a name="errors-and-warnings"></a>오류 및 경고  
이름이 같은 폴더가 이미 있는 경우 저장 프로시저에서 오류를 반환합니다.  
  
  
