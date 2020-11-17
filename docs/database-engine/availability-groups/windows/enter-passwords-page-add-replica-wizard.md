---
title: '복제본 추가 마법사: 가용성 그룹에 대한 암호 입력 페이지'
description: SQL Server Management Studio에 '복제본 추가' 마법사의 '암호 입력 페이지'에 있는 속성에 대한 설명입니다.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: end-user-help
f1_keywords:
- sql13.swb.addreplicawizard.enterpasswords.f1
ms.assetid: e69207a0-c5c4-44e4-ae9a-4afbb67251d1
author: cawrites
ms.author: chadam
ms.openlocfilehash: 4ab6d424bfa1ff70ada91956e4552032843ff28b
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584277"
---
# <a name="enter-passwords-page-add-replica-wizard-for-always-on-availability-groups"></a>Always On 가용성 그룹에 대한 암호 입력 페이지(복제본 추가 마법사)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  이 도움말 항목에서는 **암호 입력** 페이지의 옵션에 대해 설명합니다. 이 항목은 [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] 의 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에 적용됩니다.  
  
 **복제본 선택** 페이지에서 선택한 복제본에 데이터베이스 마스터 키가 있는 데이터베이스가 포함되어 있으면 암호 입력 페이지가 나타납니다.  
  
## <a name="enter-passwords-options"></a>암호 입력 옵션  
 **이 SQL Server 인스턴스의 사용자 데이터베이스 선택** 표에는 모든 로컬 사용자 데이터베이스가 나열됩니다. 열은 다음과 같습니다.  
  
 **이름**  
 로컬 사용자 데이터베이스의 이름을 표시합니다.  
  
 **크기**  
 마법사에서 사용할 수 있는 데이터베이스 크기를 표시합니다.  
  
 **상태**  
 데이터베이스 마스터 키가 있는 데이터베이스에 대한 **암호 필요** 상태를 나타냅니다. **암호** 열에서 데이터베이스 마스터 키의 암호를 입력한 후 **새로 고침** 을 클릭합니다. 암호를 올바르게 입력하면 **상태** 열에 **암호 입력됨** 이 표시됩니다.  
  
 데이터베이스에 데이터베이스 마스터 키가 없는 경우 **상태** 열에는 **암호가 필요하지 않음** 이 표시됩니다.  
  
 **암호**  
 **상태** 열에 **암호 필요** 가 표시되면 데이터베이스 마스터 키의 암호를 입력합니다.  
  
 **새로 고침**  
 표를 새로 고치려면 클릭합니다. 필요한 암호를 입력한 후에 이 기능을 사용하면 유용합니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
-   [가용성 그룹에 복제본 추가 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
