---
title: Kerberos 연결의 서비스 사용자 이름 등록
description: SPN(서비스 사용자 이름)을 Active Directory에 등록하는 방법을 알아봅니다. 이 등록은 SQL Server에서 Kerberos 인증을 사용하는 데 필요합니다.
ms.prod: sql
ms.prod_service: high-availability
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], SPNs
- network connections [SQL Server], SPNs
- registering SPNs
- Server Principal Names
- SPNs [SQL Server]
ms.assetid: e38d5ce4-e538-4ab9-be67-7046e0d9504e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 08/12/2020
ms.openlocfilehash: 27e19a66912c220e8c407c4182c3241906af5ea5
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670336"
---
# <a name="register-a-service-principal-name-for-kerberos-connections"></a>Kerberos 연결의 서비스 사용자 이름 등록

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

 SQL Server에서 Kerberos 인증을 사용하려면 다음 조건 둘 다에 해당되어야 합니다.  

- 클라이언트 및 서버 컴퓨터는 동일한 Windows 도메인이나 트러스트된 도메인의 일부여야 합니다.  

- SPN(서비스 사용자 이름)은 Windows 도메인에서 키 배포 센터 역할을 가정하는 Active Directory에 등록해야 합니다. SPN은 등록된 후에 SQL Server 인스턴스 서비스를 시작한 Windows 계정에 매핑됩니다. SPN 등록이 수행되지 않았거나 실패하면 Windows 보안 계층이 SPN과 연결된 계정을 확인할 수 없으며 Kerberos 인증이 사용되지 않습니다.

    > [!NOTE]  
    >  서버가 SPN을 자동으로 등록할 수 없으면 수동으로 SPN을 등록해야 합니다. [수동 SPN 등록](#Manual)을 참조하십시오.  

sys.dm_exec_connections 동적 관리 뷰를 쿼리하여 연결에 Kerberos가 사용되는지 확인할 수 있습니다. 다음 쿼리를 실행하고, Kerberos를 사용할 수 있을 경우 "KERBEROS"가 되는 auth_scheme 열의 값을 확인하십시오.

```sql
SELECT auth_scheme FROM sys.dm_exec_connections WHERE session_id = @@spid ;
```

> [!TIP]
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server용 Kerberos 구성 관리자** 는 SQL Server에서 Kerberos 관련 연결 문제를 해결하는 데 도움이 되는 진단 도구입니다. 자세한 내용은 [SQL Server용 Microsoft Kerberos 구성 관리자](https://www.microsoft.com/download/details.aspx?id=39046)를 참조하십시오.  

##  <a name="the-role-of-the-spn-in-authentication"></a><a name="Role"></a> 인증에서 SPN의 역할  

애플리케이션에서 연결을 열고 Windows 인증을 사용하는 경우 SQL Server Native Client는 SQL Server 컴퓨터 이름과 인스턴스 이름 그리고 선택적으로 SPN을 전달합니다. 연결에서 SPN을 전달하면 SPN은 변경 없이 사용됩니다.  

연결에서 SPN을 전달하지 않으면 사용된 프로토콜, 서버 이름 및 인스턴스 이름을 기반으로 기본 SPN이 생성됩니다.  

위의 두 시나리오에서 SPN은 키 배포 센터에 전달되어 연결 인증을 위한 보안 토큰을 가져옵니다. 보안 토큰을 가져올 수 없으면 인증에서 NTLM을 사용합니다.  

SPN(서비스 사용자 이름)은 클라이언트가 서비스 인스턴스를 고유하게 식별하는 이름입니다. Kerberos 인증 서비스에서는 서비스를 인증하는 데 SPN을 사용합니다. 클라이언트는 서비스에 연결할 때 서비스의 인스턴스를 찾고 해당 인스턴스에 대한 SPN을 작성한 다음 서비스에 연결하고 인증을 위해 서비스에 대한 SPN을 제공합니다.  
  
> [!NOTE]  
>  이 항목에 제공되어 있는 정보는 클러스터링을 사용하는 SQL Server 구성에도 적용됩니다.  
  
Windows 인증은 사용자를 SQL Server에 인증하는 데 사용하는 기본 인증 방법입니다. Windows 인증을 사용하는 클라이언트는 NTLM이나 Kerberos를 사용하여 인증됩니다. Active Directory 환경에서는 항상 Kerberos 인증이 먼저 시도됩니다. 명명된 파이프를 사용하는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 클라이언트에는 Kerberos 인증을 사용할 수 없습니다.  

##  <a name="permissions"></a><a name="Permissions"></a> 권한

데이터베이스 엔진 서비스를 시작하면 서비스가 SPN(서비스 사용자 이름)을 등록하려고 합니다. SQL Server를 시작하는 계정에 Active Directory Domain Services에서 SPN을 등록할 권한이 없을 수 있습니다. 그러면 이 호출이 실패하고 애플리케이션 이벤트 로그 및 SQL Server 오류 로그에 경고 메시지가 로그됩니다. SPN을 등록하려면 데이터베이스 엔진이 로컬 시스템(권장되지 않음)이나 NETWORK SERVICE 같은 기본 제공 계정 또는 SPN을 등록할 권한이 있는 계정으로 실행되고 있어야 합니다. 도메인 관리자 계정을 사용하여 SPN을 등록할 수 있지만 프로덕션 환경에서는 사용하지 않는 것이 좋습니다. SQL Server가 Windows 7 또는 Windows Server 2008 R2 운영 체제에서 실행되는 경우 가상 계정이나 MSA(관리형 서비스 계정)를 사용하여 SQL Server를 실행할 수 있습니다. 가상 계정 및 MSA 모두 SPN을 등록할 수 있습니다. SQL Server가 이러한 계정 중 하나로 실행되고 있지 않으면 시작할 때 SPN이 등록되지 않으므로 도메인 관리자가 SPN을 수동으로 등록해야 합니다.

> [!NOTE]  
>  Windows 도메인이 Windows Server 2008 R2 기능 수준 이하에서 실행되도록 구성된 경우 관리형 서비스 계정에는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 서비스의 SPN을 등록하는 데 필요한 권한이 없습니다. Kerberos 인증이 필요한 경우 도메인 관리자가 관리형 서비스 계정으로 SQL Server SPN을 수동으로 등록해야 합니다.

추가 정보는 [SQL Server 2008에서 Kerberos 제한된 위임을 구현하는 방법(How to Implement Kerberos Constrained Delegation with SQL Server 2008)](/previous-versions/sql/sql-server-2008/ee191523(v=sql.100))에서 이용할 수 있습니다.  

##  <a name="spn-formats"></a><a name="Formats"></a> SPN 형식

[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]부터 SPN 형식이 TCP/IP, 명명된 파이프 및 공유 메모리에서 Kerberos 인증을 지원하도록 변경됩니다. 명명된 인스턴스 및 기본 인스턴스에 대해 지원되는 SPN 형식은 다음과 같습니다.  
  
**명명된 인스턴스**  
  
-   **MSSQLSvc/\<FQDN>:[\<port> | \<instancename>]** . 여기서  
  
    -   **MSSQLSvc** 는 등록할 서비스입니다.  
  
    -   **\<FQDN>** 은 서버의 정규화된 도메인 이름입니다.  
  
    -   **\<port>** 는 TCP 포트 번호입니다.  
  
    -   **\<instancename>** 은 SQL Server 인스턴스의 이름입니다.  
  
**기본 인스턴스**  
  
-   **MSSQLSvc/\<FQDN>:\<port>**  | **MSSQLSvc/\<FQDN>** . 여기서  
  
    -   **MSSQLSvc** 는 등록할 서비스입니다.  
  
    -   **\<FQDN>** 은 서버의 정규화된 도메인 이름입니다.  
  
    -   **\<port>** 는 TCP 포트 번호입니다.  
  
    > [!NOTE]
    > 새로운 SPN 형식에는 포트 번호가 필요하지 않습니다. 따라서 포트 번호를 사용하지 않는 다중 포트 서버 또는 프로토콜에서 Kerberos 인증을 사용할 수 있습니다.  
   
|SPN 형식|Description|  
|-|-|  
|MSSQLSvc/\<FQDN>:\<port>|TCP가 사용될 때 공급자가 생성하는 기본 SPN입니다. \<port>는 TCP 포트 번호입니다.|  
|MSSQLSvc/\<FQDN>|TCP 이외의 프로토콜이 사용될 때 기본 인스턴스에 대해 공급자가 생성하는 기본 SPN입니다. \<FQDN>은 정규화된 도메인 이름입니다.|  
|MSSQLSvc/\<FQDN>:\<instancename>|TCP 이외의 프로토콜이 사용될 때 명명된 인스턴스에 대해 공급자가 생성하는 기본 SPN입니다. \<instancename>은 SQL Server 인스턴스의 이름입니다.|  

> [!NOTE]  
> SPN에 TCP 포트가 포함되어 있는 TCP/IP 연결의 경우 사용자가 Kerberos 인증을 사용하여 연결할 TCP 프로토콜을 SQL Server에서 사용하도록 설정해야 합니다. 

##  <a name="automatic-spn-registration"></a><a name="Auto"></a> SPN 자동 등록  

[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스가 시작되면 SQL Server에서 SQL Server 서비스 SPN을 등록하려고 합니다. 인스턴스가 중지되면 SQL Server에서 SPN 등록을 취소하려고 합니다. TCP/IP 연결의 경우 SPN은 *MSSQLSvc/\<FQDN>* : *\<tcpport>* 형식으로 등록됩니다. 명명된 인스턴스와 기본 인스턴스는 둘 다 *MSSQLSvc* 로 등록됩니다. 인스턴스는 *\<tcpport>* 값에 따라 차별화됩니다.  
  
Kerberos를 지원하는 다른 연결에서 SPN은 명명된 인스턴스의 경우 *MSSQLSvc/\<FQDN>* / *\<instancename>* 형식으로 등록됩니다. 기본 인스턴스는 *MSSQLSvc/\<FQDN>* 형식으로 등록됩니다.  

서비스 계정에 이러한 동작을 수행하는 데 필요한 권한이 없는 경우에는 수동으로 SPN을 등록하거나 등록 취소해야 합니다.  

##  <a name="manual-spn-registration"></a><a name="Manual"></a> 수동 SPN 등록  

SPN을 수동으로 등록하려면 관리자가 Microsoft [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 지원 도구와 함께 제공되는 Setspn.exe 도구를 사용해야 합니다. 자세한 내용은 [Windows Server 2003 서비스 팩 1 지원 도구](https://support.microsoft.com/kb/892777) 기술 자료 문서를 참조하십시오.  

Setspn.exe는 SPN(서비스 사용자 이름) 디렉터리 속성을 읽고 수정하고 삭제하는 데 사용할 수 있는 명령줄 도구입니다. 또한 이 도구를 통해 현재 SPN을 보고 계정의 기본 SPN을 다시 설정하고 보조 SPN을 추가 또는 삭제할 수도 있습니다.  

다음 예에서는 도메인 사용자 계정으로 TCP/IP 연결용 SPN을 수동으로 등록하는 데 사용되는 구문을 보여 줍니다.  

```
setspn -A MSSQLSvc/myhost.redmond.microsoft.com:1433 redmond\accountname  
```

> [!NOTE]
> SPN이 이미 있는 경우에는 해당 SPN을 삭제한 후 다시 등록해야 합니다. 이 작업을 수행하려면 `setspn` 명령을 `-D` 스위치와 함께 사용합니다. 다음 예에서는 새로운 인스턴스 기반 SPN을 수동으로 등록하는 방법을 보여 줍니다. 도메인 사용자 계정을 사용하는 기본 인스턴스의 경우 다음을 사용합니다.  

```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com redmond\accountname  
```  
  
명명된 인스턴스의 경우에는 다음을 사용합니다.  
  
```  
setspn -A MSSQLSvc/myhost.redmond.microsoft.com:instancename redmond\accountname  
```  
  
##  <a name="client-connections"></a><a name="Client"></a> 클라이언트 연결  

사용자 지정 SPN은 클라이언트 드라이버에서 지원됩니다. 하지만 SPN이 제공되지 않으면 클라이언트 연결 형식을 기반으로 SPN이 자동 생성됩니다. TCP 연결의 경우 명명된 인스턴스와 기본 인스턴스 모두에 대해 *MSSQLSvc*/*FQDN*:[*port*] 형식의 SPN이 사용됩니다.  
  
명명된 파이프와 공유 메모리 연결에서 명명된 인스턴스에는 *MSSQLSvc/\<FQDN>:\<instancename>* 형식의 SPN이 사용되고 기본 인스턴스에는 *MSSQLSvc/\<FQDN>* 형식의 SPN이 사용됩니다.  
  
**서비스 계정을 SPN으로 사용**  
  
서비스 계정을 SPN으로 사용할 수 있습니다. 서비스 계정은 Kerberos 인증에 대한 연결 특성을 통해 지정되며 다음 형식을 사용합니다.  
  
- **username\@domain** 또는 **domain\username**(도메인 사용자 계정의 경우)  

- **machine$\@domain** 또는 **host\FQDN**(로컬 시스템 또는 NETWORK SERVICE와 같은 컴퓨터 도메인 계정의 경우)  

연결 인증 방법을 확인하려면 다음 쿼리를 실행합니다.  
  
```sql  
SELECT net_transport, auth_scheme   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
``` 

##  <a name="authentication-defaults"></a><a name="Defaults"></a> 인증 기본값  

다음 표에서는 SPN 등록 시나리오에 따라 다르게 사용되는 인증 기본값에 대해 설명합니다.  
  
|시나리오|인증 방법|  
|--------------|---------------------------|  
|SPN이 올바른 도메인 계정, 가상 계정, MSA 또는 기본 제공 계정에 매핑됩니다. 예를 들어 로컬 시스템 또는 NETWORK SERVICE에 매핑됩니다.|로컬 연결은 NTLM을 사용하고, 원격 연결은 Kerberos를 사용합니다.|  
|SPN이 올바른 도메인 계정, 가상 계정, MSA 또는 기본 제공 계정입니다.|로컬 연결은 NTLM을 사용하고, 원격 연결은 Kerberos를 사용합니다.|  
|SPN이 잘못된 도메인 계정, 가상 계정, MSA 또는 기본 제공 계정에 매핑됩니다.|인증에 실패하게 됩니다.|  
|SPN 조회에 실패하거나 SPN이 올바른 도메인 계정, 가상 계정, MSA 또는 기본 제공 계정에 매핑되지 않거나 SPN이 올바른 도메인 계정, 가상 계정, MSA 또는 기본 제공 계정이 아닙니다.|로컬 및 원격 연결이 NTLM을 사용합니다.|  

> [!NOTE]
> 여기서 '올바르다'는 것은 등록된 SPN에 의해 매핑되는 계정이 SQL Server 서비스를 실행하고 있는 계정과 일치함을 의미합니다.  

##  <a name="comments"></a><a name="Comments"></a> 설명  

DAC(관리자 전용 연결)는 인스턴스 이름 기반 SPN을 사용합니다. 해당 SPN이 성공적으로 등록되었으면 DAC에 Kerberos 인증을 사용할 수 있습니다. 또는 사용자가 계정 이름을 SPN으로 지정할 수 있습니다.

시작 시 SPN 등록에 실패하면 해당 내용이 SQL Server 오류 로그에 기록되고 시작이 계속됩니다.  

종료 시 SPN 등록 취소에 실패하면 해당 내용이 SQL Server 오류 로그에 기록되고 종료가 계속됩니다.  

## <a name="see-also"></a>관련 항목  
- [클라이언트 연결의 서비스 사용자 이름&#40;SPN&#41; 지원](../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)
- [클라이언트 연결의 SPN&#40;서비스 사용자 이름&#41;&#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)
- [클라이언트 연결의 SPN&#40;서비스 사용자 이름&#41;&#40;ODBC&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)
- [SQL Server Native Client 기능](../../relational-databases/native-client/features/sql-server-native-client-features.md)
- [Reporting Services 환경의 Kerberos 인증 문제 관리(영문)](/previous-versions/sql/sql-server-2008/ff679930(v=sql.100))