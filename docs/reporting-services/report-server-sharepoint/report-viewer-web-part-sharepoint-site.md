---
title: SharePoint 사이트의 보고서 뷰어 웹 파트 - SSRS| Microsoft Docs
description: 보고서 뷰어 사용자 지정 웹 파트를 사용하여 SharePoint 사이트에서 SQL Server Reporting Services 보고서를 보고, 탐색하고, 인쇄하고, 내보낼 수 있습니다.
ms.date: 02/11/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2eb1b02a7291d7d9eccd95a082fadb71f5e07010
ms.sourcegitcommit: 4b7ecc080795c5f90322d60df5c0550884f48140
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/06/2020
ms.locfileid: "94334437"
---
# <a name="report-viewer-web-part-on-a-sharepoint-site---reporting-services"></a>SharePoint 사이트의 보고서 뷰어 웹 파트 - Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)]  [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2016-and-later](../../includes/ssrs-appliesto-sharepoint-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-not-sharepoint-online](../../includes/ssrs-appliesto-not-sharepoint-online.md)]

보고서 뷰어 웹 파트는 사용자 지정 웹 파트입니다. 웹 파트를 사용하여 SharePoint 사이트 내의 보고서 서버에서 보고서를 보고 탐색하며 인쇄하고 내보낼 수 있습니다. 보고서 뷰어 웹 파트는 Microsoft SQL Server Reporting Services 보고서 서버에서 처리하는 보고서 정의 파일(.rdl)과 연결됩니다. 

최신 보고서 뷰어 웹 파트는 Power BI Report Server에 배포된 페이지를 매긴 보고서를 제공할 수도 있습니다. 웹 파트는 Power BI 보고서와 함께 작동하지 않습니다.

## <a name="why-the-report-viewer-web-part-is-re-introduced"></a>보고서 뷰어 웹 파트가 다시 도입되는 이유

보고서 뷰어 웹 파트는 SharePoint 제품용 Reporting Services 추가 기능의 일환으로 사용할 수 있었습니다. 웹 파트는 SharePoint 통합 모드의 보고서 서버에 대한 것이었습니다. SharePoint 통합 모드는 SQL Server 2016 이후 사용되지 않았습니다.

SQL Server 2017부터 Reporting Services의 설치 모드는 **기본 모드** 하나뿐입니다. *rs:Embed=true* URL 매개 변수를 사용하는 페이지 뷰어 웹 파트를 사용하여 모든 보고서 형식을 포함할 수 있습니다. SharePoint 페이지에 보고서를 포함하는 것은 고객이 요청한 통합 스토리이며 업데이트된 보고서 뷰어 웹 파트를 통해 페이지가 매겨진 보고서에 대해 이 시나리오가 지원됩니다.

페이지 뷰어 웹 파트가 페이지가 매겨진 보고서를 SharePoint 페이지에 포함하는 데 충분한 반면 업데이트된 보고서 뷰어 웹 파트는 추가 기능을 제공합니다.

* 특정 도구 모음 단추 표시/숨기기
* 보고서 매개 변수 값 재정의
* 보고서 매개 변수에 필터 웹 파트 연결

## <a name="download-the-report-viewer-web-part-solution-package"></a>보고서 뷰어 웹 파트 솔루션 패키지 다운로드

보고서 뷰어 웹 파트는 Microsoft 다운로드 센터에서 제공됩니다.

[보고서 뷰어 웹 파트 솔루션 패키지 다운로드](https://www.microsoft.com/download/details.aspx?id=55949)

## <a name="considerations-and-limitations"></a>고려 사항 및 제한 사항

나열된 항목은 업데이트된 보고서 뷰어 웹 파트와 관련이 있습니다.

* 웹 파트는 *클래식* SharePoint 페이지에서만 사용할 수 있습니다.
* 페이지를 매긴(RDL) 보고서에만 보고서 뷰어 웹 파트에서 포함이 지원됩니다. Power BI 보고서 또는 모바일 보고서를 포함하려는 경우 *rs:Embed=true* URL 매개 변수를 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

업데이트된 보고서 뷰어 웹 파트를 시작하려면 [SharePoint 사이트의 보고서 뷰어 웹 파트 배포](deploy-report-viewer-web-part.md)를 참조하세요.
