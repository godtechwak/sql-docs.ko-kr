---
title: 미러된 데이터베이스 등록 | Microsoft Docs
description: 데이터베이스 관련 정보를 캐시하는 데이터베이스 미러링 모니터에 미러된 데이터베이스를 추가하여 서버 인스턴스에 미러된 데이터베이스를 등록하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dbmmonitor.registermirroreddb.f1
ms.assetid: 6acd02b9-2311-49b0-a5f8-3852beecb4b0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 23bc66a0c782005a2426ee9fc4e35a237f49cb96
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126153"
---
# <a name="register-mirrored-database"></a>미러된 데이터베이스 등록
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 대화 상자를 사용하면 데이터베이스 미러링 모니터에 데이터베이스를 추가하여 지정된 서버 인스턴스에서 하나 이상의 미러된 데이터베이스를 등록할 수 있습니다. 데이터베이스가 추가되면 데이터베이스 미러링 모니터는 데이터베이스, 해당 파트너, 파트너에 연결되는 방법 등에 대한 정보를 로컬로 캐시합니다.  
  
> [!IMPORTANT]  
>  주 서버 인스턴스에서 **sysadmin** 고정 서버 역할의 멤버이지만 미러 서버 인스턴스에서는 이 역할의 멤버가 아닌 경우 주 서버 인스턴스에 대한 상태만 볼 수 있습니다.  
  
 **SQL Server Management Studio를 사용하여 데이터베이스 미러링을 모니터링하려면**  
  
-   [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="options"></a>옵션  
 **서버 인스턴스**  
 데이터베이스 미러링 모니터에 이미 저장된 연결이 있는 서버 인스턴스가 포함된 목록에서 서버 인스턴스를 선택하거나 **연결** 을 클릭합니다. 나열된 서버 인스턴스에 대해 새 자격 증명을 지정하려면 **연결** 을 클릭하고 새 자격 증명을 사용하여 연결합니다.  
  
> [!NOTE]  
>  여러 서버 인스턴스에서 데이터베이스를 등록하려면 한 서버 인스턴스에 대해 원하는 데이터베이스의 검사를 완료한 후에 **적용** 을 클릭하고 다른 서버 인스턴스를 선택합니다.  
  
 **연결**  
 서버 인스턴스에 대한 새 자격 증명을 지정하려면 **연결** 을 클릭하고 새 자격 증명을 사용하여 연결합니다. 서버 인스턴스에 연결되어 있는 동안 데이터베이스 미러링 모니터는 **데이터를 기다리는 중** 을 표시합니다.  
  
 **미러된 데이터베이스**  
 **미러된 데이터베이스** 표에는 서버 인스턴스의 미러된 데이터베이스가 나열됩니다.  
  
 표에는 다음 열이 있습니다.  
  
|열 이름|Description|  
|-----------------|-----------------|  
|**등록**|등록할 각 데이터베이스를 검사합니다. 데이터베이스가 현재 모니터링되고 있는 경우 해당 확인란은 선택된 상태로 비활성화되어 있습니다.<br /><br /> 참고: 데이터베이스 등록을 취소하려면 **미러된 데이터베이스 등록** 대화 상자를 닫고 탐색 트리에서 데이터베이스를 선택하고 **동작** 메뉴에서 **등록 취소** 를 선택합니다.|  
|**Database**|선택한 서버 인스턴스에 있는 미러된 데이터베이스의 이름입니다.|  
|**현재 역할**|선택한 서버 인스턴스에 있는 데이터베이스의 현재 미러링 역할(주 서버 또는 미러 서버)입니다.|  
|**파트너(연결 대상)**|데이터베이스에 대한 장애 조치(Failover) 파트너의 이름입니다. **콘솔 사용자의 Windows 인증** 또는 ‘ _\<login name>_ ’ **로그인의 SQL Server 인증** 이 괄호 안에 표시됩니다. 이것은 인스턴스가 이전에 추가된 경우에는 현재 사용되는 인증 정보이고 인스턴스가 모니터에 추가되지 않은 경우에는 사용될 인증 정보입니다.|  
  
 **[확인]을 클릭할 때 [서버 연결 관리] 대화 상자 표시**  
 기본적으로 데이터베이스 미러링 모니터는 이전에 자격 증명이 제공되지 않은 파트너 서버 인스턴스에 대해 Windows 인증 자격 증명을 사용합니다. 데이터베이스 등록을 완료할 때 하나 이상의 서버 인스턴스에 대한 자격 증명을 변경하려면 이 옵션을 설정합니다.  
  
 이 옵션을 설정할 경우 **확인** 을 클릭하면 **서버 연결 관리** 대화 상자가 열립니다. 이 대화 상자에서 지정된 장애 조치 파트너에 연결할 때 사용할 모니터에 대한 자격 증명을 지정할 서버 인스턴스를 선택할 수 있습니다.  
  
 파트너에 대한 자격 증명을 편집하려면 **서버 인스턴스** 표에서 항목을 찾은 다음 해당 행에서 **편집** 을 클릭합니다. 이렇게 하면 자격 증명 컨트롤이 현재 캐시된 값으로 초기화된 상태에서 해당 서버 인스턴스 이름의 **서버에 연결** 대화 상자가 열립니다. 필요에 따라 자격 증명을 변경하고 **연결** 을 클릭합니다. 자격 증명에 충분한 권한이 있는 경우 **연결 방법** 열이 새 자격 증명으로 업데이트됩니다.  
  
 **적용**  
 대화 상자를 열어 둔 상태에서 선택한 데이터베이스를 등록하고 파트너 서버 인스턴스의 자격 증명을 저장하려면 이 단추를 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링 모니터 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [데이터베이스 미러링 보안 구성 마법사 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
  
