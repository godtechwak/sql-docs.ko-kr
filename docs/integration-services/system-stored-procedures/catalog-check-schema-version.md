---
description: catalog.check_schema_version
title: catalog.check_schema_version | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: e0d5e9f5-59c6-4118-87b5-4aa5c37a7df6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b8f1d04f2a41c247a3de8a66f5b07ee74f5036b5
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96129940"
---
# <a name="catalogcheck_schema_version"></a>catalog.check_schema_version 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SSISDB 카탈로그 스키마와 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 이진 파일(ISServerExec 및 SQLCLR 어셈블리)이 호환되는지 여부를 결정합니다.  
  
 ISServerExec.exc는 스키마와 이진 파일이 호환되지 않는 경우 오류 메시지를 기록합니다.  
  
 SSISDB 스키마 버전은 패치 적용 및 업그레이드 중에 스키마가 변경되면 증가합니다. 스키마와 이진 파일이 호환되는지 확인하기 위해 SSISDB 백업이 복원된 후 이 저장 프로시저를 실행하는 것이 좋습니다.  
  
## <a name="syntax"></a>구문  
  
```sql  
catalog.check_schema_version [ @use32bitruntime = ] use32bitruntime  
```  
  
## <a name="arguments"></a>인수  
 [ @use32bitruntime= ] *use32bitruntime*  
 매개 변수를 **1** 로 설정하면 32비트 버전의 dtexec가 호출됩니다. *use32bitruntime* 은 **int** 입니다.  
  
## <a name="result-set"></a>결과 집합  
 None  
  
## <a name="permissions"></a>사용 권한  
 이 저장 프로시저를 실행하려면 다음 권한이 필요합니다.  
  
-   **ssis_admin** 데이터베이스 역할에 대한 멤버 자격  
  
  
