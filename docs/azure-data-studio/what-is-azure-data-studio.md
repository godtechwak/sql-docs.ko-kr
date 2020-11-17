---
title: Azure Data Studio란?
description: Azure Data Studio는 Windows, macOS, Linux에서 실행되는 간단한 무료 도구로, SQL Server, Azure SQL Database, Azure Synapse Analytics를 관리하는 데 사용됩니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: overview
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein
ms.custom: seodec18, sqlfreshmay19
ms.date: 10/20/2020
ms.openlocfilehash: 669379b4db1bd2c975875c443fe6a80e38926a5c
ms.sourcegitcommit: 2144a22ad4380182133e87664a907fe6f06b5f95
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2020
ms.locfileid: "94570880"
---
# <a name="what-is-azure-data-studio"></a>Azure Data Studio란?

Azure Data Studio는 Windows, macOS, Linux에서 온-프레미스 및 클라우드 데이터 플랫폼을 사용하는 데이터 전문가를 위한 플랫폼 간 데이터베이스 도구입니다.

Azure Data Studio는 IntelliSense, 코드 조각, 원본 제어 통합 및 통합 터미널을 포함하는 최신 편집기 환경을 제공합니다. 데이터 플랫폼 사용자를 대상으로 설계되었으며 쿼리 결과 세트의 기본 제공 차트 기능과 사용자 지정이 가능한 대시보드를 포함합니다.

Azure Data Studio와 데이터 공급자의 소스 코드는 GitHub에서 소프트웨어를 수정 및 사용할 수 있지만 클라우드 서비스에서 재배포하거나 호스트할 수는 없도록 하는 소스 코드 EULA에 따라 사용할 수 있습니다. 자세한 내용은 [Azure Data Studio FAQ](faq.md)를 참조하세요.

**[Azure Data Studio 다운로드 및 설치](./download-azure-data-studio.md)**

## <a name="sql-code-editor-with-intellisense"></a>IntelliSense를 포함하는 SQL 코드 편집기

Azure Data Studio는 여러 탭 창, 다양한 기능의 SQL 편집기, IntelliSense, 키워드 완성, 코드 조각, 코드 탐색, 원본 제어 통합(Git)과 같은 기본 제공 기능을 통해 일상적인 작업을 간편하게 수행할 수 있는 최신 키보드 중심 SQL 코딩 환경을 제공합니다. 주문형 SQL 쿼리를 실행한 다음, 결과를 표시하고 텍스트, JSON 또는 Excel로 저장합니다. 데이터를 편집하고, 즐겨 사용하는 데이터베이스 연결을 구성하며, 익숙한 개체 검색 환경에서 데이터베이스 개체를 찾습니다. SQL 편집기를 사용하는 방법에 대한 자세한 내용은 [SQL 편집기를 사용하여 데이터베이스 개체 만들기](tutorial-sql-editor.md)를 참조하세요.

## <a name="smart-sql-code-snippets"></a>스마트 SQL 코드 조각

SQL 코드 조각은 데이터베이스, 테이블, 뷰, 저장 프로시저, 사용자, 로그인, 역할을 만드는 적절한 SQL 구문을 생성하고 기존 데이터베이스 개체를 업데이트합니다. 스마트 코드 조각을 사용하여 개발 또는 테스트 목적으로 데이터베이스 복사본을 빠르게 만들고 CREATE 및 INSERT 스크립트를 생성 및 실행할 수 있습니다.

Azure Data Studio에서는 사용자 지정 SQL 코드 조각을 만드는 기능도 제공합니다. 자세한 내용은 [코드 조각 만들기 및 사용](code-snippets.md)을 참조하세요.

## <a name="customizable-server-and-database-dashboards"></a>사용자 지정 가능한 서버 및 데이터베이스 대시보드

다양한 기능의 사용자 지정 가능한 대시보드를 만들어 데이터베이스에서 성능 병목 현상을 모니터링하고 신속하게 해결합니다. 인사이트 위젯 및 데이터베이스(및 서버) 대시보드에 대한 자세한 내용은 [인사이트 위젯을 사용하여 서버 및 데이터베이스 관리](insight-widgets.md)를 참조하세요.

## <a name="connection-management-server-groups"></a>연결 관리(서버 그룹)

서버 그룹은 사용하는 서버 및 데이터베이스의 연결 정보를 구성하는 방법을 제공합니다. 자세한 내용은 [서버 그룹](server-groups.md)을 참조하세요.

## <a name="integrated-terminal"></a>통합 터미널

Azure Data Studio 사용자 인터페이스 안에 있는 통합 터미널 창에서 즐겨 사용하는 명령줄 도구(예: Bash, PowerShell, sqlcmd, bcp 및 ssh)를 사용할 수 있습니다. 통합 터미널에 대한 자세한 내용은 [통합 터미널](integrated-terminal.md)을 참조하세요.

## <a name="extensibility-and-extension-authoring"></a>확장성 및 확장 작성

