---
title: 데이터베이스 선택 페이지(새 가용성 그룹 및 데이터베이스 추가 마법사)
description: SQL Server Management Studio GUI에 있는 새 가용성 그룹 및 데이터베이스 추가 마법사 모두의 “데이터베이스 선택” 페이지에 대해 설명합니다.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.adddatabasewizard.selectdatabases.f1
- sql13.swb.newagwizard.selectdatabases.f1
ms.assetid: 929c5e15-d087-438d-b1f2-aa97c5f8bff8
author: cawrites
ms.author: chadam
ms.openlocfilehash: 1576b98f62832f5c45759afe96fd0254d3d83513
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94583921"
---
# <a name="select-databases-page-new-availability-group-wizard-and-add-database-wizard"></a>Select Databases Page (New Availability Group Wizard and Add Database Wizard)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  이 도움말 항목에서는 **데이터베이스 지정** 페이지의 옵션에 대해 설명합니다. 이 항목은 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 의 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] 및 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에 적용됩니다.  
  
##  <a name="select-databases-options"></a><a name="PageOptions"></a> 데이터베이스 선택 옵션  
 **이 SQL Server 인스턴스의 사용자 데이터베이스 선택** 표에는 모든 로컬 사용자 데이터베이스가 나열됩니다. 열은 다음과 같습니다.  
  
 **이름**  
 로컬 사용자 데이터베이스의 이름을 표시합니다.  

 **크기**  
 마법사에서 사용할 수 있는 데이터베이스 크기를 표시합니다.  
  
 **상태**  
 지정된 데이터베이스가 가용성 그룹에 추가하기 위한 사전 요구 사항을 충족하는지 여부를 나타내는 텍스트가 있는 하이퍼링크를 표시합니다. 상태가 "**사전 요구 사항 일치**"인 경우 데이터베이스를 가용성 그룹에 추가할 수 있습니다. 데이터베이스가 모든 사전 요구 사항을 충족하지 않는 경우 **상태** 하이퍼링크에 데이터베이스를 사용할 수 없는 이유에 대한 간략한 설명이 제공됩니다. 자세한 내용을 보려면 하이퍼링크를 클릭하세요.  
  
 사전 요구 사항을 충족하기 위해 데이터베이스에서 작업을 수행하는 동안 **데이터베이스 선택** 페이지에서 마법사를 종료할 수 있습니다. **데이터베이스 선택** 페이지로 돌아가서 **새로 고침** 을 클릭하여 표를 업데이트합니다.  
  
 **암호**  
 데이터베이스에 데이터베이스 마스터 키가 들어 있는 경우 데이터베이스 마스터 키에 대한 암호를 입력합니다.  
  
 **새로 고침**  
 표를 새로 고치려면 클릭합니다. 이 기능은 사전 요구 사항을 충족하기 위해 데이터베이스에서 작업을 수행한 이후에 유용합니다.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [새 가용성 그룹 대화 상자 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [가용성 그룹에 데이터베이스 추가 마법사 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Always On 가용성 그룹에 대한 필수 조건, 제한 사항 및 권장 사항&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
