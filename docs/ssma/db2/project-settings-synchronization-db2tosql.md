---
description: 프로젝트 설정 (동기화) (DB2ToSQL)
title: 프로젝트 설정 (동기화) (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: a5629a72-8c17-46a4-bb4d-19d51a0b98a2
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: d6b4aef228ca1631bb550437ff0f66ff20555cb0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88321069"
---
# <a name="project-settingssynchronization-db2tosql"></a>프로젝트 설정 (동기화) (DB2ToSQL)
**프로젝트 설정** 대화 상자의 동기화 페이지에는에서 테이블 및 저장 프로시저와 같은 데이터베이스 개체를 로드 하 고 새로 고치는 방법을 사용자 지정 하는 설정이 포함 되어 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
기본 작업 옵션은 DB2 데이터베이스에서 개체를 새로 고치고 SQL Server 데이터베이스와 개체를 동기화 하기 위한 기본 설정을 지정 합니다. 자세한 내용은 [데이터베이스에서 새로 고침 &#40;DB2ToSQL&#41;](../../ssma/db2/refresh-from-database-db2tosql.md)을 참조 하세요.  
  
동일한 설정을 포함 하는 두 개의 서로 다른 동기화 페이지에 액세스할 수 있습니다.  
  
-   모든 향후 SSMA 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **기본 프로젝트 설정**을 클릭 한 다음 왼쪽 창의 맨 아래에서 **동기화** 를 클릭 합니다.  
  
-   현재 프로젝트에 대 한 설정을 지정 하려면 **도구** 메뉴에서 **프로젝트 설정**을 클릭 한 다음 왼쪽 창의 맨 아래에서 **동기화** 를 클릭 합니다.  
  
## <a name="miscellaneous-options"></a>기타 옵션  
**시도한**  
에서 개체를 로드할 때의 시도 횟수를 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 현재 시도에서로 로드 되지 않은 개체는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSMA가 현재 동기화 프로세스의 최대 시도 수에 도달할 때까지 다시 시도 됩니다. 기본값 설정 값은 **2** 입니다.  
  
## <a name="synchronization-for-db2-options"></a>DB2 옵션에 대 한 동기화  
**로컬 및 원격 개체 변경에 대 한 작업**  
SSMA 및 데이터베이스 서버에서 개체 정의가 변경 되는 경우 동기화 대화 상자에서 기본 설정을 지정 합니다. 기본값 설정은 **데이터베이스에서 새로 고침**입니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 메타 데이터에 데이터베이스 정의를 로드 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  
**로컬 개체 변경에 대 한 작업**  
SSMA에서 개체가 변경 될 때 동기화 대화 상자에서 기본 설정을 지정 합니다. 기본값 설정은 **Skip**입니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 메타 데이터에 데이터베이스 정의를 로드 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  
**원격 개체 변경에 대 한 작업**  
데이터베이스 서버에서 개체가 변경 될 때 동기화 대화 상자에서 기본 설정을 지정 합니다. 기본값 설정은 **데이터베이스에서 새로 고침**입니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 메타 데이터에 데이터베이스 정의를 로드 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  
**로컬 개체 메타 데이터가 없는 경우의 작업**  
로컬 메타 데이터가 없는 경우 동기화 대화 상자에서 기본 설정을 지정 합니다. 기본값 설정은 **데이터베이스에서 새로 고침**입니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 메타 데이터에 데이터베이스 정의를 로드 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  
## <a name="synchronization-for-sql-server-options"></a>SQL Server 옵션에 대 한 동기화  
**로컬 및 원격 개체 변경에 대 한 작업**  
SSMA 및 데이터베이스 서버에서 개체 정의가 변경 되는 경우 동기화 대화 상자에서 기본 설정을 지정 합니다. 기본값 설정은 **데이터베이스에 쓰기**입니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 메타 데이터에 데이터베이스 정의를 로드 합니다.  
  
-   **데이터베이스에 쓰기**를 선택 하는 경우 ssma는 조건이 충족 될 때 ssma 메타 데이터 내용에 따라 데이터베이스의 개체를 업데이트 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  
**로컬 개체 변경에 대 한 작업**  
SSMA에서 개체가 변경 될 때 동기화 대화 상자에서 기본 설정을 지정 합니다. 기본값 설정은 **데이터베이스에 쓰기**입니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 메타 데이터에 데이터베이스 정의를 로드 합니다.  
  
-   **데이터베이스에 쓰기**를 선택 하는 경우 ssma는 조건이 충족 될 때 ssma 메타 데이터 내용에 따라 데이터베이스의 개체를 업데이트 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  
**원격 개체 변경에 대 한 작업**  
데이터베이스 서버에서 개체가 변경 될 때 동기화 대화 상자에서 기본 설정을 지정 합니다.  기본값 설정은 **데이터베이스에서 새로 고침**입니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 메타 데이터에 데이터베이스 정의를 로드 합니다.  
  
-   **데이터베이스에 쓰기**를 선택 하는 경우 ssma는 조건이 충족 될 때 ssma 메타 데이터 내용에 따라 데이터베이스의 개체를 업데이트 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  
**로컬 개체 메타 데이터가 없는 경우의 작업**  
로컬 메타 데이터가 없는 경우 동기화 대화 상자에서 기본 설정을 지정 합니다. 기본값 설정은 **데이터베이스에서 새로 고침**입니다.  
  
-   **데이터베이스에서 새로 고침**을 선택 하는 경우 ssma는 조건이 충족 될 때 **데이터베이스에서 새로 고침** 옵션을 선택 합니다.  
  
-   **데이터베이스에 쓰기**를 선택 하는 경우 ssma는 조건이 충족 될 때 데이터베이스에서 개체를 삭제 합니다.  
  
-   **건너뛰기**를 선택 하면 ssma는 새로 고침 작업을 수행 하지 않습니다.  
  
