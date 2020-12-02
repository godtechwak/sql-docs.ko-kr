---
description: InfoSource 만들기
title: InfoSource 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e7db233b-5464-43de-9d26-6dd24c7ac1b7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c4672ce48890af7202445d283d15c2c167550f5a
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127256"
---
# <a name="create-infosource"></a>InfoSource 만들기

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **InfoSource 만들기** 대화 상자에서는 새 InfoSource를 만들 수 있습니다. 새 InfoSource를 만들려면 **트랜잭션 데이터용 InfoSource 만들기** 또는 **마스터 데이터용 InfoSource 만들기** 대화 상자를 사용합니다.  
  
 **InfoSource 만들기** 대화 상자는 **SAP BW 대상 편집기** 의 **연결 관리자** 페이지에서 열 수 있습니다. SAP BW 대상에 대한 자세한 내용은 [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  SAP BW용 Microsoft Connector 1.1 설명서는 SAP Netweaver BW 환경에 익숙한 것으로 가정합니다. SAP Netweaver BW 또는 SAP Netweaver BW 개체 및 프로세스 구성 방법에 대한 자세한 내용은 SAP 설명서를 참조하십시오.  
  
 **InfoSource 만들기 대화 상자를 열려면**  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 SAP BW 대상이 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 엽니다.  
  
2.  **데이터 흐름** 탭에서 SAP BW 대상을 두 번 클릭합니다.  
  
3.  **SAP BW 대상 편집기** 에서 **연결 관리자** 를 클릭하여 편집기의 **연결 관리자** 페이지를 엽니다.  
  
4.  **연결 관리자** 페이지의 **SAP BW 개체 만들기** 그룹 상자에서 **InfoSource** 를 선택한 다음 **만들기** 를 클릭합니다.  
  
## <a name="options"></a>옵션  
 **트랜잭션 데이터**  
 트랜잭션 데이터용 새 InfoSource를 만듭니다.  
  
 이 옵션을 선택하는 경우 **트랜잭션 데이터용 InfoSource 만들기** 대화 상자가 열립니다. **트랜잭션 데이터용 InfoSource 만들기** 대화 상자를 사용하여 새 InfoSource를 만들 수 있습니다. 이 대화 상자에 대한 자세한 내용은 [Create InfoSource for Transaction Data](../../integration-services/data-flow/create-infosource-for-transaction-data.md)을 참조하십시오.  
  
 **마스터 데이터**  
 마스터 데이터용 새 InfoSource를 만듭니다.  
  
 이 옵션을 선택하는 경우 **마스터 데이터용 InfoSource 만들기** 대화 상자가 열립니다. **마스터 데이터용 InfoSource 만들기** 대화 상자를 사용하여 새 InfoSource를 만들 수 있습니다. 이 대화 상자에 대한 자세한 내용은 [Create InfoSource for Master Data](../../integration-services/data-flow/create-infosource-for-master-data.md)을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft Connector for SAP BW F1 도움말](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
