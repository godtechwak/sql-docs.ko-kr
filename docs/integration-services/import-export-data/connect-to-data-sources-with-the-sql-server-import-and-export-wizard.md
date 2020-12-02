---
description: SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 원본에 연결
title: 데이터 원본에 연결(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: fd726506-54b7-433b-bf70-3642235b7b31
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7d8738fb22682ad4a6f432187998663c4c8282cd
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96122825"
---
# <a name="connect-to-data-sources-with-the-sql-server-import-and-export-wizard"></a>SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 원본에 연결

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


이 단원의 항목에서는 SQL Server 가져오기 및 내보내기 마법사를 실행할 때 자주 사용되는 데이터 원본에 연결하는 방법을 보여 줍니다. 마법사의 **데이터 원본 선택** 및 **대상 선택** 페이지에서 데이터 원본에 대한 연결 정보를 제공해야 합니다.

이 섹션의 항목에서는 마법사의 **데이터 원본 선택** 및 **대상 선택** 페이지에서 **데이터 원본에 연결** 하는 방법만 설명합니다. 다른 내용을 찾으려면 [관련 태스크 및 콘텐츠](#related)를 참조하세요.

## <a name="connect-to-a-commonly-used-data-source"></a>자주 사용되는 데이터 원본에 연결
자주 사용되는 다음 데이터 원본 중 하나에 연결하는 방법을 자세히 알아보려면 링크를 클릭합니다.
-   [SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [플랫 파일(텍스트 파일)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Azure Blob Storage](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)

## <a name="connect-to-other-data-providers"></a>다른 데이터 공급자에 연결
여기에 나열되지 않은 데이터 원본에 연결하는 방법에 대한 내용은 [연결 문자열 참조](https://www.connectionstrings.com/)를 참조하세요. 이 타사 사이트에는 샘플 연결 문자열과 필요한 데이터 공급자 및 연결 정보에 대한 추가 정보가 포함되어 있습니다.

## <a name="related-tasks-and-content"></a><a name="related"></a> 관련 태스크 및 콘텐츠  
다음은 몇 가지 다른 기본 작업입니다.
-   **마법사의 작동 원리에 대한 빠른 예제를 참조하세요.**

    -   **스크린샷을 보려면.** 단일 페이지([가져오기 및 내보내기 마법사의 간단한 예제 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md))에서 간단한 엔드투엔드 예제를 살펴봅니다.

    -   **비디오를 시청하려면.** 마법사를 보여 주고 Excel로 데이터를 내보내는 방법을 명료하고 간단하게 설명하는 4분 길이의 YouTube 동영상([SQL Server 가져오기 및 내보내기 마법사를 사용하여 Excel로 내보내기](https://go.microsoft.com/fwlink/?linkid=829049))을 시청합니다.

-   **마법사의 작동 원리에 대해 자세히 알아보기.**

    -   **마법사에 대해 자세히 알아봅니다.** 마법사에 대한 개요를 살펴보려면 [SQL Server 가져오기 및 내보내기 마법사를 사용하여 데이터 가져오기 및 내보내기](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)를 참조하세요.

    -   **마법사의 단계에 대해 자세히 알아보기** - 마법사의 단계에 대한 정보를 찾으려면 [SQL Server 가져오기 및 내보내기 마법사의 단계](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md)를 참조하세요. 또한 마법사의 각 페이지마다 별도의 설명서 페이지가 있습니다.

-   **마법사를 시작합니다.** 마법사 실행 준비를 마치고 시작하는 방법을 알고 싶으면 [SQL Server 가져오기 및 내보내기 마법사 시작](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)을 참조하세요.

-   **마법사를 가져옵니다.** 마법사를 실행하려고 하지만 컴퓨터에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 설치되지 않은 경우 SSDT(SQL Server Data Tools)를 설치하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 설치할 수 있습니다. 자세한 내용은 [SSDT(SQL Server Data Tools) 다운로드](../../ssdt/download-sql-server-data-tools-ssdt.md)를 참조하세요.

## <a name="see-also"></a>참고 항목
[데이터 원본 선택](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[대상 선택](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)