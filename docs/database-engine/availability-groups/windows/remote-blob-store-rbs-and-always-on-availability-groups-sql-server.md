---
title: 가용성 그룹을 사용한 RBS(원격 Blob 저장소)
description: 'Always On 가용성 그룹의 일부인 데이터베이스와 함께 RBS(원격 Blob 저장소)를 사용하는 방법에 대한 설명입니다. '
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 01a70258-d4fd-40bc-bc44-c490b5d6c420
author: cawrites
ms.author: chadam
ms.openlocfilehash: e6fb7f1bdc9e01037129be72657cd5dcdeba4f56
ms.sourcegitcommit: 54cd97a33f417432aa26b948b3fc4b71a5e9162b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2020
ms.locfileid: "94584041"
---
# <a name="use-remote-blob-store-rbs-with-always-on-availability-groups"></a>Always On 가용성 그룹과 함께 RBS(원격 Blob 저장소) 사용
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][RBS(Remote Blob Store)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md) BLOB 개체에 대한 고가용성 재해 복구 솔루션을 제공할 수 있습니다. [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 은 가용성 데이터베이스에 저장된 RBS 메타데이터 및 스키마를 보조 복제본에 복제하여 보호합니다. 다음은 SharePoint 콘텐츠 데이터베이스입니다. 일반적으로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 은 BLOB에서 이 RBS 메타데이터를 독립적으로 저장합니다.  
  
 RBS BLOB 데이터 보호는 다음과 같이 BLOB 저장소 위치에 따라 다릅니다.  
  
|BLOB 저장소 위치|가용성 그룹이 이 BLOB 데이터를 보호할 수 있습니까?|  
|-------------------------|-----------------------------------------------------|  
|RBS 메타데이터를 포함하는 동일한 데이터베이스(RBS 원격 FILESTREAM 공급자를 사용하여 저장)|yes|  
|동일한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 있는 다른 데이터베이스(RBS 원격 FILESTREAM 공급자를 사용하여 저장)|yes<br /><br /> RBS 메타데이터를 포함하는 데이터베이스와 동일한 가용성 그룹에 이 데이터베이스를 두는 것이 좋습니다.|  
|다른 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 있는 다른 데이터베이스(RBS 원격 FILESTREAM 공급자를 사용하여 저장)|yes<br /><br /> 이 데이터베이스는 별도의 가용성 그룹에 있어야 합니다.|  
|타사 BLOB 저장소|예<br /><br /> 이 BLOB 데이터를 보호하려면 BLOB 저장소 공급자의 고가용성 메커니즘을 사용하십시오.|  
  
##  <a name="limitations"></a><a name="Limitations"></a> 제한 사항  
  
-   RBS 유지 관리자는 주 복제본에서 대상이 되어야 합니다.  
  
##  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   가용성 그룹 수신기를 사용합니다. 자세한 내용은 [가용성 그룹 수신기, 클라이언트 연결 및 애플리케이션 장애 조치(failover)&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)를 참조하세요.  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> 관련 내용  
  
-   [온라인 설명서의](https://msdn.microsoft.com/library/gg316773\(SQL.105\).aspx) Remote BLOB Store 유지 관리 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]  
  
-   [RBS 유지 관리자 실행](/archive/blogs/sqlrbs/running-rbs-maintainer) (블로그)  
  
-   [FILESTREAM 공급자를 사용하여 RBS(Remote BLOB Storage) 구성(SharePoint 2010)](/archive/blogs/mvpawardprogram/configure-remote-blob-storage-rbs-with-the-filestream-provider-sharepoint-2010) (블로그)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 클라이언트 연결&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)   
 [RBS&#40;Remote Blob Store&#41;&#40;SQL Server&#41;](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