기본 설치의 기능을 확장하여 Azure Data Studio 환경을 향상시킬 수 있습니다. Azure Data Studio는 데이터 관리 작업을 위한 확장성 지점과 확장 작성 지원을 제공합니다.

Azure Data Studio 확장성에 대해 자세히 알아보려면 [확장성](extensibility.md)을 참조하세요.
확장 작성에 대한 자세한 내용은 [확장 작성](extensions/extension-authoring.md)을 참조하세요.

## <a name="feature-comparison-with-sql-server-management-studio-ssms"></a>SSMS(SQL Server Management Studio)와의 기능 비교

**Azure Data Studio를 사용하는 경우:**

- 대부분 쿼리를 편집 또는 실행하는 경우입니다.
- 결과 집합을 빠르게 차트로 만들고 시각화하는 기능이 필요합니다.
- sqlcmd 또는 PowerShell을 사용하여 통합 터미널을 통해 대부분의 관리 작업을 실행할 수 있습니다.
- 마법사 환경이 별로 필요하지 않습니다.
- 심층 관리 또는 플랫폼 관련 구성을 수행할 필요가 없습니다.
- macOS 또는 Linux에서 실행해야 합니다.

**SQL Server Management Studio를 사용하는 경우:**

- 복잡한 관리 또는 플랫폼 구성을 수행하고 있습니다.
- 사용자 관리, 취약성 평가 및 보안 기능 구성을 비롯한 보안 관리를 수행하고 있습니다.
- 성능 튜닝 관리자 및 대시보드를 사용해야 합니다.
- 데이터베이스 다이어그램 및 테이블 디자이너를 사용합니다.
- 등록된 서버에 액세스해야 합니다.
- 활성 쿼리 통계 또는 클라이언트 통계를 사용합니다.

### <a name="shell-features"></a>셸 기능

|기능|Azure Data Studio|SSMS|
|:---|:---|:---|
|Azure 로그인|예|예|
|대시보드|예| |
|확장|예| |
|통합 터미널|예||
|개체 탐색기|예|예|
|개체 스크립팅|예|예|
|프로젝트 시스템|예||
|테이블에서 선택|예|예|
|원본 코드 제어|예||
|작업창|예||
|어둡게 모드를 포함한 테마|예||
|Azure Resource Explorer|미리 보기||
|스크립트 생성 마법사||예|
|개체 속성||예|
|테이블 디자이너||예|

### <a name="query-editor"></a>쿼리 편집기

|기능|Azure Data Studio|SSMS|
|:---|:---|:---|
|차트 뷰어|예||
|CSV, JSON, XLSX로 결과 내보내기|예||
|파일로 결과 저장||예|
|텍스트로 결과 표시||예|
|IntelliSense|예|예|
|코드 조각|예|예|
|플랜 표시|미리 보기|예|
|클라이언트 통계||예|
|활성 쿼리 통계||예|
|쿼리 옵션||예|
|공간 뷰어||예|
|SQLCMD|예|예|

### <a name="operating-system-support"></a>운영 체제 지원

|기능|Azure Data Studio|SSMS|
|:---|:---|:---|
|Windows|예|예|
|macOS|예||
|Linux|예||

### <a name="data-engineering"></a>데이터 엔지니어링

|기능|Azure Data Studio|SSMS|
|:---|:---|:---|
|외부 데이터 마법사|미리 보기||
|HDFS 통합|미리 보기||
|Notebooks|미리 보기||

### <a name="database-administration"></a>데이터베이스 관리

|기능|Azure Data Studio|SSMS|
|:---|:---|:---|
|백업/복원|예|예|
|플랫 파일 가져오기|예|예|
|SQL 에이전트|미리 보기|예|
|SQL 프로파일러|미리 보기|예|
|Always On||예|
|Always Encrypted||예|
|데이터 복사 마법사||예|
|데이터 튜닝 관리자||예|
|데이터베이스 다이어그램||예|
|오류 로그 뷰어||예|
|유지 관리 계획||예|
|다중 서버 쿼리||예|
|정책 기반 관리||예|
|PolyBase||예|
|쿼리 저장소||예|
|등록된 서버||예|
|복제||예|
|보안 관리||예|
|Service Broker||예|
|SQL 평가|미리 보기|예|
|SQL 메일||예|
|Template Explorer||예|
|취약성 평가||예|
|XEvent 관리||예|

### <a name="database-development"></a>데이터베이스 개발
|기능|Azure Data Studio|SSMS|
|:---|:---|:---|
|DACPAC 가져오기\내보내기|예|예|
|SQL 프로젝트|미리 보기||
|스키마 비교|예||

## <a name="next-steps"></a>다음 단계

- [Azure Data Studio 다운로드 및 설치](./download-azure-data-studio.md)
- [Azure Data Studio FAQ](faq.md)
- [SQL Server 연결 및 쿼리](quickstart-sql-server.md)
- [Azure SQL Database 연결 및 쿼리](quickstart-sql-database.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
