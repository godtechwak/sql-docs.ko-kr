---
title: SqlPackage.exe
description: SqlPackage.exe를 사용하여 데이터베이스 개발 작업을 자동화하는 방법을 알아봅니다. 예제 및 사용 가능한 매개 변수, 속성 및 SQLCMD 변수를 확인합니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 198198e2-7cf4-4a21-bda4-51b36cb4284b
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan; sstein
ms.date: 11/4/2020
ms.openlocfilehash: 7894ea12ef77a7fb07a61ff454f27150812c7dfb
ms.sourcegitcommit: 0c0e4ab90655dde3e34ebc08487493e621f25dda
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96443064"
---
# <a name="sqlpackageexe"></a>SqlPackage.exe

**SqlPackage.exe** 는 다음 데이터베이스 개발 작업을 자동화하는 명령줄 유틸리티입니다.  
  
- [버전](#version): SqlPackage 애플리케이션의 빌드 번호를 반환합니다.  버전 18.6에 추가되었습니다.

- [추출](#extract-parameters-and-properties): 라이브 SQL Server 또는 Azure SQL Database에서 데이터베이스 스냅샷(.dacpac) 파일을 만듭니다.  
  
- [게시](#publish-parameters-properties-and-sqlcmd-variables): 원본 .dacpac 파일의 스키마와 일치하도록 데이터베이스 스키마를 증분식으로 업데이트합니다. 데이터베이스가 서버에 존재하지 않을 경우 게시 작업을 통해 생성됩니다. 존재하는 경우 기존 데이터베이스가 업데이트됩니다.  
  
- [Export](#export-parameters-and-properties): 데이터베이스 스키마 및 사용자 데이터를 비롯한 라이브 데이터베이스를 SQL Server 또는 Azure SQL Database에서 BACPAC 패키지(.bacpac 파일)로 내보냅니다.  
  
- [Import](#import-parameters-and-properties): BACPAC 패키지의 스키마 및 테이블 데이터를 SQL Server 또는 Azure SQL Database 인스턴스의 새로운 사용자 데이터베이스로 가져옵니다.  
  
- [DeployReport](#deployreport-parameters-and-properties): 게시 작업으로 변경된 사항의 XML 보고서를 만듭니다.  
  
- [DriftReport](#driftreport-parameters): 등록된 데이터베이스가 마지막으로 등록된 후에 변경된 사항의 XML 보고서를 만듭니다.  
  
- [스크립트](#script-parameters-and-properties): 대상의 스키마가 원본의 스키마와 일치하도록 업데이트하는 Transact-SQL 증분 업데이트 스크립트를 만듭니다.  
  
**SqlPackage.exe** 명령줄을 사용하면 작업별 매개 변수 및 속성과 함께 이러한 작업을 지정할 수 있습니다.  

**[최신 버전 다운로드](sqlpackage-download.md)** . 최신 릴리스에 대한 자세한 내용은 [릴리스 정보](release-notes-sqlpackage.md)를 참조하세요.
  
## <a name="command-line-syntax"></a>명령줄 구문

**SqlPackage.exe** 는 명령줄에 지정된 매개 변수, 속성 및 SQLCMD 변수를 사용하여 지정된 작업을 시작합니다.  
  
```
SqlPackage {parameters}{properties}{SQLCMD Variables}  
```

### <a name="usage-examples"></a>사용 예

**SQL 스크립트 출력과 함께 .dacpac 파일을 사용하여 데이터베이스 간 비교 생성**

최신 데이터베이스 변경 내용의 .dacpac 파일을 만들어 시작합니다.

```
sqlpackage.exe /TargetFile:"C:\sqlpackageoutput\output_current_version.dacpac" /Action:Extract /SourceServerName:"." /SourceDatabaseName:"Contoso.Database"
 ```
 
변경되지 않은 데이터베이스 대상의 .dacpac 파일을 만듭니다.

 ```
 sqlpackage.exe /TargetFile:"C:\sqlpackageoutput\output_target.dacpac" /Action:Extract /SourceServerName:"." /SourceDatabaseName:"Contoso.Database"
 ```

두 .dacpac 파일의 차이점을 생성하는 SQL 스크립트를 만듭니다.

```
sqlpackage.exe /Action:Script /SourceFile:"C:\sqlpackageoutput\output_current_version.dacpac" /TargetFile:"C:\sqlpackageoutput\output_target.dacpac" /TargetDatabaseName:"Contoso.Database" /OutputPath:"C:\sqlpackageoutput\output.sql"
 ```


## <a name="version"></a>버전

sqlpackage 버전을 빌드 번호로 표시합니다.  [자동화된 파이프라인](sqlpackage-pipelines.md)뿐만 아니라 대화형 프롬프트에서도 사용할 수 있습니다.

```
sqlpackage.exe /Version
 ```


## <a name="extract-parameters-and-properties"></a>매개 변수 및 속성 추출
SqlPackage.exe 추출 작업은 SQL Server 또는 Azure SQL Database에서 DACPAC 패키지(.dacpac 파일)로 라이브 데이터베이스 스키마를 만듭니다. 기본적으로 데이터는 .dacpac 파일에 포함되지 않습니다. 데이터를 포함하려면 [내보내기 작업](#export-parameters-and-properties)을 사용합니다. 

### <a name="help-for-the-extract-action"></a>Extract 동작에 대한 도움말

|매개 변수|약식|값|설명|
|---|---|---|---|
|**/Action:**|**/a**|Extract|수행할 작업을 지정합니다. |
|**/AccessToken:**|**/at**|{string}| 대상 데이터베이스에 연결할 때 사용할 액세스 토큰 기반 인증 액세스 토큰을 지정합니다. |
|**/Diagnostics:**|**/d**|{True&#124;False}|진단 로깅이 콘솔로 출력되는지 여부를 지정합니다. 기본값은 False입니다. |
|**/DiagnosticsFile:**|**/df**|{string}|진단 로그를 저장할 파일을 지정합니다. |
|**/MaxParallelism:**|**/mp**|{int}| 데이터베이스에 대해 실행 중인 동시 작업에 대한 병렬 처리 수준을 지정합니다. 기본값은 8입니다. |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|sqlpackage.exe이 기존 파일을 덮어써야 할지 여부를 지정합니다. False를 지정하면 기존 파일이 나타나는 경우 sqlpackage.exe에서 작업이 중단됩니다. 기본값은 True입니다. |
|**/Properties:**|**/p**|{PropertyName}={Value}|작업별 속성에 대한 이름 값 쌍을 지정합니다. {PropertyName}={Value}. 해당 작업의 속성 이름을 보려면 특정 작업의 도움말을 참조하십시오. 예: sqlpackage.exe /Action:Extract /?. |
|**/Quiet:**|**/q**|{True&#124;False}|자세한 피드백을 무시할지 여부를 지정합니다. 기본값은 False입니다. |
|**/SourceConnectionString:**|**/scs**|{string}|원본 데이터베이스에 대한 유효한 SQL Server/Azure 연결 문자열을 지정합니다. 이 매개 변수를 지정한 경우 다른 모든 원본 매개 변수와 단독으로 연결 문자열이 사용됩니다. |
|**/SourceDatabaseName:**|**/sdn**|{string}|원본 데이터베이스의 이름을 정의합니다. |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|원본 데이터베이스 연결에 대해 SQL 암호화를 사용할지 여부를 지정합니다. |
|**/SourcePassword:**|**/sp**|{string}|SQL Server 인증 시나리오에서 원본 데이터베이스에 액세스하는 데 사용할 암호를 정의합니다. |
|**/SourceServerName:**|**/ssn**|{string}|원본 데이터베이스를 호스팅하는 서버의 이름을 정의합니다. |
|**/SourceTimeout:**|**/st**|{int}|원본 데이터베이스에 대한 연결을 설정하는 데 대한 제한 시간(초)을 지정합니다. |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|원본 데이터베이스 연결을 암호화하고 신뢰의 유효성을 검증하기 위한 인증서 체인 검색을 건너뛰는 데 TLS를 사용할지 여부를 지정합니다. |
|**/SourceUser:**|**/su**|{string}|SQL Server 인증 시나리오에서 원본 데이터베이스에 액세스하는 데 사용할 SQL Server 사용자를 정의합니다. |
|**/TargetFile:**|**/tf**|{string}| 데이터베이스 대신 작업 대상으로 사용될 대상 파일(.dacpac 파일)을 지정합니다. 이 매개 변수를 사용하는 경우 다른 대상 매개 변수가 무효화됩니다. 이 매개 변수는 데이터베이스 대상만 지원하는 동작에는 유효하지 않습니다.| 
|**/TenantId:**|**/tid**|{string}|Azure AD 테넌트 ID 또는 도메인 이름을 나타냅니다. 이 옵션은 outlook.com, hotmail.com 또는 live.com과 같은 Microsoft 계정뿐만 아니라 게스트 또는 가져온 Azure AD 사용자를 지원해야 합니다. 이 매개 변수를 생략하면 인증된 사용자가 이 AD의 기본 사용자라고 가정하여 Azure AD의 기본 테넌트 ID가 사용됩니다. 그러나 이 경우 이 Azure AD에서 호스트되는 모든 게스트 또는 가져온 사용자 및/또는 Microsoft 계정은 지원되지 않으며 작업이 실패합니다. <br/> Active Directory 유니버설 인증에 대한 자세한 내용은 [SQL Database 및 Azure Synapse Analytics에 대한 유니버설 인증(SSMS의 MFA 지원)](/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|유니버설 인증을 사용해야 하는지 여부를 지정합니다. True로 설정되면 대화형 인증 프로토콜이 MFA를 지원하도록 활성화됩니다. 이 옵션은 사용자가 사용자 이름 및 암호 또는 통합 인증(Windows 자격 증명)을 입력해야 하는 대화형 프로토콜을 사용하여 MFA가 없는 Azure AD 인증에도 사용할 수 있습니다. /UniversalAuthentication을 True로 설정하면 SourceConnectionString(/scs)에 Azure AD 인증을 지정할 수 없습니다. /UniversalAuthentication을 False로 설정하면 SourceConnectionString(/scs)에 Azure AD 인증을 지정해야 합니다. <br/> Active Directory 유니버설 인증에 대한 자세한 내용은 [SQL Database 및 Azure Synapse Analytics에 대한 유니버설 인증(SSMS의 MFA 지원)](/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.|

### <a name="properties-specific-to-the-extract-action"></a>Extract 동작과 관련된 속성

|속성|값|Description|
|---|---|---|
|**/p:**|CommandTimeout=(INT32 '60')|SQL Server에 대한 쿼리를 실행할 때 명령 시간 제한(초)을 지정합니다.|
|**/p:**|DacApplicationDescription=(STRING)|DACPAC 메타데이터에 저장할 애플리케이션 설명을 정의합니다.|
|**/p:**|DacApplicationName=(STRING)|DACPAC 메타데이터에 저장할 애플리케이션 이름을 정의했습니다. 기본값은 데이터베이스 이름입니다.|
|**/p:**|DacMajorVersion=(INT32 '1')|DACPAC 메타데이터에 저장할 주 버전을 정의합니다.|
|**/p:**|DacMinorVersion=(INT32 '0')|DACPAC 메타데이터에 저장할 부 버전을 정의합니다.|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| SQLServer에 대해 쿼리를 실행할 때의 데이터베이스 잠금 시간 제한(초)를 지정합니다. 무기한 대기하려면 -1을 사용합니다.|
|**/p:**|ExtractAllTableData=(BOOLEAN)|모든 사용자 테이블의 데이터를 추출하는지 여부를 나타냅니다. 'true'인 경우 모든 사용자 테이블의 데이터가 추출되며 데이터 추출을 위해 개별 사용자 테이블을 지정할 수 없습니다. 'false'인 경우 데이터를 추출할 하나 이상의 사용자 테이블을 지정합니다.|
|**/p:**|ExtractApplicationScopedObjectsOnly=(BOOLEAN 'True')|True인 경우 지정된 원본에 대해 애플리케이션 범위 개체만 추출합니다. False인 경우 지정된 원본에 대해 모든 개체를 추출합니다.|
|**/p:**|ExtractReferencedServerScopedElements=(BOOLEAN 'True')|True인 경우 원본 데이터베이스 개체에서 참조하는 로그인, 서버 감사 및 자격 증명 개체를 추출합니다.|
|**/p:**|ExtractUsageProperties=(BOOLEAN)|테이블 행 개수, 인덱스 크기를 비롯한 사용 속성을 데이터베이스에서 추출할지를 지정합니다.|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|확장된 속성을 무시할지 여부를 지정합니다.|
|**/p:**|IgnorePermissions=(BOOLEAN 'True')|권한을 무시할지 여부를 지정합니다.|
|**/p:**|IgnoreUserLoginMappings=(BOOLEAN)|사용자와 로그인 간의 관계를 무시할지 여부를 지정합니다.|
|**/p:**|LongRunningCommandTimeout=(INT32)| SQL Server에 대한 쿼리를 실행할 때 장기 명령 시간 제한(초)을 지정합니다. 무기한 대기하려면 0을 사용합니다.|
|**/p:**|Storage=({File&#124;Memory} 'File')|추출 중에 사용되는 스키마 모델에 대한 지원 스토리지 유형을 지정합니다.|
|**/p:**|TableData=(STRING)|데이터를 추출할 테이블을 나타냅니다. schema_name.table_identifier 형식에서 이름 부분이 괄호로 묶이거나 묶이지 않은 형태로 테이블 이름을 지정하십시오. 이 옵션은 여러 번 지정할 수 있습니다.|
|**/p:**| TempDirectoryForTableData=(STRING)|패키지 파일에 기록되기 전에 테이블 데이터를 버퍼링하는 데 사용되는 임시 디렉터리를 지정합니다.|
|**/p:**|VerifyExtraction=(BOOLEAN)|추출된 dacpac를 확인할지 여부를 지정합니다.|

## <a name="publish-parameters-properties-and-sqlcmd-variables"></a>매개 변수, 속성 및 SQLCMD 변수 게시

SqlPackage.exe 게시 작업은 원본 데이터베이스의 구조와 일치하도록 대상 데이터베이스의 스키마를 증분식으로 업데이트합니다. 테이블 전체나 하위 집합의 사용자 데이터를 포함하는 배포 패키지를 게시하면 스키마 외에도 테이블 데이터가 업데이트됩니다. 데이터 배포는 대상 데이터베이스의 기존 테이블에 있는 스키마와 데이터를 덮어씁니다. 이때 배포 패키지에 포함되지 않은 대상 데이터베이스의 테이블에 대한 기존 스키마나 데이터는 변경되지 않습니다.  

### <a name="help-for-publish-action"></a>Publish 동작에 대한 도움말

|매개 변수|약식|값|설명|
|---|---|---|---|
|**/Action:**|**/a**|게시|수행할 작업을 지정합니다. |
|**/AccessToken:**|**/at**|{string}| 대상 데이터베이스에 연결할 때 사용할 액세스 토큰 기반 인증 액세스 토큰을 지정합니다. |
|**/AzureKeyVaultAuthMethod:**|**/akv**|{Interactive&#124;ClientIdSecret}|게시 작업에 암호화된 테이블/열의 수정 내용이 포함된 경우 Azure KeyVault에 액세스하는 데 사용되는 인증 방법을 지정합니다. |
|**/ClientId:**|**/cid**|{string}|필요한 경우 Azure KeyVault에 대해 인증 시 사용할 클라이언트 ID를 지정합니다. |
|**/DeployScriptPath:**|**/dsp**|{string}|배포 스크립트를 출력할 선택적 파일 경로를 지정합니다. Azure 배포의 경우 master 데이터베이스를 만들거나 수정하는 TSQL 명령이 있을 경우 스크립트가 동일한 경로에 작성되지만 “Filename_Master.sql”을 출력 파일 이름으로 사용합니다. |
|**/DeployReportPath:**|**/drp**|{string}|배포 보고서 xml 파일을 출력할 선택적 파일 경로를 지정합니다. |
|**/Diagnostics:**|**/d**|{True&#124;False}|진단 로깅이 콘솔로 출력되는지 여부를 지정합니다. 기본값은 False입니다. |
|**/DiagnosticsFile:**|**/df**|{string}|진단 로그를 저장할 파일을 지정합니다. |
|**/MaxParallelism:**|**/mp**|{int}| 데이터베이스에 대해 실행 중인 동시 작업에 대한 병렬 처리 수준을 지정합니다. 기본값은 8입니다. |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|sqlpackage.exe이 기존 파일을 덮어써야 할지 여부를 지정합니다. False를 지정하면 기존 파일이 나타나는 경우 sqlpackage.exe에서 작업이 중단됩니다. 기본값은 True입니다. |
|**/Profile:**|**/pr**|{string}|DAC 게시 프로필에 대한 파일 경로를 지정합니다. 프로필은 출력을 생성할 때 사용할 속성 및 변수 컬렉션을 정의합니다.|
|**/Properties:**|**/p**|{PropertyName}={Value}|작업별 속성에 대한 이름 값 쌍을 지정합니다. {PropertyName}={Value}. 해당 작업의 속성 이름을 보려면 특정 작업의 도움말을 참조하십시오. 예: sqlpackage.exe /Action:Publish /?.|
|**/Quiet:**|**/q**|{True&#124;False}|자세한 피드백을 무시할지 여부를 지정합니다. 기본값은 False입니다.|
|**/Secret:**|**/secr**|{string}|필요한 경우 Azure KeyVault에 대해 인증 시 사용할 클라이언트 암호를 지정합니다. |
|**/SourceConnectionString:**|**/scs**|{string}|원본 데이터베이스에 대한 유효한 SQL Server/Azure 연결 문자열을 지정합니다. 이 매개 변수를 지정한 경우 다른 모든 원본 매개 변수와 단독으로 연결 문자열이 사용됩니다. |
|**/SourceDatabaseName:**|**/sdn**|{string}|원본 데이터베이스의 이름을 정의합니다. |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|원본 데이터베이스 연결에 대해 SQL 암호화를 사용할지 여부를 지정합니다. |
|**/SourceFile:**|**/sf**|{string}|데이터베이스 대신 작업 원본으로 사용할 원본 파일을 지정합니다. 이 매개 변수를 사용하는 경우 다른 원본 매개 변수가 무효화됩니다. |
|**/SourcePassword:**|**/sp**|{string}|SQL Server 인증 시나리오에서 원본 데이터베이스에 액세스하는 데 사용할 암호를 정의합니다. |
|**/SourceServerName:**|**/ssn**|{string}|원본 데이터베이스를 호스팅하는 서버의 이름을 정의합니다. |
|**/SourceTimeout:**|**/st**|{int}|원본 데이터베이스에 대한 연결을 설정하는 데 대한 제한 시간(초)을 지정합니다. |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|원본 데이터베이스 연결을 암호화하고 신뢰의 유효성을 검증하기 위한 인증서 체인 검색을 건너뛰는 데 TLS를 사용할지 여부를 지정합니다. |
|**/SourceUser:**|**/su**|{string}|SQL Server 인증 시나리오에서 원본 데이터베이스에 액세스하는 데 사용할 SQL Server 사용자를 정의합니다. |
|**/TargetConnectionString:**|**/tcs**|{string}|대상 데이터베이스에 대한 유효한 SQL Server/Azure 연결 문자열을 지정합니다. 이 매개 변수를 지정한 경우 다른 모든 대상 매개 변수와 단독으로 연결 문자열이 사용됩니다. |
|**/TargetDatabaseName:**|**/tdn**|{string}|sqlpackage.exe 동작의 대상인 데이터베이스의 이름에 대한 재정의를 지정합니다. |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|대상 데이터베이스 연결에 대해 SQL 암호화를 사용할지 여부를 지정합니다. |
|**/TargetPassword:**|**/tp**|{string}|SQL Server 인증 시나리오에서 대상 데이터베이스에 액세스하는 데 사용할 암호를 정의합니다. |
|**/TargetServerName:**|**/tsn**|{string}|대상 데이터베이스를 호스팅하는 서버의 이름을 정의합니다. |
|**/TargetTimeout:**|**/tt**|{int}|대상 데이터베이스에 대한 연결을 설정하는 데 대한 제한 시간(초)을 지정합니다. Azure AD의 경우 이 값을 30초보다 크거나 같게 하는 것이 좋습니다.|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|대상 데이터베이스 연결을 암호화하고 신뢰의 유효성을 검증하기 위한 인증서 체인 검색을 건너뛰는 데 TLS를 사용할지 여부를 지정합니다. |
|**/TargetUser:**|**/tu**|{string}|SQL Server 인증 시나리오에서 대상 데이터베이스에 액세스하는 데 사용할 SQL Server 사용자를 정의합니다. |
|**/TenantId:**|**/tid**|{string}|Azure AD 테넌트 ID 또는 도메인 이름을 나타냅니다. 이 옵션은 outlook.com, hotmail.com 또는 live.com과 같은 Microsoft 계정뿐만 아니라 게스트 또는 가져온 Azure AD 사용자를 지원해야 합니다. 이 매개 변수를 생략하면 인증된 사용자가 이 AD의 기본 사용자라고 가정하여 Azure AD의 기본 테넌트 ID가 사용됩니다. 그러나 이 경우 이 Azure AD에서 호스트되는 모든 게스트 또는 가져온 사용자 및/또는 Microsoft 계정은 지원되지 않으며 작업이 실패합니다. <br/> Active Directory 유니버설 인증에 대한 자세한 내용은 [SQL Database 및 Azure Synapse Analytics에 대한 유니버설 인증(SSMS의 MFA 지원)](/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|유니버설 인증을 사용해야 하는지 여부를 지정합니다. True로 설정되면 대화형 인증 프로토콜이 MFA를 지원하도록 활성화됩니다. 이 옵션은 사용자가 사용자 이름 및 암호 또는 통합 인증(Windows 자격 증명)을 입력해야 하는 대화형 프로토콜을 사용하여 MFA가 없는 Azure AD 인증에도 사용할 수 있습니다. /UniversalAuthentication을 True로 설정하면 SourceConnectionString(/scs)에 Azure AD 인증을 지정할 수 없습니다. /UniversalAuthentication을 False로 설정하면 SourceConnectionString(/scs)에 Azure AD 인증을 지정해야 합니다. <br/> Active Directory 유니버설 인증에 대한 자세한 내용은 [SQL Database 및 Azure Synapse Analytics에 대한 유니버설 인증(SSMS의 MFA 지원)](/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.|
|**/Variables:**|**/v**|{PropertyName}={Value}|작업별 변수에 대한 이름 값 쌍을 지정합니다. {VariableName}={Value}. DACPAC 파일에는 유효한 SQLCMD 변수 목록이 포함됩니다. 모든 변수에 대해 값을 제공하지 않으면 오류가 발생합니다. |

### <a name="properties-specific-to-the-publish-action"></a>Publish 동작과 관련된 속성

|속성|값|Description|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|배포 참가자에 대한 추가 배포 참가자 인수를 지정합니다. 세미콜론으로 구분된 값의 목록이어야 합니다.|
|**/p:**|AdditionalDeploymentContributors=(STRING)|dacpac가 배포될 때 실행되어야 하는 추가 배포 기여자를 지정합니다. 세미콜론으로 구분된 정규화된 빌드 참가자 이름 또는 ID의 목록이어야 합니다.|
|**/p:**|AdditionalDeploymentContributorPaths=(STRING)| 추가 배포 참가자를 로드할 경로를 지정합니다. 세미콜론으로 구분된 값의 목록이어야 합니다. | 
|**/p:**|AllowDropBlockingAssemblies=(BOOLEAN)|이 속성은 SqlClr 배포에서 배포 계획의 일부로 차단 어셈블리를 삭제하는 데 사용됩니다. 기본적으로 어셈블리를 삭제해야 하는 경우에는 모든 차단/참조 어셈블리가 어셈블리 업데이트를 차단합니다.|
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|SQL Server 플랫폼이 호환되지 않을 수 있는 경우에도 작업을 시도해야 하는지 여부를 지정합니다.|
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|이 속성이 True로 설정되어 있으면 행 수준 보안이 설정된 테이블에서 데이터 이동을 차단하지 않습니다. 기본값은 false입니다.|
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|변경 내용을 배포하기 전 데이터베이스를 백업합니다.|
|**/p:**|BlockOnPossibleDataLoss=(BOOLEAN 'True')|publish.operation으로 인해 데이터 손실이 발생할 수 있는 경우 게시 에피소드를 종료할지 여부를 지정합니다.|
|**/p:**|BlockWhenDriftDetected=(BOOLEAN 'True')|스키마가 더 이상 해당 등록과 일치하지 않거나 등록이 해제된 데이터베이스 업데이트를 차단할지 여부를 지정합니다.|
|**/p:**|CommandTimeout=(INT32 '60')|SQL Server에 대한 쿼리를 실행할 때 명령 시간 제한(초)을 지정합니다.|
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|생성된 게시 스크립트에서 SETVAR 변수 선언을 주석 처리할지 여부를 지정합니다. 게시할 때 SQLCMD.EXE 등의 도구를 사용하여 명령줄에 값을 지정하려는 경우 이와 같이 할 수 있습니다.|
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|이 설정은 배포 중 데이터베이스의 데이터 정렬 처리 방법을 지정합니다.기본적으로 원본에서 지정하는 데이터 정렬과 일치하지 않을 경우 대상 데이터베이스의 데이터 정렬이 업데이트됩니다. 이 옵션을 설정하면 대상 데이터베이스(또는 서버)의 데이터 정렬이 사용됩니다.|
|**/p:**|CreateNewDatabase=(BOOLEAN)|데이터베이스에 게시할 때 대상 데이터베이스를 업데이트할지 또는 삭제 후 다시 만들지 여부를 지정합니다.|
|**/p:**|DatabaseEdition=({Basic&#124;Standard&#124;Premium&#124;DataWarehouse&#124;GeneralPurpose&#124;BusinessCritical&#124;Hyperscale&#124;Default} 'Default')|Azure SQL Database의 버전을 정의합니다.|
|**/p:**|DatabaseLockTimeout=(INT32 '60')|SQLServer에 대해 쿼리를 실행할 때의 데이터베이스 잠금 시간 제한(초)를 지정합니다. 무기한 대기하려면 -1을 사용합니다.|
|**/p:**|DatabaseMaximumSize=(INT32)|Azure SQL Database의 최대 크기(GB)를 정의합니다.|
|**/p:**|DatabaseServiceObjective=(STRING)|“P0” 또는 “S1”과 같은 Azure SQL Database의 성능 수준을 정의합니다.|
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|True인 경우 배포 전에 데이터베이스가 단일 사용자 모드로 설정됩니다.|
|**/p:**|DisableAndReenableDdlTriggers=(BOOLEAN 'True')|게시 프로세스가 시작할 때 DDL(데이터 정의 언어) 트리거를 사용하지 않고 게시 작업이 끝날 때 다시 사용할지 여부를 지정합니다.|
|**/p:**|DoNotAlterChangeDataCaptureObjects=(BOOLEAN 'True')|True인 경우 변경 데이터 캡처 개체가 수정되지 않습니다.|
|**/p:**|DoNotAlterReplicatedObjects=(BOOLEAN 'True')|복제된 개체를 확인 중에 식별할지 여부를 지정합니다.|
|**/p:**|DoNotDropObjectType=(STRING)|DropObjectsNotInSource가 true인 경우 삭제하지 않아야 하는 개체 형식입니다. 유효한 개체 유형 이름은 Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers입니다.|
|**/p:**|DoNotDropObjectTypes=(STRING)|DropObjectsNotInSource가 true인 경우 삭제하지 않아야 하는 개체 형식을 세미콜론으로 구분한 목록입니다. 유효한 개체 유형 이름은 Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers입니다.|
|**/p:**|DropConstraintsNotInSource=(BOOLEAN 'True')|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 제약 조건을 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropDmlTriggersNotInSource=(BOOLEAN 'True')|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 DML 트리거를 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropExtendedPropertiesNotInSource=(BOOLEAN 'True')|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 확장 속성을 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropIndexesNotInSource=(BOOLEAN 'True')|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 인덱스를 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 개체를 대상 데이터베이스에서 삭제할지 여부를 지정합니다. 이 값은 DropExtendedProperties보다 우선적으로 적용됩니다.|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|데이터베이스에 업데이트를 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 권한을 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|데이터베이스에 업데이트를 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 정의되지 않은 역할 멤버를 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropStatisticsNotInSource=(BOOLEAN 'True')|데이터베이스 스냅샷(.dacpac) 파일에 없는 통계를 데이터베이스에 게시할 때 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|ExcludeObjectType=(STRING)|배포 중에 무시되어야 하는 개체 유형입니다. 유효한 개체 유형 이름은 Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers입니다.|
|**/p:**|ExcludeObjectTypes=(STRING)|배포 중에 무시되어야 하는 개체 유형의 세미콜론으로 구분된 목록입니다. 유효한 개체 유형 이름은 Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers입니다.|
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|데이터가 들어 있는 테이블을 Null 값을 허용하지 않는 열로 업데이트할 때 자동으로 기본 값을 제공합니다.|
|**/p:**|IgnoreAnsiNulls=(BOOLEAN 'True')|데이터베이스에 게시할 때 ANSI NULLS 설정에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|데이터베이스에 게시할 때 권한 부여자를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|데이터베이스에 게시할 때 열 데이터 정렬의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|데이터베이스에 게시할 때 테이블 열 순서의 차이를 무시해야 할지 아니면 업데이트해야 할지를 지정합니다.|
|**/p:**|IgnoreComments=(BOOLEAN)|데이터베이스에 게시할 때 주석의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreCryptographicProviderFilePath=(BOOLEAN 'True')|데이터베이스에 게시할 때 암호화 공급자에 대한 파일 경로의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|데이터베이스 또는 서버에 게시할 때 DDL(Data Definition Language) 트리거 순서의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|데이터베이스에 게시할 때 DDL(Data Definition Language) 트리거 사용/사용 안 함 상태의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|데이터베이스에 게시할 때 기본 스키마의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|데이터베이스에 게시할 때 DML(Data Manipulation Language) 트리거 순서의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|데이터베이스에 게시할 때 DML 트리거 사용/사용 안 함 상태의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|데이터베이스에 게시할 때 확장 속성의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreFileAndLogFilePath=(BOOLEAN 'True')|데이터베이스에 게시할 때 파일 및 로그 파일에 대한 경로의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreFilegroupPlacement=(BOOLEAN 'True')|데이터베이스에 게시할 때 FILEGROUP에서의 개체 배치에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreFileSize=(BOOLEAN 'True')|데이터베이스에 게시할 때 파일 크기의 차이를 무시할지 또는 경고를 발생하도록 할지를 지정합니다.|
|**/p:**|IgnoreFillFactor=(BOOLEAN 'True')|데이터베이스에 게시할 때 인덱스 스토리지의 채우기 비율에 대한 차이를 무시할지 또는 경고를 발생하도록 할지를 지정합니다.|
|**/p:**|IgnoreFullTextCatalogFilePath=(BOOLEAN 'True')|데이터베이스에 게시할 때 인덱스 저장소의 채우기 비율에 대한 차이를 무시할지 또는 경고를 발생하도록 할지를 지정합니다.|
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|데이터베이스에 게시할 때 ID 열의 시드에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreIncrement=(BOOLEAN)|데이터베이스에 게시할 때 ID 열의 증가값에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|데이터베이스에 게시할 때 인덱스 옵션의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreIndexPadding=(BOOLEAN 'True')|데이터베이스에 게시할 때 인덱스 패딩의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreKeywordCasing=(BOOLEAN 'True')|데이터베이스에 게시할 때 키워드의 대/소문자 구분에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|데이터베이스에 게시할 때 인덱스의 잠금 힌트의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|
|**/p:**|IgnoreLoginSids=(BOOLEAN 'True')|데이터베이스에 게시할 때 SID(보안 ID)의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|데이터베이스에 게시할 때 복제용 아님 설정을 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreObjectPlacementOnPartitionScheme=(BOOLEAN 'True')|데이터베이스에 게시할 때 파티션 구성표에서 개체의 배치를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnorePartitionSchemes=(BOOLEAN)|데이터베이스에 게시할 때 분할 구성표와 함수의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnorePermissions=(BOOLEAN)|데이터베이스에 게시할 때 사용 권한의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreQuotedIdentifiers=(BOOLEAN 'True')|데이터베이스에 게시할 때 따옴표 붙은 식별자 설정의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|데이터베이스에 게시할 때 로그인의 역할 멤버 자격 차이를 무시 또는 업데이트할지 여부를 지정합니다.|
|**/p:**|IgnoreRouteLifetime=(BOOLEAN 'True')|데이터베이스에 게시할 때 SQL Server가 라우팅 테이블에 경로를 유지하는 시간에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreSemicolonBetweenStatements=(BOOLEAN 'True')|데이터베이스에 게시할 때 T-SQL 문 사이의 세미콜론의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreTableOptions=(BOOLEAN)|데이터베이스에 게시할 때 테이블 옵션의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreTablePartitionOptions=(BOOLEAN)|데이터베이스에 게시할 때 테이블 파티션 옵션의 차이를 무시할지 또는 업데이트할지를 지정합니다.  이 옵션은 Azure Synapse Analytics 전용 SQL 풀 데이터베이스에만 적용됩니다.|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|데이터베이스에 게시할 때 사용자 설정 개체의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreWhitespace=(BOOLEAN 'True')|데이터베이스에 게시할 때 공백의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|데이터베이스에 게시할 때 CHECK 제약 조건의 WITH NOCHECK 절에 대한 값의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|데이터베이스에 게시할 때 외래 키의 WITH NOCHECK 절에 대한 값의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|모든 복합 요소를 단일 게시 작업의 일부로 포함합니다.|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|데이터베이스에 게시할 때 가능한 위치에 트랜잭션 문을 사용할지 여부를 지정합니다.|
|**/p:**|LongRunningCommandTimeout=(INT32)|SQL Server에 대한 쿼리를 실행할 때 장기 명령 시간 제한(초)을 지정합니다. 무기한 대기하려면 0을 사용합니다.|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|차이가 있을 경우 ALTER ASSEMBLY 문을 실행하는 대신 게시에서 항상 어셈블리를 삭제하고 다시 만들지를 지정합니다.|
|**/p:**|PopulateFilesOnFileGroups=(BOOLEAN 'True')|대상 데이터베이스에 새 FileGroup이 만들어질 때 새 파일도 만들어지는지 여부를 지정합니다.|
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|스키마가 데이터베이스 서버에 등록되었는지 여부를 지정합니다.|
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|다른 작업이 실행될때 DeploymentPlanExecutor 기여자를 실행할지 여부를 지정합니다.|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|데이터베이스에 게시할 때 데이터베이스 데이터 정렬의 차이를 무시할지, 업데이트할지를 지정합니다.|
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|데이터베이스에 게시할 때 데이터베이스 호환성의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|ScriptDatabaseOptions=(BOOLEAN 'True')|게시 동작의 일부로 대상 데이터베이스 속성을 설정 또는 업데이트할지 여부를 지정합니다.|
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|데이터베이스 이름 및 서버 이름이 데이터베이스 프로젝트에 지정된 이름과 일치하는지 확인하는 문을 게시 스크립트에 생성할지 여부를 지정합니다.|
|**/p:**|ScriptFileSize=(BOOLEAN)|파일 그룹에 파일을 추가할 때 크기를 지정하는지 여부를 제어합니다.|
|**/p:**|ScriptNewConstraintValidation=(BOOLEAN 'True')|게시 마지막에 모든 제약 조건은 하나의 집합으로 확인되므로 게시 중간에 검사 또는 외래 키 제약 조건으로 인한 데이터 오류가 발생하지 않습니다. False로 설정하면 해당 데이터를 확인하지 않고 제약 조건이 게시됩니다.|
|**/p:**|ScriptRefreshModule=(BOOLEAN 'True')|게시 스크립트의 끝에 새로 고침 문을 포함합니다.|
|**/p:**|Storage=({File&#124;Memory})|데이터베이스 모델을 생성할 때 요소의 저장 방법을 지정합니다. 성능상의 이유로 기본값은 InMemory입니다. 큰 데이터베이스의 경우 파일 지원 스토리지가 필요합니다.|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|확인을 경고로 처리해야 하는 동안 발생한 오류를 게시하는지 여부를 지정합니다. 생성된 배포 계획을 대상 데이터베이스에 대해 실행하기 전에 해당 계획에 대한 확인이 수행됩니다. 계획 확인에서 대상 전용 개체(예: 인덱스)가 없는 등의 문제가 발견되면 해당 계획을 삭제하여 변경해야 합니다. 또한 복합 프로젝트에 대한 참조로 인한 종속성(예: 테이블, 뷰)이 존재하지만 대상 데이터베이스에는 존재하지 않는 상황도 확인됩니다. 첫 번째 오류에서 게시 동작을 중지하는 대신 모든 문제의 전체 목록을 가져오려면 이 작업을 수행하도록 선택할 수 있습니다.
|**/p:**|UnmodifiableObjectWarnings=(BOOLEAN 'True')|개체에서 수정할 수 없는 차이가 발견될 경우(예: 파일 경로 또는 파일 크기가 특정 파일에서 다른 경우) 경고를 생성할지 여부를 지정합니다.|
|**/p:**|VerifyCollationCompatibility=(BOOLEAN 'True')|데이터 정렬 호환성이 확인되는지 여부를 지정합니다.|
|**/p:**|VerifyDeployment=(BOOLEAN 'True')|성공적인 게시를 차단할 수 있는 문제가 존재할 경우 게시 작업을 중단하는 검사를 게시 전에 수행할지 여부를 지정합니다. 예를 들어 데이터베이스 프로젝트에 존재하지 않고 게시할 때 오류를 일으키는 외래 키를 대상 데이터베이스에 설정한 경우 게시 작업이 중단될 수 있습니다.|
|

### <a name="sqlcmd-variables"></a>SQLCMD 변수

다음 표에는 게시 작업 중 사용하는 SQL 명령(**sqlcmd**) 변수 값을 재정의하는 데 사용할 수 있는 옵션의 형식이 설명되어 있습니다. 명령줄에 지정된 변수 값은 해당 변수에 할당된 다른 값(예: 게시 프로필에서)을 재정의합니다.  
  
|매개 변수|기본값|Description|  
|-------------|-----------|---------------|  
|**/Variables:{PropertyName}={Value}**||작업별 변수에 대한 이름 값 쌍을 지정합니다. {VariableName}={Value}. DACPAC 파일에는 유효한 SQLCMD 변수 목록이 포함됩니다. 모든 변수에 대해 값을 제공하지 않으면 오류가 발생합니다.|  
  
## <a name="export-parameters-and-properties"></a>매개 변수 및 속성 내보내기

SqlPackage.exe Export 작업은 SQL Server 또는 Azure SQL Database의 라이브 데이터베이스를 BACPAC 패키지(.bacpac 파일)로 내보냅니다. 기본적으로 모든 테이블의 데이터가 .bacpac 파일에 포함됩니다. 필요에 따라 데이터를 내보낼 테이블의 하위 집합만 지정할 수 있습니다. Export 작업의 유효성 검사는 테이블의 하위 집합이 내보내기에 지정된 경우에도 전체 대상 데이터베이스에 대한 Azure SQL Database 호환성을 보장합니다.  
  
### <a name="help-for-export-action"></a>Export 동작에 대한 도움말

|매개 변수|약식|값|설명|
|---|---|---|---|
|**/Action:**|**/a**|내보내기|수행할 작업을 지정합니다. |
|**/AccessToken:**|**/at**|{string}| 대상 데이터베이스에 연결할 때 사용할 액세스 토큰 기반 인증 액세스 토큰을 지정합니다. |
|**/Diagnostics:**|**/d**|{True&#124;False}|진단 로깅이 콘솔로 출력되는지 여부를 지정합니다. 기본값은 False입니다. |
|**/DiagnosticsFile:**|**/df**|{string}|진단 로그를 저장할 파일을 지정합니다. |
|**/MaxParallelism:**|**/mp**|{int}| 데이터베이스에 대해 실행 중인 동시 작업에 대한 병렬 처리 수준을 지정합니다. 기본값은 8입니다. |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|sqlpackage.exe이 기존 파일을 덮어써야 할지 여부를 지정합니다. False를 지정하면 기존 파일이 나타나는 경우 sqlpackage.exe에서 작업이 중단됩니다. 기본값은 True입니다. |
|**/Properties:**|**/p**|{PropertyName}={Value}|작업별 속성에 대한 이름 값 쌍을 지정합니다. {PropertyName}={Value}. 해당 작업의 속성 이름을 보려면 특정 작업의 도움말을 참조하십시오. 예: sqlpackage.exe /Action:Export /?.|
|**/Quiet:**|**/q**|{True&#124;False}|자세한 피드백을 무시할지 여부를 지정합니다. 기본값은 False입니다.|
|**/SourceConnectionString:**|**/scs**|{string}|원본 데이터베이스에 대한 유효한 SQL Server/Azure 연결 문자열을 지정합니다. 이 매개 변수를 지정한 경우 다른 모든 원본 매개 변수와 단독으로 연결 문자열이 사용됩니다. |
|**/SourceDatabaseName:**|**/sdn**|{string}|원본 데이터베이스의 이름을 정의합니다. |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|원본 데이터베이스 연결에 대해 SQL 암호화를 사용할지 여부를 지정합니다. |
|**/SourcePassword:**|**/sp**|{string}|SQL Server 인증 시나리오에서 원본 데이터베이스에 액세스하는 데 사용할 암호를 정의합니다. |
|**/SourceServerName:**|**/ssn**|{string}|원본 데이터베이스를 호스팅하는 서버의 이름을 정의합니다. |
|**/SourceTimeout:**|**/st**|{int}|원본 데이터베이스에 대한 연결을 설정하는 데 대한 제한 시간(초)을 지정합니다. |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|원본 데이터베이스 연결을 암호화하고 신뢰의 유효성을 검증하기 위한 인증서 체인 검색을 건너뛰는 데 TLS를 사용할지 여부를 지정합니다. |
|**/SourceUser:**|**/su**|{string}|SQL Server 인증 시나리오에서 원본 데이터베이스에 액세스하는 데 사용할 SQL Server 사용자를 정의합니다. |
|**/TargetFile:**|**/tf**|{string}| 데이터베이스 대신 작업 대상으로 사용될 대상 파일(.dacpac 파일)을 지정합니다. 이 매개 변수를 사용하는 경우 다른 대상 매개 변수가 무효화됩니다. 이 매개 변수는 데이터베이스 대상만 지원하는 동작에는 유효하지 않습니다.|
|**/TenantId:**|**/tid**|{string}|Azure AD 테넌트 ID 또는 도메인 이름을 나타냅니다. 이 옵션은 outlook.com, hotmail.com 또는 live.com과 같은 Microsoft 계정뿐만 아니라 게스트 또는 가져온 Azure AD 사용자를 지원해야 합니다. 이 매개 변수를 생략하면 인증된 사용자가 이 AD의 기본 사용자라고 가정하여 Azure AD의 기본 테넌트 ID가 사용됩니다. 그러나 이 경우 이 Azure AD에서 호스트되는 모든 게스트 또는 가져온 사용자 및/또는 Microsoft 계정은 지원되지 않으며 작업이 실패합니다. <br/> Active Directory 유니버설 인증에 대한 자세한 내용은 [SQL Database 및 Azure Synapse Analytics에 대한 유니버설 인증(SSMS의 MFA 지원)](/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|유니버설 인증을 사용해야 하는지 여부를 지정합니다. True로 설정되면 대화형 인증 프로토콜이 MFA를 지원하도록 활성화됩니다. 이 옵션은 사용자가 사용자 이름 및 암호 또는 통합 인증(Windows 자격 증명)을 입력해야 하는 대화형 프로토콜을 사용하여 MFA가 없는 Azure AD 인증에도 사용할 수 있습니다. /UniversalAuthentication을 True로 설정하면 SourceConnectionString(/scs)에 Azure AD 인증을 지정할 수 없습니다. /UniversalAuthentication을 False로 설정하면 SourceConnectionString(/scs)에 Azure AD 인증을 지정해야 합니다. <br/> Active Directory 유니버설 인증에 대한 자세한 내용은 [SQL Database 및 Azure Synapse Analytics에 대한 유니버설 인증(SSMS의 MFA 지원)](/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.|

### <a name="properties-specific-to-the-export-action"></a>Export 동작과 관련된 속성

|속성|값|Description|
|---|---|---|
|**/p:**|CommandTimeout=(INT32 '60')|SQL Server에 대한 쿼리를 실행할 때 명령 시간 제한(초)을 지정합니다.|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| SQLServer에 대해 쿼리를 실행할 때의 데이터베이스 잠금 시간 제한(초)를 지정합니다. 무기한 대기하려면 -1을 사용합니다.|
|**/p:**|LongRunningCommandTimeout=(INT32)| SQL Server에 대한 쿼리를 실행할 때 장기 명령 시간 제한(초)을 지정합니다. 무기한 대기하려면 0을 사용합니다.|
|**/p:**|Storage=({File&#124;Memory} 'File')|추출 중에 사용되는 스키마 모델에 대한 지원 스토리지 유형을 지정합니다.|
|**/p:**|TableData=(STRING)|데이터를 추출할 테이블을 나타냅니다. schema_name.table_identifier 형식에서 이름 부분이 괄호로 묶이거나 묶이지 않은 형태로 테이블 이름을 지정하십시오. 이 옵션은 여러 번 지정할 수 있습니다.|
|**/p:**|TempDirectoryForTableData=(STRING)|패키지 파일에 기록되기 전에 테이블 데이터를 버퍼링하는 데 사용되는 임시 디렉터리를 지정합니다.|
|**/p:**|TargetEngineVersion=({Default&#124;Latest&#124;V11&#124;V12} 'Latest')|필요한 대상 엔진 버전을 지정합니다. 이 작업은 생성된 bacpac에서 V12 기능(예: 메모리 최적화 테이블)이 포함된 Azure SQL Database 서버가 지원하는 개체를 허용할지 여부에 영향을 줍니다.|
|**/p:**|VerifyFullTextDocumentTypesSupported=(BOOLEAN)|Microsoft Azure SQL Database v12에 지원되는 전체 텍스트 문서 종류를 확인할지 여부를 지정합니다.|
  
## <a name="import-parameters-and-properties"></a>매개 변수 및 속성 가져오기

SqlPackage.exe Import 작업은 BACPAC 패키지(.bacpac 파일)의 스키마 및 테이블 데이터를 SQL Server 또는 Azure SQL Database의 비어 있거나 새로운 데이터베이스로 가져옵니다. 기존 데이터베이스에 대한 가져오기 작업 시에는 대상 데이터베이스에 사용자 정의 스키마 개체가 포함될 수 없습니다.  
  
### <a name="help-for-command-actions"></a>명령 동작에 대한 도움말

|매개 변수|약식|값|설명|
|---|---|---|---|
|**/Action:**|**/a**|가져오기|수행할 작업을 지정합니다. |
|**/AccessToken:**|**/at**|{string}| 대상 데이터베이스에 연결할 때 사용할 액세스 토큰 기반 인증 액세스 토큰을 지정합니다. |
|**/Diagnostics:**|**/d**|{True&#124;False}|진단 로깅이 콘솔로 출력되는지 여부를 지정합니다. 기본값은 False입니다. |
|**/DiagnosticsFile:**|**/df**|{string}|진단 로그를 저장할 파일을 지정합니다. |
|**/MaxParallelism:**|**/mp**|{int}| 데이터베이스에 대해 실행 중인 동시 작업에 대한 병렬 처리 수준을 지정합니다. 기본값은 8입니다. |
|**/Properties:**|**/p**|{PropertyName}={Value}|작업별 속성에 대한 이름 값 쌍을 지정합니다. {PropertyName}={Value}. 해당 작업의 속성 이름을 보려면 특정 작업의 도움말을 참조하십시오. 예: sqlpackage.exe /Action:Import /?.|
|**/Quiet:**|**/q**|{True&#124;False}|자세한 피드백을 무시할지 여부를 지정합니다. 기본값은 False입니다.|
|**/SourceFile:**|**/sf**|{string}|작업 원본으로 사용할 원본 파일을 지정합니다. 이 매개 변수를 사용하는 경우 다른 원본 매개 변수가 무효화됩니다. |
|**/TargetConnectionString:**|**/tcs**|{string}|대상 데이터베이스에 대한 유효한 SQL Server/Azure 연결 문자열을 지정합니다. 이 매개 변수를 지정한 경우 다른 모든 대상 매개 변수와 단독으로 연결 문자열이 사용됩니다. |
|**/TargetDatabaseName:**|**/tdn**|{string}|sqlpackage.exe 동작의 대상인 데이터베이스의 이름에 대한 재정의를 지정합니다. |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|대상 데이터베이스 연결에 대해 SQL 암호화를 사용할지 여부를 지정합니다. |
|**/TargetPassword:**|**/tp**|{string}|SQL Server 인증 시나리오에서 대상 데이터베이스에 액세스하는 데 사용할 암호를 정의합니다. |
|**/TargetServerName:**|**/tsn**|{string}|대상 데이터베이스를 호스팅하는 서버의 이름을 정의합니다. |
|**/TargetTimeout:**|**/tt**|{int}|대상 데이터베이스에 대한 연결을 설정하는 데 대한 제한 시간(초)을 지정합니다. Azure AD의 경우 이 값을 30초보다 크거나 같게 하는 것이 좋습니다.|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|대상 데이터베이스 연결을 암호화하고 신뢰의 유효성을 검증하기 위한 인증서 체인 검색을 건너뛰는 데 TLS를 사용할지 여부를 지정합니다. |
|**/TargetUser:**|**/tu**|{string}|SQL Server 인증 시나리오에서 대상 데이터베이스에 액세스하는 데 사용할 SQL Server 사용자를 정의합니다. |
|**/TenantId:**|**/tid**|{string}|Azure AD 테넌트 ID 또는 도메인 이름을 나타냅니다. 이 옵션은 outlook.com, hotmail.com 또는 live.com과 같은 Microsoft 계정뿐만 아니라 게스트 또는 가져온 Azure AD 사용자를 지원해야 합니다. 이 매개 변수를 생략하면 인증된 사용자가 이 AD의 기본 사용자라고 가정하여 Azure AD의 기본 테넌트 ID가 사용됩니다. 그러나 이 경우 이 Azure AD에서 호스트되는 모든 게스트 또는 가져온 사용자 및/또는 Microsoft 계정은 지원되지 않으며 작업이 실패합니다. <br/> Active Directory 유니버설 인증에 대한 자세한 내용은 [SQL Database 및 Azure Synapse Analytics에 대한 유니버설 인증(SSMS의 MFA 지원)](/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|유니버설 인증을 사용해야 하는지 여부를 지정합니다. True로 설정되면 대화형 인증 프로토콜이 MFA를 지원하도록 활성화됩니다. 이 옵션은 사용자가 사용자 이름 및 암호 또는 통합 인증(Windows 자격 증명)을 입력해야 하는 대화형 프로토콜을 사용하여 MFA가 없는 Azure AD 인증에도 사용할 수 있습니다. /UniversalAuthentication을 True로 설정하면 SourceConnectionString(/scs)에 Azure AD 인증을 지정할 수 없습니다. /UniversalAuthentication을 False로 설정하면 SourceConnectionString(/scs)에 Azure AD 인증을 지정해야 합니다. <br/> Active Directory 유니버설 인증에 대한 자세한 내용은 [SQL Database 및 Azure Synapse Analytics에 대한 유니버설 인증(SSMS의 MFA 지원)](/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.|

Import 동작과 관련된 속성:

|속성|값|Description|
|---|---|---|
|**/p:**|CommandTimeout=(INT32 '60')|SQL Server에 대한 쿼리를 실행할 때 명령 시간 제한(초)을 지정합니다.|
|**/p:**|DatabaseEdition=({Basic&#124;Standard&#124;Premium&#124;DataWarehouse&#124;GeneralPurpose&#124;BusinessCritical&#124;Hyperscale&#124;Default} 'Default')|Azure SQL Database의 버전을 정의합니다.|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| SQLServer에 대해 쿼리를 실행할 때의 데이터베이스 잠금 시간 제한(초)를 지정합니다. 무기한 대기하려면 -1을 사용합니다.|
|**/p:**|DatabaseMaximumSize=(INT32)|Azure SQL Database의 최대 크기(GB)를 정의합니다.|
|**/p:**|DatabaseServiceObjective=(STRING)|“P0” 또는 “S1”과 같은 Azure SQL Database의 성능 수준을 정의합니다.|
|**/p:**|ImportContributorArguments=(STRING)|배포 참가자에 대한 배포 참가자 인수를 지정합니다. 세미콜론으로 구분된 값의 목록이어야 합니다.|
|**/p:**|ImportContributors=(STRING)|bacpac를 가져올 때 실행되어야 하는 배포 기여자를 지정합니다. 세미콜론으로 구분된 정규화된 빌드 참가자 이름 또는 ID의 목록이어야 합니다.|
|**/p:**|ImportContributorPaths=(STRING)|추가 배포 참가자를 로드할 경로를 지정합니다. 세미콜론으로 구분된 값의 목록이어야 합니다. |
|**/p:**|LongRunningCommandTimeout=(INT32)| SQL Server에 대한 쿼리를 실행할 때 장기 명령 시간 제한(초)을 지정합니다. 무기한 대기하려면 0을 사용합니다.|
|**/p:**|Storage=({File&#124;Memory})|데이터베이스 모델을 생성할 때 요소의 저장 방법을 지정합니다. 성능상의 이유로 기본값은 InMemory입니다. 큰 데이터베이스의 경우 파일 지원 스토리지가 필요합니다.|
  
## <a name="deployreport-parameters-and-properties"></a>DeployReport 매개 변수 및 속성

**SqlPackage.exe** 보고서 작업은 게시 작업으로 변경된 사항의 XML 보고서를 만듭니다.  
  
### <a name="help-for-deployreport-action"></a>DeployReport 동작에 대한 도움말

|매개 변수|약식|값|설명|
|---|---|---|---|
|**/Action:**|**/a**|DeployReport|수행할 작업을 지정합니다. |
|**/AccessToken:**|**/at**|{string}| 대상 데이터베이스에 연결할 때 사용할 액세스 토큰 기반 인증 액세스 토큰을 지정합니다. |
|**/Diagnostics:**|**/d**|{True&#124;False}|진단 로깅이 콘솔로 출력되는지 여부를 지정합니다. 기본값은 False입니다. |
|**/DiagnosticsFile:**|**/df**|{string}|진단 로그를 저장할 파일을 지정합니다. |
|**/MaxParallelism:**|**/mp**|{int}| 데이터베이스에 대해 실행 중인 동시 작업에 대한 병렬 처리 수준을 지정합니다. 기본값은 8입니다. |
|**/OutputPath:**|**/op**|{string}|출력 파일이 생성되는 파일 경로를 지정합니다. |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|sqlpackage.exe이 기존 파일을 덮어써야 할지 여부를 지정합니다. False를 지정하면 기존 파일이 나타나는 경우 sqlpackage.exe에서 작업이 중단됩니다. 기본값은 True입니다. |
|**/Profile:**|**/pr**|{string}|DAC 게시 프로필에 대한 파일 경로를 지정합니다. 프로필은 출력을 생성할 때 사용할 속성 및 변수 컬렉션을 정의합니다. |
|**/Properties:**|**/p**|{PropertyName}={Value}|작업별 속성에 대한 이름 값 쌍을 지정합니다. {PropertyName}={Value}. 해당 작업의 속성 이름을 보려면 특정 작업의 도움말을 참조하십시오. 예: sqlpackage.exe /Action:DeployReport /?. |
|**/Quiet:**|**/q**|{True&#124;False}|자세한 피드백을 무시할지 여부를 지정합니다. 기본값은 False입니다. |
|**/SourceConnectionString:**|**/scs**|{string}|원본 데이터베이스에 대한 유효한 SQL Server/Azure 연결 문자열을 지정합니다. 이 매개 변수를 지정한 경우 다른 모든 원본 매개 변수와 단독으로 연결 문자열이 사용됩니다. |
|**/SourceDatabaseName:**|**/sdn**|{string}|원본 데이터베이스의 이름을 정의합니다. |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|원본 데이터베이스 연결에 대해 SQL 암호화를 사용할지 여부를 지정합니다. |
|**/SourceFile:**|**/sf**|{string}|데이터베이스 대신 작업 원본으로 사용할 원본 파일을 지정합니다. 이 매개 변수를 사용하는 경우 다른 원본 매개 변수가 무효화됩니다. |
|**/SourcePassword:**|**/sp**|{string}|SQL Server 인증 시나리오에서 원본 데이터베이스에 액세스하는 데 사용할 암호를 정의합니다. |
|**/SourceServerName:**|**/ssn**|{string}|원본 데이터베이스를 호스팅하는 서버의 이름을 정의합니다. |
|**/SourceTimeout:**|**/st**|{int}|원본 데이터베이스에 대한 연결을 설정하는 데 대한 제한 시간(초)을 지정합니다. |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|원본 데이터베이스 연결을 암호화하고 신뢰의 유효성을 검증하기 위한 인증서 체인 검색을 건너뛰는 데 TLS를 사용할지 여부를 지정합니다. |
|**/SourceUser:**|**/su**|{string}|SQL Server 인증 시나리오에서 원본 데이터베이스에 액세스하는 데 사용할 SQL Server 사용자를 정의합니다. |
|**/TargetConnectionString:**|**/tcs**|{string}|대상 데이터베이스에 대한 유효한 SQL Server/Azure 연결 문자열을 지정합니다. 이 매개 변수를 지정한 경우 다른 모든 대상 매개 변수와 단독으로 연결 문자열이 사용됩니다. |
|**/TargetDatabaseName:**|**/tdn**|{string}|sqlpackage.exe 동작의 대상인 데이터베이스의 이름에 대한 재정의를 지정합니다. |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|대상 데이터베이스 연결에 대해 SQL 암호화를 사용할지 여부를 지정합니다. |
|**/TargetFile:**|**/tf**|{string}|데이터베이스 대신 작업 대상으로 사용될 대상 파일(.dacpac 파일)을 지정합니다. 이 매개 변수를 사용하는 경우 다른 대상 매개 변수가 무효화됩니다. 이 매개 변수는 데이터베이스 대상만 지원하는 동작에는 유효하지 않습니다.|
|**/TargetPassword:**|**/tp**|{string}|SQL Server 인증 시나리오에서 대상 데이터베이스에 액세스하는 데 사용할 암호를 정의합니다. |
|**/TargetServerName:**|**/tsn**|{string}|대상 데이터베이스를 호스팅하는 서버의 이름을 정의합니다. |
|**/TargetTimeout:**|**/tt**|{int}|대상 데이터베이스에 대한 연결을 설정하는 데 대한 제한 시간(초)을 지정합니다. Azure AD의 경우 이 값을 30초보다 크거나 같게 하는 것이 좋습니다.|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|대상 데이터베이스 연결을 암호화하고 신뢰의 유효성을 검증하기 위한 인증서 체인 검색을 건너뛰는 데 TLS를 사용할지 여부를 지정합니다. |
|**/TargetUser:**|**/tu**|{string}|SQL Server 인증 시나리오에서 대상 데이터베이스에 액세스하는 데 사용할 SQL Server 사용자를 정의합니다. |
|**/TenantId:**|**/tid**|{string}|Azure AD 테넌트 ID 또는 도메인 이름을 나타냅니다. 이 옵션은 outlook.com, hotmail.com 또는 live.com과 같은 Microsoft 계정뿐만 아니라 게스트 또는 가져온 Azure AD 사용자를 지원해야 합니다. 이 매개 변수를 생략하면 인증된 사용자가 이 AD의 기본 사용자라고 가정하여 Azure AD의 기본 테넌트 ID가 사용됩니다. 그러나 이 경우 이 Azure AD에서 호스트되는 모든 게스트 또는 가져온 사용자 및/또는 Microsoft 계정은 지원되지 않으며 작업이 실패합니다. <br/> Active Directory 유니버설 인증에 대한 자세한 내용은 [SQL Database 및 Azure Synapse Analytics에 대한 유니버설 인증(SSMS의 MFA 지원)](/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|유니버설 인증을 사용해야 하는지 여부를 지정합니다. True로 설정되면 대화형 인증 프로토콜이 MFA를 지원하도록 활성화됩니다. 이 옵션은 사용자가 사용자 이름 및 암호 또는 통합 인증(Windows 자격 증명)을 입력해야 하는 대화형 프로토콜을 사용하여 MFA가 없는 Azure AD 인증에도 사용할 수 있습니다. /UniversalAuthentication을 True로 설정하면 SourceConnectionString(/scs)에 Azure AD 인증을 지정할 수 없습니다. /UniversalAuthentication을 False로 설정하면 SourceConnectionString(/scs)에 Azure AD 인증을 지정해야 합니다. <br/> Active Directory 유니버설 인증에 대한 자세한 내용은 [SQL Database 및 Azure Synapse Analytics에 대한 유니버설 인증(SSMS의 MFA 지원)](/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.|
|**/Variables:**|**/v**|{PropertyName}={Value}|작업별 변수에 대한 이름 값 쌍을 지정합니다. {VariableName}={Value}. DACPAC 파일에는 유효한 SQLCMD 변수 목록이 포함됩니다. 모든 변수에 대해 값을 제공하지 않으면 오류가 발생합니다. |

## <a name="properties-specific-to-the-deployreport-action"></a>DeployReport 동작과 관련된 속성

|속성|값|Description|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|배포 참가자에 대한 추가 배포 참가자 인수를 지정합니다. 세미콜론으로 구분된 값의 목록이어야 합니다.|
|**/p:**|AdditionalDeploymentContributors=(STRING)|dacpac가 배포될 때 실행되어야 하는 추가 배포 기여자를 지정합니다. 세미콜론으로 구분된 정규화된 빌드 참가자 이름 또는 ID의 목록이어야 합니다.|
|**/p:**|AdditionalDeploymentContributorPaths=(STRING)| 추가 배포 참가자를 로드할 경로를 지정합니다. 세미콜론으로 구분된 값의 목록이어야 합니다. | 
|**/p:**|AllowDropBlocking Assemblies=(BOOLEAN)|이 속성은 SqlClr 배포에서 배포 계획의 일부로 차단 어셈블리를 삭제하는 데 사용됩니다. 기본적으로 어셈블리를 삭제해야 하는 경우에는 모든 차단/참조 어셈블리가 어셈블리 업데이트를 차단합니다.|
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|SQL Server 플랫폼이 호환되지 않을 수 있는 경우에도 작업을 시도해야 하는지 여부를 지정합니다.|
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|이 속성이 True로 설정되어 있으면 행 수준 보안이 설정된 테이블에서 데이터 이동을 차단하지 않습니다. 기본값은 false입니다.|
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|변경 내용을 배포하기 전 데이터베이스를 백업합니다.|
|**/p:**|BlockOnPossibleDataLoss=(BOOLEAN 'True')|publish.operation으로 인해 데이터 손실이 발생할 수 있는 경우 게시 에피소드를 종료할지 여부를 지정합니다.|
|**/p:**|BlockWhenDriftDetected=(BOOLEAN 'True')|스키마가 더 이상 해당 등록과 일치하지 않거나 등록이 해제된 데이터베이스 업데이트를 차단할지 여부를 지정합니다. |
|**/p:**|CommandTimeout=(INT32 '60')|SQL Server에 대한 쿼리를 실행할 때 명령 시간 제한(초)을 지정합니다. |
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|생성된 게시 스크립트에서 SETVAR 변수 선언을 주석 처리할지 여부를 지정합니다. 게시할 때 SQLCMD.EXE 등의 도구를 사용하여 명령줄에 값을 지정하려는 경우 이와 같이 할 수 있습니다. |
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|이 설정은 배포 중 데이터베이스의 데이터 정렬 처리 방법을 지정합니다.기본적으로 원본에서 지정하는 데이터 정렬과 일치하지 않을 경우 대상 데이터베이스의 데이터 정렬이 업데이트됩니다. 이 옵션을 설정하면 대상 데이터베이스(또는 서버)의 데이터 정렬이 사용됩니다. |
|**/p:**|CreateNewDatabase=(BOOLEAN)|데이터베이스에 게시할 때 대상 데이터베이스를 업데이트할지 또는 삭제 후 다시 만들지 여부를 지정합니다. |
|**/p:**|DatabaseEdition=({Basic&#124;Standard&#124;Premium&#124;DataWarehouse&#124;GeneralPurpose&#124;BusinessCritical&#124;Hyperscale&#124;Default} 'Default')|Azure SQL Database의 버전을 정의합니다.|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| SQLServer에 대해 쿼리를 실행할 때의 데이터베이스 잠금 시간 제한(초)를 지정합니다. 무기한 대기하려면 -1을 사용합니다.|
|**/p:**|DatabaseMaximumSize=(INT32)|Azure SQL Database의 최대 크기(GB)를 정의합니다.|
|**/p:**|DatabaseServiceObjective=(STRING)|“P0” 또는 “S1”과 같은 Azure SQL Database의 성능 수준을 정의합니다. |
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|True인 경우 배포 전에 데이터베이스가 단일 사용자 모드로 설정됩니다. |
|**/p:**|DisableAndReenableDdlTriggers=(BOOLEAN 'True')| 게시 프로세스가 시작할 때 DDL(데이터 정의 언어) 트리거를 사용하지 않고 게시 작업이 끝날 때 다시 사용할지 여부를 지정합니다.|
|**/p:**|DoNotAlterChangeDataCaptureObjects=(BOOLEAN 'True')|True인 경우 변경 데이터 캡처 개체가 수정되지 않습니다.|
|**/p:**|DoNotAlterReplicatedObjects=(BOOLEAN 'True')|복제된 개체를 확인 중에 식별할지 여부를 지정합니다.|
|**/p:**|DoNotDropObjectType=(STRING)|DropObjectsNotInSource가 true인 경우 삭제하지 않아야 하는 개체 형식입니다. 유효한 개체 유형 이름은 Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers입니다. |
|**/p:**|DoNotDropObjectTypes=(STRING)|DropObjectsNotInSource가 true인 경우 삭제하지 않아야 하는 개체 형식을 세미콜론으로 구분한 목록입니다. 유효한 개체 유형 이름은 Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers입니다.|
|**/p:**|DropConstraintsNotInSource=(BOOLEAN 'True')|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 제약 조건을 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropDmlTriggersNotInSource=(BOOLEAN 'True')|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 DML 트리거를 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropExtendedPropertiesNotInSource=(BOOLEAN 'True')|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 확장 속성을 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropIndexesNotInSource=(BOOLEAN 'True')|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 인덱스를 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 개체를 대상 데이터베이스에서 삭제할지 여부를 지정합니다. 이 값은 DropExtendedProperties보다 우선적으로 적용됩니다.|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|데이터베이스에 업데이트를 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 권한을 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|데이터베이스에 업데이트를 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 정의되지 않은 역할 멤버를 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropStatisticsNotInSource=(BOOLEAN 'True')|데이터베이스 스냅샷(.dacpac) 파일에 없는 통계를 데이터베이스에 게시할 때 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|ExcludeObjectType=(STRING)|배포 중에 무시되어야 하는 개체 유형입니다. 유효한 개체 유형 이름은 Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers입니다.|
|**/p:**|ExcludeObjectTypes=(STRING)|배포 중에 무시되어야 하는 개체 유형의 세미콜론으로 구분된 목록입니다. 유효한 개체 유형 이름은 Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers입니다.|
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|데이터가 들어 있는 테이블을 Null 값을 허용하지 않는 열로 업데이트할 때 자동으로 기본 값을 제공합니다.|
|**/p:**|IgnoreAnsiNulls=(BOOLEAN 'True')|데이터베이스에 게시할 때 ANSI NULLS 설정에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|데이터베이스에 게시할 때 권한 부여자를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|데이터베이스에 게시할 때 열 데이터 정렬의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|데이터베이스에 게시할 때 테이블 열 순서의 차이를 무시해야 할지 아니면 업데이트해야 할지를 지정합니다.|
|**/p:**|IgnoreComments=(BOOLEAN)|데이터베이스에 게시할 때 주석의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreCryptographicProviderFilePath=(BOOLEAN 'True')|데이터베이스에 게시할 때 암호화 공급자에 대한 파일 경로의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|데이터베이스 또는 서버에 게시할 때 DDL(Data Definition Language) 트리거 순서의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|데이터베이스에 게시할 때 DDL(Data Definition Language) 트리거 사용/사용 안 함 상태의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|데이터베이스에 게시할 때 기본 스키마의 차이를 무시할지 또는 업데이트할지를 지정합니다. |
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|데이터베이스에 게시할 때 DML(Data Manipulation Language) 트리거 순서의 차이를 무시할지 또는 업데이트할지를 지정합니다.| 
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|데이터베이스에 게시할 때 DML 트리거 사용/사용 안 함 상태의 차이를 무시할지 또는 업데이트할지를 지정합니다. |
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|데이터베이스에 게시할 때 확장 속성의 차이를 무시할지 또는 업데이트할지를 지정합니다. |
|**/p:**|IgnoreFileAndLogFilePath=(BOOLEAN 'True')|데이터베이스에 게시할 때 파일 및 로그 파일에 대한 경로의 차이를 무시할지 또는 업데이트할지를 지정합니다. |
|**/p:**|IgnoreFilegroupPlacement=(BOOLEAN 'True')|데이터베이스에 게시할 때 FILEGROUP에서의 개체 배치에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.| 
|**/p:**|IgnoreFileSize=(BOOLEAN 'True')|데이터베이스에 게시할 때 파일 크기의 차이를 무시할지 또는 경고를 발생하도록 할지를 지정합니다. |
|**/p:**|IgnoreFillFactor=(BOOLEAN 'True')|데이터베이스에 게시할 때 인덱스 스토리지의 채우기 비율에 대한 차이를 무시할지 또는 경고를 발생하도록 할지를 지정합니다.|
|**/p:**|IgnoreFullTextCatalogFilePath=(BOOLEAN 'True')|데이터베이스에 게시할 때 인덱스 저장소의 채우기 비율에 대한 차이를 무시할지 또는 경고를 발생하도록 할지를 지정합니다.| 
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|데이터베이스에 게시할 때 ID 열의 시드에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다. |
|**/p:**|IgnoreIncrement=(BOOLEAN)|데이터베이스에 게시할 때 ID 열의 증가값에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다. |
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|데이터베이스에 게시할 때 인덱스 옵션의 차이를 무시할지 또는 업데이트할지를 지정합니다. |
|**/p:**|IgnoreIndexPadding=(BOOLEAN 'True')|데이터베이스에 게시할 때 인덱스 패딩의 차이를 무시할지 또는 업데이트할지를 지정합니다. |
|**/p:**|IgnoreKeywordCasing=(BOOLEAN 'True')|데이터베이스에 게시할 때 키워드의 대/소문자 구분에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다. |
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|데이터베이스에 게시할 때 인덱스의 잠금 힌트의 차이를 무시 또는 업데이트할지 여부를 지정합니다. |
|**/p:**|IgnoreLoginSids=(BOOLEAN 'True')| 데이터베이스에 게시할 때 SID(보안 ID)의 차이를 무시할지 또는 업데이트할지를 지정합니다.| 
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|데이터베이스에 게시할 때 복제용 아님 설정을 무시할지 또는 업데이트할지를 지정합니다. |
|**/p:**|IgnoreObjectPlacementOnPartitionScheme=(BOOLEAN 'True')|데이터베이스에 게시할 때 파티션 구성표에서 개체의 배치를 무시할지 또는 업데이트할지를 지정합니다.|
 |**/p:**|IgnorePartitionSchemes=(BOOLEAN)|데이터베이스에 게시할 때 분할 구성표와 함수의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnorePermissions=(BOOLEAN)|데이터베이스에 게시할 때 사용 권한의 차이를 무시할지 또는 업데이트할지를 지정합니다. |
|**/p:**|IgnoreQuotedIdentifiers=(BOOLEAN 'True')|데이터베이스에 게시할 때 따옴표 붙은 식별자 설정의 차이를 무시할지 또는 업데이트할지를 지정합니다. |
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|데이터베이스에 게시할 때 로그인의 역할 멤버 자격 차이를 무시 또는 업데이트할지 여부를 지정합니다. |
|**/p:**|IgnoreRouteLifetime=(BOOLEAN 'True')|데이터베이스에 게시할 때 SQL Server가 라우팅 테이블에 경로를 유지하는 시간에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreSemicolonBetweenStatements=(BOOLEAN 'True')|데이터베이스에 게시할 때 T-SQL 문 사이의 세미콜론의 차이를 무시할지 또는 업데이트할지를 지정합니다.| 
|**/p:**|IgnoreTableOptions=(BOOLEAN)|데이터베이스에 게시할 때 테이블 옵션의 차이를 무시할지 또는 업데이트할지를 지정합니다.| 
|**/p:**|IgnoreTablePartitionOptions=(BOOLEAN)|데이터베이스에 게시할 때 테이블 파티션 옵션의 차이를 무시할지 또는 업데이트할지를 지정합니다.  이 옵션은 Azure Synapse Analytics 데이터 웨어하우스 데이터베이스에만 적용됩니다.|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|데이터베이스에 게시할 때 사용자 설정 개체의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreWhitespace=(BOOLEAN 'True')|데이터베이스에 게시할 때 공백의 차이를 무시할지 또는 업데이트할지를 지정합니다. |
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|데이터베이스에 게시할 때 CHECK 제약 조건의 WITH NOCHECK 절에 대한 값의 차이를 무시할지 또는 업데이트할지를 지정합니다.| 
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|데이터베이스에 게시할 때 외래 키의 WITH NOCHECK 절에 대한 값의 차이를 무시할지 또는 업데이트할지를 지정합니다.| 
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|모든 복합 요소를 단일 게시 작업의 일부로 포함합니다.|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|데이터베이스에 게시할 때 가능한 위치에 트랜잭션 문을 사용할지 여부를 지정합니다.|
|**/p:**|LongRunningCommandTimeout=(INT32)| SQL Server에 대한 쿼리를 실행할 때 장기 명령 시간 제한(초)을 지정합니다. 무기한 대기하려면 0을 사용합니다.|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|차이가 있을 경우 ALTER ASSEMBLY 문을 실행하는 대신 게시에서 항상 어셈블리를 삭제하고 다시 만들지를 지정합니다. |
|**/p:**|PopulateFilesOnFileGroups=(BOOLEAN 'True')|대상 데이터베이스에 새 FileGroup이 만들어질 때 새 파일도 만들어지는지 여부를 지정합니다. |
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|스키마가 데이터베이스 서버에 등록되었는지 여부를 지정합니다. 
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|다른 작업이 실행될때 DeploymentPlanExecutor 기여자를 실행할지 여부를 지정합니다.|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|데이터베이스에 게시할 때 데이터베이스 데이터 정렬의 차이를 무시할지, 업데이트할지를 지정합니다. |
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|데이터베이스에 게시할 때 데이터베이스 호환성의 차이를 무시할지 또는 업데이트할지를 지정합니다. |
|**/p:**|ScriptDatabaseOptions=(BOOLEAN 'True')|게시 동작의 일부로 대상 데이터베이스 속성을 설정 또는 업데이트할지 여부를 지정합니다. |
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|데이터베이스 이름 및 서버 이름이 데이터베이스 프로젝트에 지정된 이름과 일치하는지 확인하는 문을 게시 스크립트에 생성할지 여부를 지정합니다.|
|**/p:**|ScriptFileSize=(BOOLEAN)|파일 그룹에 파일을 추가할 때 크기를 지정하는지 여부를 제어합니다. |
|**/p:**|ScriptNewConstraintValidation=(BOOLEAN 'True')|게시 마지막에 모든 제약 조건은 하나의 집합으로 확인되므로 게시 중간에 검사 또는 외래 키 제약 조건으로 인한 데이터 오류가 발생하지 않습니다. False로 설정하면 해당 데이터를 확인하지 않고 제약 조건이 게시됩니다.|
|**/p:**|ScriptRefreshModule=(BOOLEAN 'True')|게시 스크립트의 끝에 새로 고침 문을 포함합니다.|
|**/p:**|Storage=({File&#124;Memory})|데이터베이스 모델을 생성할 때 요소의 저장 방법을 지정합니다. 성능상의 이유로 기본값은 InMemory입니다. 큰 데이터베이스의 경우 파일 지원 스토리지가 필요합니다.|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|확인을 경고로 처리해야 하는 동안 발생한 오류를 게시하는지 여부를 지정합니다. 생성된 배포 계획을 대상 데이터베이스에 대해 실행하기 전에 해당 계획에 대한 확인이 수행됩니다. 계획 확인에서 대상 전용 개체(예: 인덱스)가 없는 등의 문제가 발견되면 해당 계획을 삭제하여 변경해야 합니다. 또한 복합 프로젝트에 대한 참조로 인한 종속성(예: 테이블, 뷰)이 존재하지만 대상 데이터베이스에는 존재하지 않는 상황도 확인됩니다. 첫 번째 오류에서 게시 동작을 중지하는 대신 모든 문제의 전체 목록을 가져오려면 이 작업을 수행하도록 선택할 수 있습니다. |
|**/p:**|UnmodifiableObjectWarnings=(BOOLEAN 'True')|개체에서 수정할 수 없는 차이가 발견될 경우(예: 파일 경로 또는 파일 크기가 특정 파일에서 다른 경우) 경고를 생성할지 여부를 지정합니다.| 
|**/p:**|VerifyCollationCompatibility=(BOOLEAN 'True')|데이터 정렬 호환성이 확인되는지 여부를 지정합니다.| 
|**/p:**|VerifyDeployment=(BOOLEAN 'True')|성공적인 게시를 차단할 수 있는 문제가 존재할 경우 게시 작업을 중단하는 검사를 게시 전에 수행할지 여부를 지정합니다. 예를 들어 데이터베이스 프로젝트에 존재하지 않고 게시할 때 오류를 일으키는 외래 키를 대상 데이터베이스에 설정한 경우 게시 작업이 중단될 수 있습니다. |
  
## <a name="driftreport-parameters"></a>DriftReport 매개 변수

**SqlPackage.exe** 보고서 작업은 마지막으로 등록된 후에 등록된 데이터베이스에 변경된 사항의 XML 보고서를 만듭니다.  
  
### <a name="help-for-driftreport-action"></a>DriftReport 동작에 대한 도움말

|매개 변수|약식|값|설명|
|---|---|---|---|
|**/Action:**|**/a**|DriftReport|수행할 작업을 지정합니다. |
|**/AccessToken:**|**/at**|{string}| 대상 데이터베이스에 연결할 때 사용할 액세스 토큰 기반 인증 액세스 토큰을 지정합니다. |
|**/Diagnostics:**|**/d**|{True&#124;False}|진단 로깅이 콘솔로 출력되는지 여부를 지정합니다. 기본값은 False입니다. |
|**/DiagnosticsFile:**|**/df**|{string}|진단 로그를 저장할 파일을 지정합니다. |
|**/MaxParallelism:**|**/mp**|{int}| 데이터베이스에 대해 실행 중인 동시 작업에 대한 병렬 처리 수준을 지정합니다. 기본값은 8입니다. |
|**/OutputPath:**|**/op**|{string}|출력 파일이 생성되는 파일 경로를 지정합니다. |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|sqlpackage.exe이 기존 파일을 덮어써야 할지 여부를 지정합니다. False를 지정하면 기존 파일이 나타나는 경우 sqlpackage.exe에서 작업이 중단됩니다. 기본값은 True입니다. |
|**/Quiet:**|**/q**|{True&#124;False}|자세한 피드백을 무시할지 여부를 지정합니다. 기본값은 False입니다.|
|**/TargetConnectionString:**|**/tcs**|{string}|대상 데이터베이스에 대한 유효한 SQL Server/Azure 연결 문자열을 지정합니다. 이 매개 변수를 지정한 경우 다른 모든 대상 매개 변수와 단독으로 연결 문자열이 사용됩니다. |
|**/TargetDatabaseName:**|**/tdn**|{string}|sqlpackage.exe 동작의 대상인 데이터베이스의 이름에 대한 재정의를 지정합니다. |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|대상 데이터베이스 연결에 대해 SQL 암호화를 사용할지 여부를 지정합니다. |
|**/TargetPassword:**|**/tp**|{string}|SQL Server 인증 시나리오에서 대상 데이터베이스에 액세스하는 데 사용할 암호를 정의합니다. |
|**/TargetServerName:**|**/tsn**|{string}|대상 데이터베이스를 호스팅하는 서버의 이름을 정의합니다. |
|**/TargetTimeout:**|**/tt**|{int}|대상 데이터베이스에 대한 연결을 설정하는 데 대한 제한 시간(초)을 지정합니다. Azure AD의 경우 이 값을 30초보다 크거나 같게 하는 것이 좋습니다.|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|대상 데이터베이스 연결을 암호화하고 신뢰의 유효성을 검증하기 위한 인증서 체인 검색을 건너뛰는 데 TLS를 사용할지 여부를 지정합니다. |
|**/TargetUser:**|**/tu**|{string}|SQL Server 인증 시나리오에서 대상 데이터베이스에 액세스하는 데 사용할 SQL Server 사용자를 정의합니다. |
|**/TenantId:**|**/tid**|{string}|Azure AD 테넌트 ID 또는 도메인 이름을 나타냅니다. 이 옵션은 outlook.com, hotmail.com 또는 live.com과 같은 Microsoft 계정뿐만 아니라 게스트 또는 가져온 Azure AD 사용자를 지원해야 합니다. 이 매개 변수를 생략하면 인증된 사용자가 이 AD의 기본 사용자라고 가정하여 Azure AD의 기본 테넌트 ID가 사용됩니다. 그러나 이 경우 이 Azure AD에서 호스트되는 모든 게스트 또는 가져온 사용자 및/또는 Microsoft 계정은 지원되지 않으며 작업이 실패합니다. <br/> Active Directory 유니버설 인증에 대한 자세한 내용은 [SQL Database 및 Azure Synapse Analytics에 대한 유니버설 인증(SSMS의 MFA 지원)](/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|유니버설 인증을 사용해야 하는지 여부를 지정합니다. True로 설정되면 대화형 인증 프로토콜이 MFA를 지원하도록 활성화됩니다. 이 옵션은 사용자가 사용자 이름 및 암호 또는 통합 인증(Windows 자격 증명)을 입력해야 하는 대화형 프로토콜을 사용하여 MFA가 없는 Azure AD 인증에도 사용할 수 있습니다. /UniversalAuthentication을 True로 설정하면 SourceConnectionString(/scs)에 Azure AD 인증을 지정할 수 없습니다. /UniversalAuthentication을 False로 설정하면 SourceConnectionString(/scs)에 Azure AD 인증을 지정해야 합니다. <br/> Active Directory 유니버설 인증에 대한 자세한 내용은 [SQL Database 및 Azure Synapse Analytics에 대한 유니버설 인증(SSMS의 MFA 지원)](/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.|

## <a name="script-parameters-and-properties"></a>스크립트 매개 변수 및 속성

**SqlPackage.exe** 스크립트 작업은 대상 데이터베이스의 스키마가 원본 데이터베이스 스키마와 일치하도록 업데이트하는 Transact-SQL 증분 업데이트 스크립트를 만듭니다.  
  
### <a name="help-for-the-script-action"></a>Script 동작에 대한 도움말

|매개 변수|약식|값|설명|
|---|---|---|---|
|**/Action:**|**/a**|스크립트|수행할 작업을 지정합니다. |
|**/AccessToken:**|**/at**|{string}| 대상 데이터베이스에 연결할 때 사용할 액세스 토큰 기반 인증 액세스 토큰을 지정합니다. |
|**/DeployScriptPath:**|**/dsp**|{string}|배포 스크립트를 출력할 선택적 파일 경로를 지정합니다. Azure 배포의 경우 master 데이터베이스를 만들거나 수정하는 TSQL 명령이 있을 경우 스크립트가 동일한 경로에 작성되지만 “Filename_Master.sql”을 출력 파일 이름으로 사용합니다. |
|**/DeployReportPath:**|**/drp**|{string}|배포 보고서 xml 파일을 출력할 선택적 파일 경로를 지정합니다. |
|**/Diagnostics:**|**/d**|{True&#124;False}|진단 로깅이 콘솔로 출력되는지 여부를 지정합니다. 기본값은 False입니다. |
|**/DiagnosticsFile:**|**/df**|{string}|진단 로그를 저장할 파일을 지정합니다. |
|**/MaxParallelism:**|**/mp**|{int}| 데이터베이스에 대해 실행 중인 동시 작업에 대한 병렬 처리 수준을 지정합니다. 기본값은 8입니다. |
|**/OutputPath:**|**/op**|{string}|출력 파일이 생성되는 파일 경로를 지정합니다. |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|sqlpackage.exe이 기존 파일을 덮어써야 할지 여부를 지정합니다. False를 지정하면 기존 파일이 나타나는 경우 sqlpackage.exe에서 작업이 중단됩니다. 기본값은 True입니다. |
|**/Profile:**|**/pr**|{string}|DAC 게시 프로필에 대한 파일 경로를 지정합니다. 프로필은 출력을 생성할 때 사용할 속성 및 변수 컬렉션을 정의합니다.|
|**/Properties:**|**/p**|{PropertyName}={Value}|작업별 속성에 대한 이름 값 쌍을 지정합니다. {PropertyName}={Value}. 해당 작업의 속성 이름을 보려면 특정 작업의 도움말을 참조하십시오. 예: sqlpackage.exe /Action:Script /?.|
|**/Quiet:**|**/q**|{True&#124;False}|자세한 피드백을 무시할지 여부를 지정합니다. 기본값은 False입니다.|
|**/SourceConnectionString:**|**/scs**|{string}|원본 데이터베이스에 대한 유효한 SQL Server/Azure 연결 문자열을 지정합니다. 이 매개 변수를 지정한 경우 다른 모든 원본 매개 변수와 단독으로 연결 문자열이 사용됩니다. |
|**/SourceDatabaseName:**|**/sdn**|{string}|원본 데이터베이스의 이름을 정의합니다. |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|원본 데이터베이스 연결에 대해 SQL 암호화를 사용할지 여부를 지정합니다. |
|**/SourceFile:**|**/sf**|{string}|작업 원본으로 사용할 원본 파일을 지정합니다. 이 매개 변수를 사용하는 경우 다른 원본 매개 변수가 무효화됩니다. |
|**/SourcePassword:**|**/sp**|{string}|SQL Server 인증 시나리오에서 원본 데이터베이스에 액세스하는 데 사용할 암호를 정의합니다. |
|**/SourceServerName:**|**/ssn**|{string}|원본 데이터베이스를 호스팅하는 서버의 이름을 정의합니다. |
|**/SourceTimeout:**|**/st**|{int}|원본 데이터베이스에 대한 연결을 설정하는 데 대한 제한 시간(초)을 지정합니다. |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|원본 데이터베이스 연결을 암호화하고 신뢰의 유효성을 검증하기 위한 인증서 체인 검색을 건너뛰는 데 TLS를 사용할지 여부를 지정합니다. |
|**/SourceUser:**|**/su**|{string}|SQL Server 인증 시나리오에서 원본 데이터베이스에 액세스하는 데 사용할 SQL Server 사용자를 정의합니다. |
|**/TargetConnectionString:**|**/tcs**|{string}|대상 데이터베이스에 대한 유효한 SQL Server/Azure 연결 문자열을 지정합니다. 이 매개 변수를 지정한 경우 다른 모든 대상 매개 변수와 단독으로 연결 문자열이 사용됩니다. |
|**/TargetDatabaseName:**|**/tdn**|{string}|sqlpackage.exe 동작의 대상인 데이터베이스의 이름에 대한 재정의를 지정합니다. |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|대상 데이터베이스 연결에 대해 SQL 암호화를 사용할지 여부를 지정합니다. |
|**/TargetFile:**|**/tf**|{string}| 데이터베이스 대신 작업 대상으로 사용될 대상 파일(.dacpac 파일)을 지정합니다. 이 매개 변수를 사용하는 경우 다른 대상 매개 변수가 무효화됩니다. 이 매개 변수는 데이터베이스 대상만 지원하는 동작에는 유효하지 않습니다.|
|**/TargetPassword:**|**/tp**|{string}|SQL Server 인증 시나리오에서 대상 데이터베이스에 액세스하는 데 사용할 암호를 정의합니다. |
|**/TargetServerName:**|**/tsn**|{string}|대상 데이터베이스를 호스팅하는 서버의 이름을 정의합니다. |
|**/TargetTimeout:**|**/tt**|{int}|대상 데이터베이스에 대한 연결을 설정하는 데 대한 제한 시간(초)을 지정합니다. Azure AD의 경우 이 값을 30초보다 크거나 같게 하는 것이 좋습니다.|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|대상 데이터베이스 연결을 암호화하고 신뢰의 유효성을 검증하기 위한 인증서 체인 검색을 건너뛰는 데 TLS를 사용할지 여부를 지정합니다. |
|**/TargetUser:**|**/tu**|{string}|SQL Server 인증 시나리오에서 대상 데이터베이스에 액세스하는 데 사용할 SQL Server 사용자를 정의합니다. |
|**/TenantId:**|**/tid**|{string}|Azure AD 테넌트 ID 또는 도메인 이름을 나타냅니다. 이 옵션은 outlook.com, hotmail.com 또는 live.com과 같은 Microsoft 계정뿐만 아니라 게스트 또는 가져온 Azure AD 사용자를 지원해야 합니다. 이 매개 변수를 생략하면 인증된 사용자가 이 AD의 기본 사용자라고 가정하여 Azure AD의 기본 테넌트 ID가 사용됩니다. 그러나 이 경우 이 Azure AD에서 호스트되는 모든 게스트 또는 가져온 사용자 및/또는 Microsoft 계정은 지원되지 않으며 작업이 실패합니다. <br/> Active Directory 유니버설 인증에 대한 자세한 내용은 [SQL Database 및 Azure Synapse Analytics에 대한 유니버설 인증(SSMS의 MFA 지원)](/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|유니버설 인증을 사용해야 하는지 여부를 지정합니다. True로 설정되면 대화형 인증 프로토콜이 MFA를 지원하도록 활성화됩니다. 이 옵션은 사용자가 사용자 이름 및 암호 또는 통합 인증(Windows 자격 증명)을 입력해야 하는 대화형 프로토콜을 사용하여 MFA가 없는 Azure AD 인증에도 사용할 수 있습니다. /UniversalAuthentication을 True로 설정하면 SourceConnectionString(/scs)에 Azure AD 인증을 지정할 수 없습니다. /UniversalAuthentication을 False로 설정하면 SourceConnectionString(/scs)에 Azure AD 인증을 지정해야 합니다. <br/> Active Directory 유니버설 인증에 대한 자세한 내용은 [SQL Database 및 Azure Synapse Analytics에 대한 유니버설 인증(SSMS의 MFA 지원)](/azure/sql-database/sql-database-ssms-mfa-authentication)을 참조하세요.|
|**/Variables:**|**/v**|{PropertyName}={Value}|작업별 변수에 대한 이름 값 쌍을 지정합니다. {VariableName}={Value}. DACPAC 파일에는 유효한 SQLCMD 변수 목록이 포함됩니다. 모든 변수에 대해 값을 제공하지 않으면 오류가 발생합니다. |

### <a name="properties-specific-to-the-script-action"></a>Script 동작과 관련된 속성

|속성|값|Description|
|---|---|---|
|**/p:**|AdditionalDeploymentContributorArguments=(STRING)|배포 참가자에 대한 추가 배포 참가자 인수를 지정합니다. 세미콜론으로 구분된 값의 목록이어야 합니다.
|**/p:**|AdditionalDeploymentContributors=(STRING)|dacpac가 배포될 때 실행되어야 하는 추가 배포 기여자를 지정합니다. 세미콜론으로 구분된 정규화된 빌드 참가자 이름 또는 ID의 목록이어야 합니다.
|**/p:**|AdditionalDeploymentContributorPaths=(STRING)| 추가 배포 참가자를 로드할 경로를 지정합니다. 세미콜론으로 구분된 값의 목록이어야 합니다. | 
|**/p:**|AllowDropBlockingAssemblies=(BOOLEAN)|이 속성은 SqlClr 배포에서 배포 계획의 일부로 차단 어셈블리를 삭제하는 데 사용됩니다. 기본적으로 어셈블리를 삭제해야 하는 경우에는 모든 차단/참조 어셈블리가 어셈블리 업데이트를 차단합니다.
|**/p:**|AllowIncompatiblePlatform=(BOOLEAN)|SQL Server 플랫폼이 호환되지 않을 수 있는 경우에도 작업을 시도해야 하는지 여부를 지정합니다.
|**/p:**|AllowUnsafeRowLevelSecurityDataMovement=(BOOLEAN)|이 속성이 True로 설정되어 있으면 행 수준 보안이 설정된 테이블에서 데이터 이동을 차단하지 않습니다. 기본값은 false입니다.
|**/p:**|BackupDatabaseBeforeChanges=(BOOLEAN)|변경 내용을 배포하기 전 데이터베이스를 백업합니다.
|**/p:**|BlockOnPossibleDataLoss=(BOOLEAN 'True')|publish.operation으로 인해 데이터 손실이 발생할 수 있는 경우 게시 에피소드를 종료할지 여부를 지정합니다.
|**/p:**|BlockWhenDriftDetected=(BOOLEAN 'True')|스키마가 더 이상 해당 등록과 일치하지 않거나 등록이 해제된 데이터베이스 업데이트를 차단할지 여부를 지정합니다.
|**/p:**|CommandTimeout=(INT32 '60')|SQL Server에 대한 쿼리를 실행할 때 명령 시간 제한(초)을 지정합니다.
|**/p:**|CommentOutSetVarDeclarations=(BOOLEAN)|생성된 게시 스크립트에서 SETVAR 변수 선언을 주석 처리할지 여부를 지정합니다. 게시할 때 SQLCMD.EXE 등의 도구를 사용하여 명령줄에 값을 지정하려는 경우 이와 같이 할 수 있습니다.
|**/p:**|CompareUsingTargetCollation=(BOOLEAN)|이 설정은 배포 중 데이터베이스의 데이터 정렬 처리 방법을 지정합니다.기본적으로 원본에서 지정하는 데이터 정렬과 일치하지 않을 경우 대상 데이터베이스의 데이터 정렬이 업데이트됩니다. 이 옵션을 설정하면 대상 데이터베이스(또는 서버)의 데이터 정렬이 사용됩니다.|
|**/p:**|CreateNewDatabase=(BOOLEAN)|데이터베이스에 게시할 때 대상 데이터베이스를 업데이트할지 또는 삭제 후 다시 만들지 여부를 지정합니다.
|**/p:**|DatabaseEdition=({Basic&#124;Standard&#124;Premium&#124;DataWarehouse&#124;GeneralPurpose&#124;BusinessCritical&#124;Hyperscale&#124;Default} 'Default')|Azure SQL Database의 버전을 정의합니다.|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| SQLServer에 대해 쿼리를 실행할 때의 데이터베이스 잠금 시간 제한(초)를 지정합니다. 무기한 대기하려면 -1을 사용합니다.|
|**/p:**|DatabaseMaximumSize=(INT32)|Azure SQL Database의 최대 크기(GB)를 정의합니다.
|**/p:**|DatabaseServiceObjective=(STRING)|“P0” 또는 “S1”과 같은 Azure SQL Database의 성능 수준을 정의합니다.
|**/p:**|DeployDatabaseInSingleUserMode=(BOOLEAN)|True인 경우 배포 전에 데이터베이스가 단일 사용자 모드로 설정됩니다.
|**/p:**|DisableAndReenableDdlTriggers=(BOOLEAN 'True')| 게시 프로세스가 시작할 때 DDL(데이터 정의 언어) 트리거를 사용하지 않고 게시 작업이 끝날 때 다시 사용할지 여부를 지정합니다.|
|**/p:**|DoNotAlterChangeDataCaptureObjects=(BOOLEAN 'True')|True인 경우 변경 데이터 캡처 개체가 수정되지 않습니다.
|**/p:**|DoNotAlterReplicatedObjects=(BOOLEAN 'True')|복제된 개체를 확인 중에 식별할지 여부를 지정합니다.
|**/p:**|DoNotDropObjectType=(STRING)|DropObjectsNotInSource가 true인 경우 삭제하지 않아야 하는 개체 형식입니다. 유효한 개체 유형 이름은 Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers입니다.
|**/p:**|DoNotDropObjectTypes=(STRING)|DropObjectsNotInSource가 true인 경우 삭제하지 않아야 하는 개체 형식을 세미콜론으로 구분한 목록입니다. 유효한 개체 유형 이름은 Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers입니다.
|**/p:**|DropConstraintsNotInSource=(BOOLEAN 'True')|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 제약 조건을 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropDmlTriggersNotInSource=(BOOLEAN 'True')|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 DML 트리거를 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropExtendedPropertiesNotInSource=(BOOLEAN 'True')|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 확장 속성을 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropIndexesNotInSource=(BOOLEAN 'True')|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 인덱스를 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropObjectsNotInSource=(BOOLEAN)|데이터베이스에 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 개체를 대상 데이터베이스에서 삭제할지 여부를 지정합니다. 이 값은 DropExtendedProperties보다 우선적으로 적용됩니다.|
|**/p:**|DropPermissionsNotInSource=(BOOLEAN)|데이터베이스에 업데이트를 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 없는 권한을 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropRoleMembersNotInSource=(BOOLEAN)|데이터베이스에 업데이트를 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 정의되지 않은 역할 멤버를 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|DropStatisticsNotInSource=(BOOLEAN 'True')|데이터베이스에 업데이트를 게시할 때 데이터베이스 스냅샷(.dacpac) 파일에 정의되지 않은 역할 멤버를 대상 데이터베이스에서 삭제할지 여부를 지정합니다.|
|**/p:**|ExcludeObjectType=(STRING)|배포 중에 무시되어야 하는 개체 유형입니다. 유효한 개체 유형 이름은 Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers입니다.
|**/p:**|ExcludeObjectTypes=(STRING)|배포 중에 무시되어야 하는 개체 유형의 세미콜론으로 구분된 목록입니다. 유효한 개체 유형 이름은 Aggregates, ApplicationRoles, Assemblies, AsymmetricKeys, BrokerPriorities, Certificates, ColumnEncryptionKeys, ColumnMasterKeys, Contracts, DatabaseRoles, DatabaseTriggers, Defaults, ExtendedProperties, ExternalDataSources, ExternalFileFormats, ExternalTables, Filegroups, FileTables, FullTextCatalogs, FullTextStoplists, MessageTypes, PartitionFunctions, PartitionSchemes, Permissions, Queues, RemoteServiceBindings, RoleMembership, Rules, ScalarValuedFunctions, SearchPropertyLists, SecurityPolicies, Sequences, Services, Signatures, StoredProcedures, SymmetricKeys, Synonyms, Tables, TableValuedFunctions, UserDefinedDataTypes, UserDefinedTableTypes, ClrUserDefinedTypes, Users, Views, XmlSchemaCollections, Audits, Credentials, CryptographicProviders, DatabaseAuditSpecifications, DatabaseScopedCredentials, Endpoints, ErrorMessages, EventNotifications, EventSessions, LinkedServerLogins, LinkedServers, Logins, Routes, ServerAuditSpecifications, ServerRoleMembership, ServerRoles, ServerTriggers입니다.
|**/p:**|GenerateSmartDefaults=(BOOLEAN)|데이터가 들어 있는 테이블을 Null 값을 허용하지 않는 열로 업데이트할 때 자동으로 기본 값을 제공합니다.
|**/p:**|IgnoreAnsiNulls=(BOOLEAN 'True')|데이터베이스에 게시할 때 ANSI NULLS 설정에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.
|**/p:**|IgnoreAuthorizer=(BOOLEAN)|데이터베이스에 게시할 때 권한 부여자를 무시할지 또는 업데이트할지를 지정합니다.
|**/p:**|IgnoreColumnCollation=(BOOLEAN)|데이터베이스에 게시할 때 열 데이터 정렬의 차이를 무시할지 또는 업데이트할지를 지정합니다.
|**/p:**|IgnoreColumnOrder=(BOOLEAN)|데이터베이스에 게시할 때 테이블 열 순서의 차이를 무시해야 할지 아니면 업데이트해야 할지를 지정합니다.|
|**/p:**|IgnoreComments=(BOOLEAN)|데이터베이스에 게시할 때 주석의 차이를 무시할지 또는 업데이트할지를 지정합니다.
|**/p:**|IgnoreCryptographicProviderFilePath=(BOOLEAN 'True')|데이터베이스에 게시할 때 암호화 공급자에 대한 파일 경로의 차이를 무시할지 또는 업데이트할지를 지정합니다.
|**/p:**|IgnoreDdlTriggerOrder=(BOOLEAN)|데이터베이스 또는 서버에 게시할 때 DDL(Data Definition Language) 트리거 순서의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreDdlTriggerState=(BOOLEAN)|데이터베이스에 게시할 때 DDL(Data Definition Language) 트리거 사용/사용 안 함 상태의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreDefaultSchema=(BOOLEAN)|데이터베이스에 게시할 때 기본 스키마의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreDmlTriggerOrder=(BOOLEAN)|데이터베이스에 게시할 때 DML(Data Manipulation Language) 트리거 순서의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreDmlTriggerState=(BOOLEAN)|데이터베이스에 게시할 때 DML 트리거 사용/사용 안 함 상태의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreExtendedProperties=(BOOLEAN)|데이터베이스에 게시할 때 확장 속성의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreFileAndLogFilePath=(BOOLEAN 'True')|데이터베이스에 게시할 때 파일 및 로그 파일에 대한 경로의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreFilegroupPlacement=(BOOLEAN 'True')|데이터베이스에 게시할 때 FILEGROUP에서의 개체 배치에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreFileSize=(BOOLEAN 'True')|데이터베이스에 게시할 때 파일 크기의 차이를 무시할지 또는 경고를 발생하도록 할지를 지정합니다.|
|**/p:**|IgnoreFillFactor=(BOOLEAN 'True')|데이터베이스에 게시할 때 인덱스 스토리지의 채우기 비율에 대한 차이를 무시할지 또는 경고를 발생하도록 할지를 지정합니다.|
|**/p:**|IgnoreFullTextCatalogFilePath=(BOOLEAN 'True')|데이터베이스에 게시할 때 전체 텍스트의 파일 경로의 차이를 무시할지 또는 경고를 발생하도록 할지를 지정합니다.|
|**/p:**|IgnoreIdentitySeed=(BOOLEAN)|데이터베이스에 게시할 때 ID 열의 시드에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreIncrement=(BOOLEAN)|데이터베이스에 게시할 때 ID 열의 증가값에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreIndexOptions=(BOOLEAN)|데이터베이스에 게시할 때 인덱스 옵션의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreIndexPadding=(BOOLEAN 'True')|데이터베이스에 게시할 때 인덱스 패딩의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreKeywordCasing=(BOOLEAN 'True')|데이터베이스에 게시할 때 키워드의 대/소문자 구분에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreLockHintsOnIndexes=(BOOLEAN)|데이터베이스에 게시할 때 인덱스의 잠금 힌트의 차이를 무시 또는 업데이트할지 여부를 지정합니다.|
|**/p:**|IgnoreLoginSids=(BOOLEAN 'True')| 데이터베이스에 게시할 때 SID(보안 ID)의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreNotForReplication=(BOOLEAN)|데이터베이스에 게시할 때 복제용 아님 설정을 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreObjectPlacementOnPartitionScheme=(BOOLEAN 'True')|데이터베이스에 게시할 때 파티션 구성표에서 개체의 배치를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnorePartitionSchemes=(BOOLEAN)|데이터베이스에 게시할 때 분할 구성표와 함수의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnorePermissions=(BOOLEAN)|데이터베이스에 게시할 때 사용 권한의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreQuotedIdentifiers=(BOOLEAN 'True')|데이터베이스에 게시할 때 따옴표 붙은 식별자 설정의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreRoleMembership=(BOOLEAN)|데이터베이스에 게시할 때 로그인의 역할 멤버 자격 차이를 무시 또는 업데이트할지 여부를 지정합니다.|
|**/p:**|IgnoreRouteLifetime=(BOOLEAN 'True')|데이터베이스에 게시할 때 SQL Server가 라우팅 테이블에 경로를 유지하는 시간에 대한 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreSemicolonBetweenStatements=(BOOLEAN 'True')|데이터베이스에 게시할 때 T-SQL 문 사이의 세미콜론의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreTableOptions=(BOOLEAN)|데이터베이스에 게시할 때 테이블 옵션의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreTablePartitionOptions=(BOOLEAN)|데이터베이스에 게시할 때 테이블 파티션 옵션의 차이를 무시할지 또는 업데이트할지를 지정합니다.  이 옵션은 Azure Synapse Analytics 데이터 웨어하우스 데이터베이스에만 적용됩니다.|
|**/p:**|IgnoreUserSettingsObjects=(BOOLEAN)|데이터베이스에 게시할 때 사용자 설정 개체의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreWhitespace=(BOOLEAN 'True')|데이터베이스에 게시할 때 공백의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreWithNocheckOnCheckConstraints=(BOOLEAN)|데이터베이스에 게시할 때 CHECK 제약 조건의 WITH NOCHECK 절에 대한 값의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IgnoreWithNocheckOnForeignKeys=(BOOLEAN)|데이터베이스에 게시할 때 외래 키의 WITH NOCHECK 절에 대한 값의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|IncludeCompositeObjects=(BOOLEAN)|모든 복합 요소를 단일 게시 작업의 일부로 포함합니다.|
|**/p:**|IncludeTransactionalScripts=(BOOLEAN)|데이터베이스에 게시할 때 가능한 위치에 트랜잭션 문을 사용할지 여부를 지정합니다.|
|**/p:**|LongRunningCommandTimeout=(INT32)| SQL Server에 대한 쿼리를 실행할 때 장기 명령 시간 제한(초)을 지정합니다. 무기한 대기하려면 0을 사용합니다.|
|**/p:**|NoAlterStatementsToChangeClrTypes=(BOOLEAN)|차이가 있을 경우 ALTER ASSEMBLY 문을 실행하는 대신 게시에서 항상 어셈블리를 삭제하고 다시 만들지를 지정합니다.|
|**/p:**|PopulateFilesOnFileGroups=(BOOLEAN 'True')|대상 데이터베이스에 새 FileGroup이 만들어질 때 새 파일도 만들어지는지 여부를 지정합니다.|
|**/p:**|RegisterDataTierApplication=(BOOLEAN)|스키마가 데이터베이스 서버에 등록되었는지 여부를 지정합니다.|
|**/p:**|RunDeploymentPlanExecutors=(BOOLEAN)|다른 작업이 실행될때 DeploymentPlanExecutor 기여자를 실행할지 여부를 지정합니다.|
|**/p:**|ScriptDatabaseCollation=(BOOLEAN)|데이터베이스에 게시할 때 데이터베이스 데이터 정렬의 차이를 무시할지, 업데이트할지를 지정합니다.|
|**/p:**|ScriptDatabaseCompatibility=(BOOLEAN)|데이터베이스에 게시할 때 데이터베이스 호환성의 차이를 무시할지 또는 업데이트할지를 지정합니다.|
|**/p:**|ScriptDatabaseOptions=(BOOLEAN 'True')|게시 동작의 일부로 대상 데이터베이스 속성을 설정 또는 업데이트할지 여부를 지정합니다.|
|**/p:**|ScriptDeployStateChecks=(BOOLEAN)|데이터베이스 이름 및 서버 이름이 데이터베이스 프로젝트에 지정된 이름과 일치하는지 확인하는 문을 게시 스크립트에 생성할지 여부를 지정합니다.|
|**/p:**|ScriptFileSize=(BOOLEAN)|파일 그룹에 파일을 추가할 때 크기를 지정하는지 여부를 제어합니다.|
|**/p:**|ScriptNewConstraintValidation=(BOOLEAN 'True')|게시 마지막에 모든 제약 조건은 하나의 집합으로 확인되므로 게시 중간에 검사 또는 외래 키 제약 조건으로 인한 데이터 오류가 발생하지 않습니다. False로 설정하면 해당 데이터를 확인하지 않고 제약 조건이 게시됩니다.|
|**/p:**|ScriptRefreshModule=(BOOLEAN 'True')|게시 스크립트의 끝에 새로 고침 문을 포함합니다.|
|**/p:**|Storage=({File&#124;Memory})|데이터베이스 모델을 생성할 때 요소의 저장 방법을 지정합니다. 성능상의 이유로 기본값은 InMemory입니다. 큰 데이터베이스의 경우 파일 지원 스토리지가 필요합니다.|
|**/p:**|TreatVerificationErrorsAsWarnings=(BOOLEAN)|확인을 경고로 처리해야 하는 동안 발생한 오류를 게시하는지 여부를 지정합니다. 생성된 배포 계획을 대상 데이터베이스에 대해 실행하기 전에 해당 계획에 대한 확인이 수행됩니다. 계획 확인에서 대상 전용 개체(예: 인덱스)가 없는 등의 문제가 발견되면 해당 계획을 삭제하여 변경해야 합니다. 또한 복합 프로젝트에 대한 참조로 인한 종속성(예: 테이블, 뷰)이 존재하지만 대상 데이터베이스에는 존재하지 않는 상황도 확인됩니다. 첫 번째 오류에서 게시 동작을 중지하는 대신 모든 문제의 전체 목록을 가져오려면 이 작업을 수행하도록 선택할 수 있습니다.|
|**/p:**|UnmodifiableObjectWarnings=(BOOLEAN 'True')|개체에서 수정할 수 없는 차이가 발견될 경우(예: 파일 경로 또는 파일 크기가 특정 파일에서 다른 경우) 경고를 생성할지 여부를 지정합니다.|
|**/p:**|VerifyCollationCompatibility=(BOOLEAN 'True')|데이터 정렬 호환성이 확인되는지 여부를 지정합니다.
|**/p:**|VerifyDeployment=(BOOLEAN 'True')|성공적인 게시를 차단할 수 있는 문제가 존재할 경우 게시 작업을 중단하는 검사를 게시 전에 수행할지 여부를 지정합니다. 예를 들어 데이터베이스 프로젝트에 존재하지 않고 게시할 때 오류를 일으키는 외래 키를 대상 데이터베이스에 설정한 경우 게시 작업이 중단될 수 있습니다.|

## <a name="exit-codes"></a>종료 코드

다음 종료 코드를 반환하는 명령:

- 0 = 성공
- 0이 아닌 값 = 실패
