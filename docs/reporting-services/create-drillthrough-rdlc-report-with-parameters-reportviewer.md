---
title: 매개 변수가 있는 드릴스루(RDLC) 보고서 만들기 - ReportViewer | Microsoft Docs
description: 로컬 모드 보고에서 매개 변수 및 쿼리를 사용하여 드릴스루(RDLC) 보고서를 만드는 방법을 알아봅니다.
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 628c8775-c62d-45ac-b349-23db86fa4e6c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7f6e6e631b32aa7eab8d6c56c8b6f9e2cf03752f
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891203"
---
# <a name="create-drillthrough-rdlc-report-with-parameters---reportviewer"></a>매개 변수가 있는 드릴스루(RDLC) 보고서 만들기 - ReportViewer
[드릴스루](./report-design/drillthrough-reports-report-builder-and-ssrs.md) 보고서는 다른 보고서 내에서 링크를 클릭했을 때 열리는 보고서입니다. 드릴스루 보고서는 원본 요약 보고서에 포함된 항목에 대한 세부 정보를 포함합니다. 이 자습서에서는 [로컬 모드 보고](report-server-sharepoint/local-mode-vs-connected-mode-reports-in-the-report-viewer.md)에서 매개 변수 및 쿼리가 있는 드릴스루 보고서를 만드는 다음과 같은 단원을 설명합니다.  
  
## <a name="requirements"></a>요구 사항  
이 연습을 사용하려면 **AdventureWorks2014** 샘플 데이터베이스에 대한 액세스 권한이 있어야 합니다. **AdventureWorks2014** 샘플 데이터베이스를 가져오는 방법에 대한 자세한 내용은 [AdventureWorks 샘플 데이터베이스](https://github.com/Microsoft/sql-server-samples/releases)를 참조하세요.  
  
이 연습에서는 Transaction-SQL 쿼리와 ADO.NET [DataSet](/dotnet/api/system.data.dataset) 및 [DataTable](/dotnet/api/system.data.datatable) 개체를 잘 알고 있다고 가정합니다.  
  
Visual Studio 2015 및 ASP.NET 웹 애플리케이션을 사용하여 ReportViewer 컨트롤이 있는 ASP.NET 웹 페이지를 만듭니다. 컨트롤은 사용자가 만드는 보고서를 보도록 구성됩니다. 이 연습에서는 Microsoft Visual C#에서 애플리케이션을 만듭니다.  
  
## <a name="tasks"></a>작업  
[1단원: 새 웹 사이트 만들기](../reporting-services/lesson-1-create-a-new-web-site.md)  
[2단원: 부모 보고서에 대한 데이터 연결 및 데이터 테이블 정의](../reporting-services/lesson-2-define-a-data-connection-and-data-table-for-parent-report.md)  
[3단원: 보고서 마법사를 사용하여 부모 보고서 디자인](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md)  
[4단원: 자식 보고서에 대한 데이터 연결 및 데이터 테이블 정의](../reporting-services/lesson-4-define-a-data-connection-and-data-table-for-child-report.md)  
[5단원: 보고서 마법사를 사용하여 자식 보고서 디자인](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md)  
[단원 6: 애플리케이션에 ReportViewer 컨트롤 추가](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md)  
[7단원: 부모 보고서에 드릴스루 동작 추가](../reporting-services/lesson-7-add-drillthrough-action-on-parent-report.md)  
[8단원: 데이터 필터 만들기](../reporting-services/lesson-8-create-a-data-filter.md)  
[단원 9: 애플리케이션 빌드 및 실행](../reporting-services/lesson-9-build-and-run-the-application.md)  
  
## <a name="see-also"></a>참고 항목  
[Reporting Services&#40;SSRS&#41; 자습서](../reporting-services/reporting-services-tutorials-ssrs.md)  
[보고서 디자이너로 보고서 디자인&#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md)  
