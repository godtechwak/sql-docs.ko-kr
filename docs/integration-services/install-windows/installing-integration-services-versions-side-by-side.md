---
description: 여러 Integration Services 버전을 병렬로 설치
title: 여러 Integration Services 버전을 병렬로 설치 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d57148134c727b03a30d75af415d1e2476dca32d
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88345999"
---
# <a name="installing-integration-services-versions-side-by-side"></a>여러 Integration Services 버전을 병렬로 설치

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  SSIS의 이전 버전과   
      [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services(SSIS)를 병렬로 설치할 수 있습니다. 이 항목에서는 병렬 설치의 몇 가지 제한에 대해 설명합니다.  
  
## <a name="designing-and-maintaining-packages"></a>패키지 디자인 및 유지 관리  
 SQL Server 2016, SQL Server 2014 또는 SQL Server 2012를 대상으로 하는 패키지를 디자인하고 유지 관리하려면 Visual Studio 2015dyd SSDT(SQL Server Data Tools)를 사용합니다. SSDT를 다운로드하려면 [최신 SQL Server Data Tools 다운로드](../../ssdt/download-sql-server-data-tools-ssdt.md)를 참조하세요.  
  
 Integration Services 프로젝트의 속성 페이지에 있는 **구성 속성** 의 **일반** 탭에서 **TargetServerVersion** 속성을 선택하고 SQL Server 2016, SQL Server 2014 또는 SQL Server 2012를 선택합니다.  
  
|SQL Server의 대상 버전|SSIS 패키지용 개발 환경|  
|----------------------------------|-----------------------------------------------|  
|2016|Visual Studio 2015용 SQL Server Data Tools|  
|2014|Visual Studio 2015용 SQL Server Data Tools<br /><br /> 또는<br /><br /> SQL Server Data Tools - Visual Studio 2013용 Business Intelligence|  
|2012|Visual Studio 2015용 SQL Server Data Tools<br /><br /> 또는<br /><br /> SQL Server Data Tools - Visual Studio 2012용 Business Intelligence|  
|2008|SQL Server 2008의 Business Intelligence Development Studio|  
  
 기존 프로젝트에 추가하는 기존 패키지는 프로젝트의 대상 형식으로 변환됩니다.  
  
## <a name="running-packages"></a>패키지 실행  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 버전의 **dtexec** 유틸리티 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 이전 버전의 개발 도구에서 만든 Integration Services 패키지를 실행할 수 있습니다. 이러한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 도구는 이전 버전의 개발 도구에서 개발한 패키지를 로드할 때 일시적으로 메모리 내의 패키지를 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] 에서 사용하는 패키지 형식으로 변환합니다. 패키지에 문제가 있어 정상적으로 변환할 수 없는 경우 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 도구는 해당 문제를 해결할 때까지 패키지를 실행할 수 없습니다. 자세한 내용은 [Integration Services 패키지 업그레이드](../../integration-services/install-windows/upgrade-integration-services-packages.md)를 참조하세요.  
  
  
