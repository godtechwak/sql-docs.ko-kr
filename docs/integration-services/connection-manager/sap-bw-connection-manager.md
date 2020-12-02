---
description: SAP BW 연결 관리자
title: SAP BW 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 06b166a1-a9df-48ea-a0e8-9b8d6979c0a1
f1_keywords:
- sql13.dts.designer.sapbwconnectionmanager.f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6e09a6cdf6f8d863e57d2de0749e29b33c989eea
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91719581"
---
# <a name="sap-bw-connection-manager"></a>SAP BW 연결 관리자

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  SAP BW 연결 관리자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 연결 관리자 구성 요소입니다. 따라서 SAP BW 연결 관리자는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 원본 및 대상 구성 요소에 필요한 SAP Netweaver BW 버전 7 시스템에 대한 연결을 제공합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW 패키지의 일부인 SAP BW 원본 및 대상은 SAP BW 연결 관리자를 사용하는 유일한 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 구성 요소입니다.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
 SAP BW 연결 관리자를 패키지에 추가하면 연결 관리자의 **ConnectionManagerType** 속성이 **SAPBI** 로 설정됩니다.  
  
## <a name="configuring-the-sap-bw-connection-manager"></a>SAP BW 연결 관리자 구성  
 다음과 같은 방법으로 SAP BW 연결 관리자를 구성할 수 있습니다.  
  
-   연결에 대한 클라이언트, 사용자 이름, 암호 및 언어를 제공합니다.  
  
-   단일 애플리케이션 서버에 연결할지 아니면 부하 분산 서버의 그룹에 연결할지를 선택합니다.  
  
-   단일 애플리케이션 서버의 호스트 및 시스템 번호를 제공하거나 부하 분산 서버 그룹의 메시지 서버, 그룹 및 SID를 제공합니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 구성 요소에 대한 RFC 함수 호출의 사용자 지정 로깅을 사용하도록 설정합니다. 이 로깅은 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에서 사용하도록 설정할 수 있는 선택적 로깅과 별개입니다. RFC 함수 호출의 로깅을 사용하도록 설정하려면 각 RFC 함수 호출 전후에 생성되는 로그 파일을 저장할 디렉터리를 지정합니다. 이 로깅 기능을 사용하면 XML 형식의 로그 파일이 많이 만들어집니다. 로그 파일에는 전송되는 모든 데이터 행도 포함되므로 많은 디스크 공간이 소비될 수 있습니다. 로그 디렉터리를 선택하지 않으면 로깅이 사용되지 않습니다.  
  
    > [!IMPORTANT]  
    >  전송되는 데이터에 중요한 정보가 포함되어 있는 경우 로그 파일에도 해당 정보가 포함됩니다.  
  
-   입력한 값을 사용하여 연결을 테스트합니다.  
  
 연결 관리자를 구성하는 데 필요한 값 중 모르는 것이 있으면 SAP 관리자에게 문의하십시오.  
  
 SAP BW 연결 관리자, 원본 및 대상을 구성하고 사용하는 방법을 제시하는 연습은 [SAP BI 7.0에서 SQL Server 2008 Integration Services 사용](/previous-versions/sql/sql-server-2008/dd299430(v=sql.100))백서를 참조하십시오. 또한 이 백서는 SAP BW에 필요한 개체를 구성하는 방법을 보여 줍니다.  
  
### <a name="using-the-ssis-designer-to-configure-the-source"></a>SSIS 디자이너를 사용하여 원본 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 SAP BW 연결 관리자의 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [SAP BW 연결 관리자 편집기]()  
  
