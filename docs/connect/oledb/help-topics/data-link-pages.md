---
title: UDL(유니버설 데이터 링크) 구성 | Microsoft Docs
description: 연결 탭에서 OLE DB Driver for SQL Server를 사용하여 데이터에 연결하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: f8d9444864dfe144918374c6d10e1a9f403faff3
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96504736"
---
# <a name="universal-data-link-udl-configuration"></a>UDL(유니버설 데이터 링크) 구성
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="connection-tab"></a>연결 탭
연결 탭에서 Microsoft OLE DB Driver for SQL Server를 사용하여 데이터에 연결하는 방법을 지정할 수 있습니다.

![OLE DB 데이터 링크 페이지 - 연결 탭의 스크린샷](../media/data-link-pages-connection-tab.png)

이 연결 탭은 공급자별 옵션이며 Microsoft OLE DB Driver for SQL Server에 필요한 연결 속성만 표시합니다.

|옵션|Description|
|---   |---        |
|서버 이름 선택 또는 입력|드롭다운 목록에서 서버 이름을 선택하거나 액세스할 데이터베이스가 있는 서버의 위치를 입력합니다. 서버에서 데이터베이스를 선택하는 것은 별개의 동작입니다. “새로 고침”을 클릭하여 목록을 업데이트합니다.
|서버 로그인 정보 입력|이 드롭다운 목록에서 다음 인증 옵션을 선택할 수 있습니다. <ul><li>`Windows Authentication:` 현재 로그인한 사용자의 Windows 계정 자격 증명을 사용하는 SQL Server 인증입니다.</li><li>`SQL Server Authentication:` 로그인 ID 및 암호를 사용하는 인증입니다.</li><li>`Active Directory - Integrated:` Azure Active Directory ID를 사용하는 통합 인증입니다. 이 모드는 SQL Server에 대한 Windows 인증에도 사용할 수 있습니다.</li><li>`Active Directory - Password:` Azure Active Directory ID를 사용하는 사용자 ID 및 암호 인증입니다.</li><li>`Active Directory - Universal with MFA support:` Azure Active Directory ID를 사용하는 대화형 인증입니다. 이 모드는 Azure MFA(다단계 인증)를 지원합니다.</li><li>`Active Directory - Service Principal:` Azure Active Directory 서비스 사용자로 인증. **사용자 이름** 은 애플리케이션(클라이언트) ID로 설정해야 합니다. **암호** 는 애플리케이션(클라이언트) 비밀로 설정해야 합니다.</li></ul>|
|서버 SPN|트러스트된 연결을 사용하면 서버에 대한 SPN(서비스 사용자 이름)을 지정할 수 있습니다.|
|사용자 이름|데이터 원본에 로그인할 때 인증에 사용할 사용자 ID를 입력합니다.|
|암호|데이터 원본에 로그인할 때 인증에 사용할 암호를 입력합니다.|
|빈 암호|이 확인란을 선택하면 지정된 공급자가 연결 문자열에 빈 암호를 사용할 수 있습니다.|
|암호 저장 허용|이 확인란을 선택하면 연결 문자열을 사용하여 암호를 저장할 수 있습니다. 암호가 연결 문자열에 포함되는지 여부는 호출 애플리케이션의 기능에 따라 달라집니다. <br/><br/>**참고:** 저장되면 암호는 마스크되거나 암호화되지 않고 반환 및 저장됩니다.|
|데이터에 대하여 강력한 암호화 사용|이 확인란을 선택하면 연결을 통해 전달되는 데이터가 암호화됩니다.|
|서버 인증서 신뢰|이 확인란을 선택하면 서버 인증서의 유효성이 검사됩니다. 서버 인증서에는 올바른 서버 호스트 이름이 있어야 하며 신뢰할 수 있는 인증 기관에서 발급한 인증서가 있어야 합니다.|
|데이터베이스 선택|액세스하려는 데이터베이스 이름을 선택하거나 입력합니다.|
|데이터베이스 파일을 데이터베이스 이름으로 연결|연결할 수 있는 데이터베이스에 대한 주 파일의 이름을 지정합니다. 이 데이터베이스는 데이터 원본에 대한 기본 데이터베이스로 연결되어 사용됩니다. 이 섹션의 첫 번째 텍스트 상자에 연결된 데이터베이스 파일에 사용할 데이터베이스 이름을 입력합니다.<br/><br/>`Using the filename`이라는 텍스트 상자에 연결할 데이터베이스 파일의 전체 경로를 입력하거나 `...` 단추를 클릭하여 데이터베이스 파일을 찾습니다.|
|암호 변경|SQL Server 암호 변경 대화 상자를 표시합니다. |
|연결을 테스트|클릭하면 지정된 데이터 원본에 대한 연결을 시도합니다. 연결이 실패할 경우 설정이 올바른지 확인하십시오. 예를 들어 맞춤법 오류 및 대/소문자 구분으로 인해 연결이 실패할 수 있습니다.|

## <a name="advanced-tab"></a>고급 탭
고급 탭을 사용하여 추가 초기화 속성을 보고 설정할 수 있습니다.

![OLE DB 데이터 링크 페이지 - 고급 탭의 스크린샷](../media/data-link-pages-advanced-tab.png)

|옵션|Description|
|---   |---        |
| Connect timeout | 초기화가 완료될 때까지 Microsoft OLE DB Driver for SQL Server가 대기하는 시간(초)을 지정합니다. 초기화가 제한 시간을 초과하면 오류가 반환되며 연결이 만들어지지 않습니다.|


> [!NOTE]  
>  데이터 링크 연결에 대한 자세한 내용은 [데이터 링크 API 개요](/previous-versions/windows/desktop/ms718102(v=vs.85))를 참조하세요.

## <a name="next-steps"></a>다음 단계
- OLE DB 드라이버를 사용하여 [Azure Active Directory에 인증](../features/using-azure-active-directory.md)합니다.

- OLE DB 드라이버를 사용하여 [인증 자격 증명을 묻는 메시지를 표시](../help-topics/sql-server-login-dialog.md)합니다.