---
description: 병합 에이전트 보안
title: 병합 에이전트 보안 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.MA.f1
helpviewer_keywords:
- Merge Agent Security dialog box
ms.assetid: 9b86171a-4381-4b39-869a-cdc161e7cd15
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6d571e5b41937947e0c6d03e5d1a84fe0dc88e8b
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88465275"
---
# <a name="merge-agent-security"></a>병합 에이전트 보안
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **병합 에이전트 보안** 대화 상자를 사용하여 병합 에이전트를 실행하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정을 지정할 수 있습니다. 병합 에이전트는 밀어넣기 구독의 경우에는 배포자에서, 끌어오기 구독의 경우에는 구독자에서 실행됩니다. Windows 계정으로 에이전트 프로세스가 실행되기 때문에 이 계정을 *프로세스 계정* 이라고도 합니다. 이 대화 상자에서 사용 가능한 추가 옵션은 대화 상자에 액세스하는 방법에 따라 달라집니다.  
  
-   새 구독 마법사에서 이 대화 상자에 액세스하는 경우에는 구독자(밀어넣기 구독의 경우) 또는 게시자 및 배포자(끌어오기 구독의 경우)에 병합 에이전트를 연결하는 컨텍스트도 지정할 수 있습니다. Windows 계정을 사용하거나 지정한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정의 컨텍스트에서 연결을 설정할 수 있습니다.  
  
-   **구독 속성** 대화 상자에서 이 대화 상자에 액세스하는 경우에는 해당 대화 상자의 **구독자 연결** 또는 **게시자 연결** 행의 속성 단추 ( **...** )를 클릭하여 병합 에이전트를 연결하는 컨텍스트를 지정합니다. **구독 속성** 대화 상자에 액세스하는 방법은 [밀어넣기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) 및 방법: [끌어오기 구독 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)을 참조하세요.  
  
 모든 계정이 유효해야 하며 각 계정에 대해 올바른 암호를 지정해야 합니다. 계정 및 암호의 유효성은 에이전트를 실행할 때 검사합니다.  
  
## <a name="options"></a>옵션  
 **Process Account**  
 병합 에이전트를 실행하는 Windows 계정을 입력합니다.  
  
-   밀어넣기 구독의 경우 계정이 다음 조건을 만족해야 합니다.  
  
    -   적어도 배포 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
    -   PAL의 멤버여야 합니다.  
  
    -   게시 데이터베이스의 사용자와 연결된 로그인이어야 합니다.  
  
    -   스냅샷 공유에 대해 읽기 권한이 있어야 합니다.  
  
-   끌어오기 구독의 경우 계정이 적어도 구독 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
 연결을 설정할 때 프로세스 계정을 가장하면 추가 사용 권한이 필요합니다. 아래의 **게시자 및 배포자에 연결** 섹션과 **구독자에 연결** 섹션을 참조하십시오.  
  
 병합 에이전트가 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 인스턴스에서 실행되지 않기 때문에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]에 대한 끌어오기 구독에 **프로세스 계정** 을 지정할 수 없습니다.  
  
 **암호** 및 **암호 확인**  
 Windows 계정의 암호를 입력합니다.  
  
 **게시자 및 배포자에 연결**  
 밀어넣기 구독의 경우 항상 **프로세스 계정** 입력란에 지정한 계정을 가장하여 게시자 및 배포자에 연결합니다.  
  
 끌어오기 구독의 경우 병합 에이전트를 게시자 및 배포자에 연결할 때 **프로세스 계정** 입력란에 지정한 계정을 가장할지, 아니면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용할 것인지를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용하도록 선택한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인과 암호를 입력합니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용하는 대신 Windows 계정을 가장하도록 선택할 것을 권장합니다.  
  
 연결에 사용할 Windows 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정은 다음 조건을 만족해야 합니다.  
  
-   PAL의 멤버여야 합니다.  
  
-   게시 데이터베이스의 사용자와 연결된 로그인이어야 합니다.  
  
-   배포 데이터베이스의 사용자와 연결된 로그인이어야 합니다. 사용자는 게스트 사용자일 수 있습니다.  
  
-   스냅샷 공유에 대해 읽기 권한이 있어야 합니다.  
  
 **구독자에 연결**  
 끌어오기 구독의 경우 항상 **프로세스 계정** 입력란에 지정한 계정을 가장하여 구독자에 연결합니다.  
  
 밀어넣기 구독의 경우 병합 에이전트를 게시자 및 배포자에 연결할 때 **프로세스 계정** 입력란에 지정한 계정을 가장할지, 아니면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용할 것인지를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용하도록 선택한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인과 암호를 입력합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정을 사용하는 것보다 Windows 계정을 가장하도록 선택하는 것이 좋습니다.  
  
 구독자 연결에 사용되는 Windows 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 계정은 적어도 구독 데이터베이스에 포함된 **db_owner** 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제의 로그인 및 암호 관리](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [복제 에이전트 보안 모델](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [복제 에이전트 개요](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [게시 구독](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
