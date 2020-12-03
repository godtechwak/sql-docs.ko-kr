---
description: Microsoft Connector for Teradata
title: Microsoft Connector for Teradata | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a866d7d1083435acffeb157edf9fe4a0bb725d3e
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88425765"
---
# <a name="microsoft-connector-for-teradata"></a>Microsoft Connector for Teradata

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Microsoft Connector for Teradata를 사용하면 SSIS 패키지의 Teradata 데이터베이스에 데이터를 로드하고 데이터를 내보낼 수 있습니다.

이 새로운 커넥터는 1MB 사용 테이블이 포함된 데이터베이스를 지원합니다.

## <a name="version-support"></a>버전 지원

Microsoft Connector for Teradata에서 지원하는 Microsoft SQL Server 제품은 다음과 같습니다.

- Microsoft SQL Server 2019
- Visual Studio 2017용 Microsoft SQL Server Data Tools(SSDT) 15.8.1 이상
- Visual Studio 2019용 Microsoft SQL Server Data Tools(SSDT)

Microsoft Connector for Teradata는 Teradata Parallel Transporter 애플리케이션 프로그래밍 언어 인터페이스를 사용하여 Teradata 데이터베이스에 데이터를 로드하고 내보냅니다. 지원되는 버전은 다음과 같습니다.

- Teradata PT(Teradata Parallel Transporter) 16.10
- Teradata PT(Teradata Parallel Transporter) 16.20

지원되는 데이터 원본의 Teradata 데이터베이스 버전은 다음과 같습니다.

- Teradata 데이터베이스 16.20
- Teradata 데이터베이스 16.10
- Teradata 데이터베이스 15.10
- Teradata 데이터베이스 15.00

Teradata Parallel Transporter 애플리케이션 프로그래밍 인터페이스 프로그래머 가이드에 대한 자세한 내용은 [Teradata 문서](https://docs.teradata.com/)를 참조하세요.

## <a name="installation"></a>설치

32비트 컴퓨터에서는 [Teradata 도구 및 유틸리티 - Windows 설치 패키지](https://downloads.teradata.com/download/tools/teradata-tools-and-utilities-windows-installation-package)를 통해 다음 드라이버를 설치합니다.

- Teradata ODBC 드라이버(32비트)
- Teradata PT API(32비트)

64비트 컴퓨터에서는 다음 드라이버를 설치합니다.

- Teradata ODBC 드라이버(64비트)
- Teradata PT API(64비트)

Teradata 데이터베이스용 커넥터를 설치하려면 [최신 버전의 Microsoft Connector for Teradata](https://www.microsoft.com/download/details.aspx?id=100599)에서 설치 관리자를 다운로드하여 실행합니다. 그런 다음 설치 마법사의 지시를 따릅니다.

커넥터를 설치한 후에는 SQL Server Integration Services를 다시 시작해야 Teradata 원본 및 대상이 제대로 작동합니다.

## <a name="design-and-execute-ssis-packages"></a>SSIS 패키지 디자인 및 실행

Microsoft Connector for Teradata는 Attunity Teradata Connector와 유사한 사용자 환경을 제공합니다. 사용자는 SQL Server 2019를 대상으로 VS 2017 또는 VS 2019용 SSDT를 사용하여 이전 환경을 기반으로 새 패키지를 디자인할 수 있습니다.

Teradata 원본 및 대상이 공통 범주 아래에 있습니다.

![Teradata 구성 요소](media/teradata-component.png)

Teradata 연결 관리자가 "TERADATA"로 표시됩니다.

![Teradata 연결 관리자 유형](media/teradata-connection-manager-type.png)

Attunity Teradata Connector를 사용하여 디자인된 기존 SSIS 패키지는 Microsoft Connector for Teradata를 사용하도록 자동으로 업그레이드됩니다. 아이콘도 변경됩니다.

SQL Server 2017 및 이전 버전을 대상으로 하는 SSIS 패키지를 실행하려면 아래 링크에서 해당 버전과 함께 **Microsoft Connector for Teradata by Attunity** 를 설치해야 합니다.

- [SQL Server 2017: Microsoft Connector Version 5.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=55179)
- [SQL Server 2016: Microsoft Connector Version 4.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=52950)
- [SQL Server 2014: Microsoft Connector Version 3.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=44582)
- [SQL Server 2012: Microsoft Connector Version 2.0 for Teradata by Attunity](https://www.microsoft.com/download/details.aspx?id=29283)

SQL Server 2017 이하를 대상으로 SSDT에서 SSIS 패키지를 디자인하려면 **Microsoft Connector for Teradata** 를 사용하고 해당 버전의 **Microsoft Connector for Teradata by Attunity** 를 설치해야 합니다.

## <a name="limitations-and-known-issues"></a>제한 사항 및 알려진 문제

- Teradata 원본/대상 편집기, **기본 데이터베이스** 속성이 적용되지 않습니다.  해결하려면 드롭다운 상자에 데이터베이스 이름을 입력하여 테이블 또는 뷰를 필터링합니다.

- Teradata 원본/대상 편집기, 매핑 단계가 \<database>.<table/view> 형식일 때 작동하지 않습니다. 이 문제를 해결하려면 \<database>.<table/view>를 입력한 다음, 드롭다운 단추를 클릭합니다.

- Teradata 원본 편집기, 데이터 액세스 모드가 "테이블 이름 – TPT 내보내기"이면 뷰를 표시할 수 없습니다. 해결하려면 Teradata 원본 고급 편집기를 사용합니다.

- Teradata 대상, 'PackMaximum' 특성을 'True'로 설정할 수 없습니다.  설정하는 경우 오류가 발생합니다.

## <a name="uninstallation"></a>제거

제거 마법사를 실행하여 **Microsoft connector for Teradata** 를 제거할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [Teradata 연결 관리자](teradata-connection-manager.md) 구성
- [Teradata 원본](teradata-source.md) 구성
- [Teradata 대상](teradata-destination.md) 구성
- 질문이 있는 경우 [Tech Community](https://aka.ms/AA6iwdw)를 방문하세요.
