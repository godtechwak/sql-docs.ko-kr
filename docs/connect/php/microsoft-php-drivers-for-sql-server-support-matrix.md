---
title: Microsoft Drivers for PHP 지원 매트릭스
description: 이 페이지에는 Microsoft PHP Driver for SQL Server에 대한 지원 매트릭스 및 지원 드라이버에 대한 지원 주기 정책이 포함되어 있습니다.
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 778d9aa4ee666ba3719095508d5f5e28516f954d
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942162"
---
# <a name="microsoft-php-drivers-for-sql-server-support-matrix"></a>Microsoft PHP Drivers for SQL Server 지원 매트릭스

[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

이 페이지에는 Microsoft PHP Driver for SQL Server에 대한 지원 매트릭스 및 지원 드라이버에 대한 지원 주기 정책이 포함되어 있습니다.

## <a name="microsoft-php-drivers-support-lifecycle-matrix-and-policy"></a>Microsoft PHP Drivers 지원 수명 주기 매트릭스 및 정책

MSL(Microsoft 지원 수명 주기) 정책은 Microsoft 제품 지원 수명 주기와 관련해서 투명하고 예측 가능한 정보를 제공합니다. PHP Driver 버전 3.x, 4.x 및 5.x는 드라이버 릴리스 날짜로부터 5년 동안 일반 지원을 제공합니다. 일반 지원은 [Microsoft 지원 수명 주기 웹 사이트](https://support.microsoft.com/lifecycle)에 정의되어 있습니다.

확장 및 사용자 지정 지원 옵션은 Microsoft PHP Driver에는 사용할 수 없습니다.

다음 Microsoft PHP Driver는 지정된 지원 종료 날짜까지 지원됩니다.

|드라이버 이름|드라이버 패키지 버전|일반 지원 종료|
|-|:-:|-|
|Microsoft PHP Drivers 5.8 for SQL Server|5.8|2025년 1월 31일|
|Microsoft PHP Drivers 5.6 for SQL Server|5.6|2024년 2월 21일|
|Microsoft PHP Drivers 5.3 for SQL Server|5.3|2023년 7월 20일|
|Microsoft PHP Drivers 5.2 for SQL Server|5.2|2023년 2월 9일|
|Microsoft PHP Drivers 4.3 for SQL Server|4.3|2022년 7월 6일|
|Microsoft PHP Drivers 4.0 for SQL Server|4.0|2021년 7월 11일|
|Microsoft PHP Drivers 3.2 for SQL Server|3.2|2020년 3월 9일|
| &nbsp; | &nbsp; | &nbsp; |

다음 Microsoft PHP Driver는 더 이상 지원되지 않습니다.

|드라이버 이름|드라이버 패키지 버전|일반 지원 종료|
|-|:-:|-|
|Microsoft PHP Drivers 3.1 for SQL Server|3.1|2019년 12월 12일|
|Microsoft PHP Drivers 3.0 for SQL Server|3.0|2017년 3월 6일|
|Microsoft PHP Drivers 2.0 for SQL Server|2.0|2015년 8월 10일|
|Microsoft PHP Drivers 1.0 for SQL Server|1.0|2014년 4월 28일|
| &nbsp; | &nbsp; | &nbsp; |

## <a name="sql-server-version-certified-compatibility"></a>SQL Server 버전 인증 호환성
 다음 매트릭스에는 테스트를 통해 해당 드라이버 버전과 호환되는 것으로 인증된 데이터베이스 버전이 나열되어 있습니다. 이전 드라이버 버전과의 호환성을 유지하기 위해 노력하고 있지만 SQL Server가 출시될 때 최신 지원 드라이버는 새 SQL Server 버전에서만 테스트하고 인증됩니다.

|드라이버 버전&nbsp;&#8594;<br />&#8595; 데이터베이스 버전|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Azure SQL Database        |예|예|예|예|예|   |   |
|Azure SQL Managed Instance|yes|예|예|예|예|   |   |
|Azure Synapse Analytics   |예|예|예|예|예|   |   |
|SQL Server 2019           |예|   |   |   |   |   |   |
|SQL Server 2017           |예|예|예|예|예|   |   |
|SQL Server 2016           |예|예|예|예|예|예|   |
|SQL Server 2014           |예|예|예|예|예|예|예|
|SQL Server 2012           |예|예|예|예|예|예|예|
|SQL Server 2008 R2        |   |예|예|예|예|예|예|
|SQL Server 2008           |   |   |   |   |   |예|예|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

Azure SQL Database에서 PHP를 사용하는 방법에 대한 자세한 내용은 [Microsoft Azure SQL Database에 연결](connecting-to-microsoft-azure-sql-database.md)을 참조하세요.

## <a name="php-version-support"></a>PHP 버전 지원

다음 버전의 PHP는 나열된 버전의 Microsoft PHP Drivers에서 지원됩니다.

|드라이버 버전&nbsp;&#8594;<br />&#8595; PHP 버전|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|:---:|---|---|---|---|---|---|---|
|7.4|7.4.0+          |                |                |                |       |        |        |
|7.3|7.3.0+          |7.3.0+          |                |                |       |        |        |
|7.2|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|7.2+<sup>1</sup>|       |        |        |
|7.1|                |7.1.0+          |7.1.0+          |7.1.0+          |7.1.0+ |        |        |
|7.0|                |                |7.0.0+          |7.0.0+          |7.0.0+ |7.0.0+  |        |
|5.6|                |                |                |                |       |        |5.6.4+  |
|5.5|                |                |                |                |       |        |5.5.16+ |
|5.4|                |                |                |                |       |        |5.4.32  |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

1. Windows에서는 버전 7.2.1 이상이 지원되고, Linux 및 macOS에서는 버전 7.2.0 이상이 지원됩니다.

## <a name="supported-operating-systems"></a>지원되는 운영 체제

다음 Windows 운영 체제 버전이 나열된 버전의 Microsoft PHP Drivers에서 지원됩니다.

|드라이버 버전&nbsp;&#8594;<br />&#8595; 운영 체제|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Windows Server 2019                 |예|예|   |   |   |   |   |
|Windows Server 2016                 |예|예|예|예|예|   |   |
|Windows Server 2012 R2              |예|예|예|예|예|예|예|
|Windows Server 2012                 |예|예|예|예|예|예|예|
|Windows Server 2008 R2 SP1          |   |   |   |   |   |예|예|
|Windows Server 2008 R2              |   |   |   |   |   |   |   |
|Windows Server 2008 SP2             |   |   |   |   |   |예|예|
|Windows 10                          |예|예|예|예|예|예|   |
|Windows 8.1                         |예|예|예|예|예|예|예|
|Windows 8                           |   |   |   |   |예|예|예|
|Windows 7 SP1                       |   |   |   |   |   |예|예|
|Windows Vista SP2                   |   |   |   |   |   |예|예|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

다음 Linux 및 macOS 운영 체제 버전(64비트만 해당)은 나열된 Microsoft PHP Drivers 버전에서 지원됩니다.

|드라이버 버전&nbsp;&#8594;<br />&#8595; 운영 체제|5.8|5.6|5.3|5.2|4.3|4.0|3.2|
|--|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|Ubuntu 20.04(64비트)               |예|   |   |   |   |   |   |
|Ubuntu 19.10(64비트)               |예|   |   |   |   |   |   |
|Ubuntu 18.10(64비트)               |   |예|   |   |   |   |   |
|Ubuntu 18.04(64비트)               |예|예|예|   |   |   |   |
|Ubuntu 17.10(64비트)               |   |   |예|예|   |   |   |
|Ubuntu 16.04(64비트)               |예|예|예|예|예|예|   |
|Ubuntu 15.10(64비트)               |   |   |   |   |예|   |   |
|Ubuntu 15.04(64비트)               |   |   |   |   |   |예|   |
|Debian 10(64비트)                  |예|   |   |   |   |   |   |
|Debian 9(64비트)                   |예|예|예|예|   |   |   |
|Debian 8(64비트)                   |예|예|예|예|예|   |   |
|Red Hat Enterprise Linux 8(64비트) |예|   |   |   |   |   |   |
|Red Hat Enterprise Linux 7(64비트) |예|예|예|예|예|예|   |
|Suse Enterprise Linux 15(64 비트)   |예|예|   |   |   |   |   |
|Suse Enterprise Linux 12(64비트)   |예|예|예|예|   |   |   |
|Alpine Linux 3.11(64비트)<sup>1</sup>|예|   |   |   |   |   |   |
|macOS Catalina(64비트)             |예|   |   |   |   |   |   |
|macOS Mojave(64비트)               |예|예|   |   |   |   |   |
|macOS High Sierra(64비트)          |예|예|예|   |   |   |   |
|macOS Sierra(64비트)               |   |예|예|예|예|   |   |
|macOS El Capitan(64비트)           |   |   |예|예|예|   |   |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<sup>1</sup> Alpine Linux 지원은 버전 5.8.0에서 실험적입니다. 버전 5.8.1은 프로덕션 지원을 도입합니다.

## <a name="see-also"></a>참고 항목

[릴리스 정보](release-notes-php-sql-driver.md)

[지원 리소스](support-resources-for-the-php-sql-driver.md)

[시스템 요구 사항](system-requirements-for-the-php-sql-driver.md)
