---
description: 서버에 연결(Oracle), 로그인
title: 서버에 연결(Oracle), 로그인 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.oracleconnection.login.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 86ed91a1-a07c-46f2-a913-67317ef2255e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b585e2a17e577aab7ade2c5906bdcd184a12e8dd
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96121354"
---
# <a name="connect-to-server-oracle-login"></a>서버에 연결(Oracle), 로그인
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **서버에 연결** 대화 상자의 **로그인** 탭을 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자에서 Oracle 게시자로 연결을 설정하는 계정을 지정할 수 있습니다. 게시자를 구성하는 중에 복제 관리 사용자 스키마에 대해 지정한 계정과 동일한 계정을 사용해야 합니다. 자세한 내용은 [Oracle 게시자 구성](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)을 참조하세요.  
  
## <a name="options"></a>옵션  
 **서버 인스턴스**  
 배포자에 설치된 Oracle 클라이언트 소프트웨어를 구성하는 중에 지정한 Oracle 게시자의 TNS(Transparent Network Substrate) 이름입니다.  
  
 **인증**  
 **Oracle 표준 인증** (권장) 또는 **Windows 인증** 을 선택합니다. **Windows 인증** 을 선택하는 경우 다음 사항을 고려해야 합니다.  
  
-   Windows 자격 증명을 사용하는 연결을 허용하도록 Oracle 서버를 구성해야 합니다. 자세한 내용은 Oracle 설명서를 참조하십시오.  
  
-   현재 복제 관리 사용자 스키마에 대해 지정한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정으로 로그인되어 있어야 합니다.  
  
 **로그인** 및 **암호**  
 **인증** 옵션을 **Oracle 표준 인증** 으로 선택한 경우 사용할 로그인 및 암호를 지정합니다. 로그인 및 암호는 복제 관리 사용자 스키마에 대해 지정한 것과 동일해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시를 위한 용어 설명](../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)  
  
  
