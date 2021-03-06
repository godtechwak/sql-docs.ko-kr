---
title: SSIS Scale Out 로깅을 위한 계정 변경 | Microsoft Docs
description: SSIS(SQL Server Integration Services) Scale Out 로깅에 사용할 계정을 변경하는 방법을 알아봅니다.
ms.custom: performance
ms.date: 06/29/2020
ms.prod: sql
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.reviewer: maghan
ms.openlocfilehash: c53a389541408080f1de43da409b4b61ca85a0ec
ms.sourcegitcommit: 7035d9471876c70b99c58bf9b46af5cce6e9c66c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2020
ms.locfileid: "87522337"
---
# <a name="change-the-account-for-scale-out-logging"></a>Scale Out 로깅을 위한 계정 변경

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


Scale Out에서 SSIS 패키지를 실행하면 SSISDB 데이터베이스에 자동으로 생성된 사용자 계정인 **##MS_SSISLogDBWorkerAgentLogin##** 으로 이벤트 메시지가 기록됩니다. 이 사용자 로그인은 SQL Server 인증을 사용합니다.

Scale Out 로깅에 사용되는 계정을 변경하려면 다음을 수행합니다.

> [!NOTE]
> 로깅에 Windows 사용자 계정을 사용하는 경우 Scale Out 작업자 서비스를 실행한 계정과 동일한 계정을 사용합니다. 그렇지 않으면 SQL Server 로그인이 실패합니다.

## <a name="1-create-a-user-for-ssisdb"></a>1. SSISDB 사용자 만들기
데이터베이스 사용자를 만드는 방법에 대한 지침은 [데이터베이스 사용자 만들기](../../relational-databases/security/authentication-access/create-a-database-user.md)를 참조하세요.

## <a name="2-add-the-user-to-the-database-role-ssis_cluster_worker"></a>2. 데이터베이스 역할 ssis_cluster_worker에 사용자 추가

데이터베이스 역할을 조인하는 방법에 대한 지침은 [역할 조인](../../relational-databases/security/authentication-access/join-a-role.md)을 참조하세요.

## <a name="3-update-the-logging-information-in-ssisdb"></a>3. SSISDB에서 로깅 정보 업데이트
다음 예제와 같이 SQL Server 이름 및 연결 문자열을 매개 변수로 사용하여 `[catalog].[update_logdb_info]` 저장 프로시저를 호출합니다.

```sql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-the-scale-out-worker-service"></a>4. Scale Out 작업자 서비스 다시 시작
Scale Out 작업자 서비스를 다시 시작하여 변경 내용을 적용합니다.

## <a name="next-steps"></a>다음 단계
-   [Integration Services Scale Out 관리자](integration-services-ssis-scale-out-manager.md)