## <a name="sap-bw-connection-manager-editor"></a>SAP BW 연결 관리자 편집기
  **SAP BW 연결 관리자 편집기** 를 사용하여 SAP Netweaver BW 버전 7 시스템에 연결하는 데 사용할 속성을 지정할 수 있습니다.  
  
 SAP BW 연결 관리자는 SAP 원본 또는 대상에서 SAP Netweaver BW 7 시스템에 연결할 수 있도록 해 줍니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 SAP BW 연결 관리자에 대한 자세한 내용은 [SAP BW 연결 관리자](../../integration-services/connection-manager/sap-bw-connection-manager.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
 **SAP BW 연결 관리자 편집기를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 연결 관리자가 포함된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **제어 흐름** 탭의 연결 관리자 영역에서 다음 단계 중 하나를 수행합니다.  
  
    -   SAP BW 연결 관리자를 두 번 클릭합니다.  
  
         또는  
  
    -   SAP BW 연결 관리자를 마우스 오른쪽 단추로 클릭한 다음 **편집** 을 선택합니다.  
  
### <a name="options"></a>옵션  
  
> [!NOTE]  
>  연결 관리자를 구성하는 데 필요한 값 중 모르는 것이 있으면 SAP 관리자에게 문의하십시오.  
  
 **클라이언트**  
 시스템의 클라이언트 번호를 지정합니다.  
  
 **언어**  
 시스템에서 사용하는 언어를 지정합니다. 예를 들어, 영어의 경우 **EN** 을 지정합니다.  
  
 **사용자 이름**  
 시스템에 연결하는 데 사용할 사용자 이름을 지정합니다.  
  
 **암호**  
 사용자 이름에 사용할 암호를 지정합니다.  
  
 **단일 애플리케이션 서버 사용**  
 단일 애플리케이션 서버에 연결합니다.  
  
 부하 분산 서버 그룹에 연결하려면 **부하 분산 사용** 옵션을 사용합니다.  
  
 **Host**  
 단일 애플리케이션 서버에 연결하는 경우 호스트 이름을 지정합니다.  
  
> [!NOTE]  
>  이 옵션은 **단일 애플리케이션 서버 사용** 옵션을 선택한 경우에만 사용할 수 있습니다.  
  
 **시스템 번호**  
 단일 애플리케이션 서버에 연결하는 경우 시스템 번호를 지정합니다.  
  
> [!NOTE]  
>  이 옵션은 **단일 애플리케이션 서버 사용** 옵션을 선택한 경우에만 사용할 수 있습니다.  
  
 **부하 분산 사용**  
 부하 분산된 서버 그룹에 연결합니다.  
  
 단일 애플리케이션 서버에 연결하려면 **단일 애플리케이션 서버 사용** 옵션을 사용합니다.  
  
 **메시지 서버**  
 부하 분산된 서버 그룹에 연결하는 경우 메시지 서버의 이름을 지정합니다.  
  
> [!NOTE]  
>  이 옵션은 **부하 분산 사용** 옵션을 선택한 경우에만 사용할 수 있습니다.  
  
 **그룹**  
 부하 분산된 서버 그룹에 연결하는 경우 서버 그룹 이름을 지정합니다.  
  
> [!NOTE]  
>  이 옵션은 **부하 분산 사용** 옵션을 선택한 경우에만 사용할 수 있습니다.  
  
 **SID**  
 부하 분산된 서버 그룹에 연결하는 경우 연결에 대한 시스템 ID를 지정합니다.  
  
> [!NOTE]  
>  이 옵션은 **부하 분산 사용** 옵션을 선택한 경우에만 사용할 수 있습니다.  
  
 **로그 디렉터리**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW의 구성 요소에 대한 로깅을 사용하도록 설정합니다.  
  
 로깅을 사용하도록 설정하려면 각 RFC 함수 호출 전후에 생성되는 로그 파일에 대한 디렉터리를 지정합니다. 이 로깅 기능을 사용하면 XML 형식의 로그 파일이 많이 만들어집니다. 로그 파일에는 전송되는 모든 데이터 행도 포함되므로 많은 디스크 공간이 소비될 수 있습니다.  
  
> [!IMPORTANT]  
>  전송되는 데이터에 중요한 정보가 포함되어 있는 경우 로그 파일에도 해당 정보가 포함됩니다.  
  
 로그 디렉터리를 지정하려면 디렉터리 경로를 수동으로 입력하거나 **찾아보기** 를 클릭하여 로그 디렉터리를 찾아봅니다.  
  
 로그 디렉터리를 선택하지 않으면 로깅이 사용되지 않습니다.  
  
 **찾아보기**  
 로그 디렉터리로 사용할 폴더를 찾아봅니다.  
  
 **연결 테스트**  
 사용자가 제공한 값을 사용하여 연결을 테스트합니다. **연결 테스트** 를 클릭하면 메시지 상자가 표시되고 연결이 성공했는지 여부가 표시됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Microsoft Connector for SAP BW 구성 요소](../../integration-services/microsoft-connector-for-sap-bw-components.md)  
  
