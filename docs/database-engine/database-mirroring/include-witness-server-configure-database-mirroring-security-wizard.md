---
title: 미러링 모니터 서버 포함(데이터베이스 미러링 보안 구성 마법사)
description: SSMS(SQL Server Management Studio) GUI 내에서 ‘데이터베이스 미러링 보안 구성’ 마법사의 ‘미러링 모니터 서버 포함’ 페이지에 대해 설명합니다.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.inclwitness.f1
ms.assetid: f04b38a4-f4e2-4d4c-bdac-7cc70e5a5684
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a8b787f59da14c1414e66f158f8001e05cca6006
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754644"
---
# <a name="include-witness-server-configure-database-mirroring-security-wizard"></a>미러링 모니터 서버 포함(데이터베이스 미러링 보안 구성 마법사)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 페이지를 사용하여 데이터베이스 미러링에 대한 보안 구성에 미러링 모니터 서버를 포함할지 여부를 지정할 수 있습니다.  
  
 **SQL Server Management Studio를 사용하여 데이터베이스 미러링을 구성하려면**  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [데이터베이스 미러링 보안 구성 마법사 시작&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>옵션  
 **예**  
 보안 구성에 미러링 모니터 서버 인스턴스를 포함하려면 클릭합니다. 주 서버 인스턴스에서 장애가 발생한 경우에 미러링 서버 인스턴스에 대한 자동 장애 조치(failover)가 있는 보호 우선 모드에서는 미러링 모니터 서버가 필요합니다.  
  
 **아니요**  
 미러링 모니터 서버를 포함하지 않고 보안을 구성하려면 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 속성&#40;미러링 페이지&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 미러링 모니터 서버](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
