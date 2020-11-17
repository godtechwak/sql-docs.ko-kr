---
description: SQL Server 개인 정보 제공
title: SQL Server 개인 정보 제공 | Microsoft Docs
ms.date: 11/11/2020
ms.prod: sql
ms.technology: release-landing
ms.reviewer: wopeter
ms.custom: ''
ms.topic: conceptual
f1_keywords: ''
helpviewer_keywords: ''
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 87cd9ec5266002f91fea682591e82dfecd403ab5
ms.sourcegitcommit: 4545b502e3cae7136411fd9a7c15450315665f38
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/12/2020
ms.locfileid: "94550007"
---
# <a name="sql-server-privacy-supplement"></a>SQL Server 개인 정보 제공

[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

이 문서에서는 익명 기능 사용 및 진단 데이터를 수집하고 Microsoft에 보낼 수 있는 인터넷 사용 기능을 요약해서 설명합니다. SQL Server는 표준 컴퓨터 정보와 사용 및 성능 데이터를 수집할 수 있습니다. 이 데이터는 Microsoft로 전송되어 제품의 품질, 보안 및 안정성 개선을 위해 분석될 수 있습니다. Microsoft Azure 서비스의 가상 머신에 SQL Server를 설치하면 Microsoft가 가상 머신에 SQL Server IaaS 에이전트 확장을 설치하고 [여기](/azure/azure-sql/virtual-machines/windows/sql-vm-resource-provider-register) 설명된 것처럼 SQL VM 리소스 공급자에 SQL 가상 머신 리소스를 등록할 수 있도록 Microsoft에 환경 정보가 전송됩니다.

이 문서는 전반적인 [Microsoft 개인정보처리방침](https://go.microsoft.com/fwlink/?LinkId=521839)에 대한 추록입니다. 이 문서에서 데이터 분류는 SQL Server 온-프레미스 제품의 버전에만 적용됩니다. 항목에 적용되지 않습니다.

- Azure SQL Database
- [SSMS(SQL Server Management Studio)](../ssms/sql-server-management-studio-telemetry-ssms.md)
- SQL Server Data Tools(SSDT)
- Azure Data Studio
- Database Migration Assistant
- SQL Server Migration Assistant
- MS-SQL 확장

*허용된 사용 시나리오* 의 정의입니다. Microsoft는 이 문서의 컨텍스트에서 Microsoft에서 시작된 작업이나 작업으로 "허용된 사용 시나리오"를 정의합니다.

## <a name="access-control"></a>Access Control

SQL Server 설치 내에서 로그인, 사용자 또는 계정을 보호하는 데 사용되는 자격 증명 관련 정보입니다.

### <a name="examples-of-access-control"></a>액세스 제어의 예제

- 암호
- 인증서

### <a name="permitted-usage-scenarios"></a>허용된 사용 시나리오

|시나리오 |액세스 제한 |보존 요구 사항 |
|---------|---------|---------|
|이러한 자격 증명은 사용 및 진단 데이터를 통해 사용자 머신에서 나가지 않습니다. |- |- |
|크래시 덤프는 액세스 제어 데이터를 포함할 수 있습니다. |- |크래시 덤프: 최대 30일입니다. |
|고객이 수동으로 삽입하지 않으면 이러한 자격 증명은 사용자 피드백을 통해 사용자 컴퓨터를 벗어나지 않습니다. |타사 액세스 권한 없이 Microsoft 내부 사용량을 제한합니다. |사용자 피드백: 최대 1년|
|&nbsp;|&nbsp;|&nbsp;|

## <a name="customer-data"></a>고객 데이터

고객 데이터는 직접 또는 간접적으로 사용자 테이블 내에 저장된 데이터로 정의됩니다. 데이터에는 사용자 테이블 내에 저장될 수 있는 쿼리 텍스트 내의 통계 또는 사용자 리터럴이 포함됩니다.

### <a name="examples-of-customer-data"></a>고객 데이터의 예

- 사용자 테이블의 행 내에 저장된 데이터 값입니다.
- 사용자 테이블의 행 내에서 값의 복사본을 포함하는 통계 개체입니다.
- 리터럴 값이 포함된 텍스트를 쿼리합니다.

### <a name="permitted-usage-scenarios"></a>허용된 사용 시나리오

|시나리오  |액세스 제한  |보존 요구 사항 |
|---------|---------|---------|
|이 데이터는 사용 및 진단 데이터를 통해 사용자 머신에서 나가지 않습니다. |- |- |
|크래시 덤프는 고객 데이터를 포함하고 Microsoft로 내보내질 수 있습니다. |- |크래시 덤프: 최대 30일입니다. |
|동의하는 고객은 고객 데이터가 포함된 사용자 피드백을 Microsoft에 보낼 수 있습니다. |타사 액세스 권한 없이 Microsoft 내부를 제한합니다. Microsoft에서는 원래 고객에게 데이터를 노출할 수 있습니다. |사용자 피드백: 최대 1년 |

## <a name="personal-data"></a>개인 데이터

사용자로부터 받거나 제품을 사용하여 생성된 데이터입니다.
- 개별 사용자에게 연결 가능합니다.
- 고객 데이터가 포함되지 않습니다.

### <a name="examples-of-personal-data"></a>개인 데이터의 예

- 인터페이스 식별 전체 IP 주소
- 컴퓨터 이름
- 로그인/사용자 이름
- 이메일 주소의 로컬 부분(joe@contoso.com)
- 위치 정보
- 고객 ID

### <a name="permitted-usage-scenarios"></a>허용된 사용 시나리오

|시나리오  |액세스 제한  |보존 요구 사항|
|---------|---------|---------|
|이 데이터는 사용 및 진단 데이터를 통해 사용자 머신에서 나가지 않습니다. |- |- |
|크래시 덤프는 개인 데이터를 포함하고 Microsoft로 내보내질 수 있습니다. |- |크래시 덤프: 최대 30일 |
|고객 식별 ID를 Microsoft에 내보내서 사용자가 구독하는 새로운 하이브리드 및 클라우드 기능을 제공할 수 있습니다. |- |현재 이러한 하이브리드 또는 클라우드 기능이 존재하지 않습니다.|
|동의하는 고객은 고객 데이터가 포함된 사용자 피드백을 Microsoft에 보낼 수 있습니다.|타사 액세스 권한 없이 Microsoft 내부 사용량을 제한합니다. Microsoft에서는 원래 고객에게 데이터를 노출할 수 있습니다. |사용자 피드백: 최대 1년 |

## <a name="internet-based-services-data"></a>인터넷 기반 서비스 데이터

SQL Server EULA당 인터넷 기반 서비스를 제공하는 데 필요한 데이터입니다.

### <a name="examples-of-internet-based-services-data"></a>인터넷 기반 서비스 데이터의 예제

- 컴퓨터 사양 정보
- 브라우저 이름/버전
- SQL Server 버전
- 언어 코드
- 특정 옥텟이 제거된 IP 주소
- 맵 데이터

### <a name="permitted-usage-scenarios"></a>허용된 사용 시나리오

|시나리오  |액세스 제한  |보존 요구 사항|
|---------|---------|---------| 
|현재 기능에서 기능 개선 및/또는 버그 수정을 수행하기 위해 Microsoft에서 사용할 수 있습니다. |타사 액세스 권한 없이 Microsoft 내부 사용량을 제한합니다. Microsoft에서는 원래 고객에게 데이터를 노출할 수 있습니다.  예: 대시보드 |최소 90일 - 최대 3년 |
|동의하는 고객은 고객 데이터가 포함된 사용자 피드백을 Microsoft에 보낼 수 있습니다. |타사 액세스 권한 없이 Microsoft 내부 사용량을 제한합니다. |동의하는 고객은 고객 데이터가 포함된 사용자 피드백을 Microsoft에 보낼 수 있습니다. |
|파워 뷰 및 SQL Reporting Services Map 항목은 Bing Maps를 사용하기 위해 데이터를 전송할 수 있습니다. |세션 데이터에 대한 제한 사항 |- |

## <a name="non-personal-data"></a>비개인 데이터

1. 조직으로부터 받거나 제품을 사용하여 생성된 데이터입니다. 해당 데이터는 조직에 연결할 수 있으며 고객 데이터를 포함하지 않습니다.

   - 예제
     - 조직 이름(예: Microsoft Corp.)

   - 허용된 사용 시나리오

     |시나리오  |액세스 제한  |보존 요구 사항|
     |---------|---------|---------|
     | Microsoft는 Azure Virtual Machines 내에서 SQL Server를 사용할 수 있도록 Azure에서 고객에게 선택적 혜택을 제공하는 명시적 목적으로 Azure Virtual Machines에서 실행되는 SQL Server 인스턴스의 일반 사용량 현황 데이터를 수집할 수 있습니다. | Microsoft는 Azure Portal 등을 통해 고객에게 데이터를 노출하여 Azure Virtual Machines에서 SQL Server를 실행하는 고객이 Azure에서 실행 중인 SQL Server와 관련된 혜택에 액세스할 수 있도록 지원합니다. </br></br>Microsoft는 고객의 사전 동의 없이는 라이선스 감사에 이 데이터를 사용하지 않습니다. | 최소 90일 - 최대 3년 |

2. 서버, 데이터베이스, 테이블 및 고객이 만들거나 제공하는 기타 리소스를 구성하는 작업을 설명하거나 이러한 작업에 사용되는 데이터입니다. 해당 데이터는 데이터베이스 테이블 및 열 이름을 포함하지만 데이터베이스 행의 콘텐츠 또는 기타 고객 데이터는 포함하지 않습니다. 고객은 해당 필드에 어떠한 개인 데이터도 배치하지 않아야 합니다. 또는 해당 필드에 개인 데이터를 저장하도록 설계된 애플리케이션을 만들지 않아야 합니다. 아래의 허용된 사용 시나리오의 경우 제품 개선을 위한 사용 패턴을 결정할 때 해시 양식만 사용됩니다.

   - 예제
      - SQL Server 데이터베이스 이름
      - 테이블 이름 및 열 이름
      - 통계 이름

    - 허용된 사용 시나리오

      > [!NOTE]
      > 모든 메타데이터 값은 수집 전에 해시됩니다.
      >

      |시나리오  |액세스 제한  |보존 요구 사항|
      |---------|---------|---------|
      |현재 기능에서 기능 개선 및/또는 버그 수정을 수행하기 위해 Microsoft에서 사용할 수 있습니다. |타사 액세스 권한 없이 Microsoft 내부 사용량을 제한합니다. |최소 90일 - 최대 3년|

3. 서버를 실행하는 과정에서 생성된 데이터입니다. 해당 데이터는 1. 또는 2.(위)에 나열된 고객 데이터, 비개인 데이터와 고객 액세스 제어 데이터 또는 개인 데이터를 포함하지 않습니다.

   - 예제
     - 데이터베이스 GUID
     - 컴퓨터 이름 해시
     - 인스턴스 이름 해시
     - 애플리케이션 이름
     - 동작/사용량 데이터
     - SQLCEIP(SQL 사용자 환경 개선 프로그램) 데이터
     - 서버 구성 데이터(예: sp_configure)
     - 기능 구성 데이터
     - 이벤트 이름 및 오류 코드
     - 하드웨어 설정 및 식별(예: OEM 제조업체)

   Microsoft는 SQL Server를 사용하는 다른 프로그램에서 설정된 애플리케이션 이름 값 집합을 검사합니다(예: SharePoint 또는 타사 패키지 프로그램, 사용량 현황 데이터를 사용하도록 설정된 경우 Microsoft에 전송되는 메타데이터 필드에 이 정보가 포함됨). 고객은 해당 메타데이터 필드에 개인 데이터를 배치하지 않아야 합니다. 또는 해당 필드에 개인 데이터를 저장하도록 설계된 애플리케이션을 만들지 않아야 합니다.

   - 허용된 사용 시나리오

     |시나리오  |액세스 제한  |보존 요구 사항|
     |---------|---------|---------|
     |현재 기능에서 기능 개선 및/또는 버그 수정을 수행하기 위해 Microsoft에서 사용할 수 있습니다.|타사 액세스 권한 없이 Microsoft 내부 사용량을 제한합니다. |최소 90일 - 최대 3년 |
     |고객에게 제안하는 데 사용할 수 있습니다.  예를 들어 "제품의 사용량에 따라 성능이 향상되기 때문에 기능 *X* 를 사용하는 것이 좋습니다." |Microsoft에서는 원래 고객에게 데이터를 노출할 수 있습니다(예: 대시보드를 통해). |고객 데이터 보안 로그: 최소 3년 - 최대 6년 |
     |향후 제품 계획을 위해 Microsoft에서 사용할 수 있습니다. |Microsoft는 해당 제품이 Microsoft 소프트웨어로 실행되는 방법을 개선하기 위해 다른 하드웨어 및 소프트웨어 공급 업체와 이 정보를 공유할 수 있습니다. |최소 90일 - 최대 3년|
     |내보낸 사용 및 진단 데이터에 따라 클라우드 기반 서비스를 제공하기 위해 Microsoft에서 사용할 수 있습니다. 예를 들어 고객 대시보드는 조직에서 설치된 모든 SQL Server에 대한 기능 사용량을 표시합니다. |Microsoft에서는 원래 고객에게 데이터를 노출할 수 있습니다(예: 대시보드를 통해). |최소 90일 - 최대 3년 |
     |동의하는 고객은 고객 데이터가 포함된 사용자 피드백을 Microsoft에 보낼 수 있습니다. |타사 액세스 권한 없이 Microsoft 내부를 제한합니다. Microsoft에서는 원래 고객에게 데이터를 노출할 수 있습니다. |사용자 피드백: 최대 1년 |
     |데이터베이스 이름과 애플리케이션 이름을 사용하여 데이터베이스와 애플리케이션을 알려진 범주(예: Microsoft 또는 다른 회사에서 제공하는 소프트웨어를 실행하는 범주)로 분류할 수 있습니다.|타사 액세스 권한 없이 Microsoft 내부를 제한합니다.|최소 90일 - 최대 3년 |

## <a name="system-generated-logs-controls"></a>시스템 생성 로그 제어

제품에서 시스템 생성 로그를 설정/해제하는 방법에 대한 지침은 [SQL Server(CEIP) 사용 현황 및 진단 데이터 수집 구성](usage-and-diagnostic-data-configuration-for-sql-server.md)에서 참조할 수 있습니다.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
