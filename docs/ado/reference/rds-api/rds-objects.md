---
description: RDS 개체
title: RDS 개체 | Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
helpviewer_keywords:
- objects [ADO], RDS
- RDS objects [ADO]
ms.assetid: f2ac8b3b-f968-41c4-a504-7aee3538b7c7
author: rothja
ms.author: jroth
ms.openlocfilehash: fa9329b1da84643f75a83ee1487f8c1be47601b1
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724344"
---
# <a name="rds-objects"></a>RDS 개체
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](/dotnet/framework/wcf/)로 마이그레이션해야 합니다.  
  
|개체|Description|  
|-|-|  
|[DataControl (RDS)](./datacontrol-object-rds.md)|텍스트 상자, 표 형태 컨트롤 또는 콤보 상자와 같은 하나 이상의 컨트롤에 데이터 쿼리 **레코드 집합** 을 바인딩하여 웹 페이지에 **레코드 집합** 데이터를 표시 합니다.<br /><br /> **DataControl** 개체는 스크립팅에 안전 합니다.|  
|[DataFactory (RDSServer)](./datafactory-object-rdsserver.md)|클라이언트 쪽 응용 프로그램에 대해 지정 된 데이터 소스에 대 한 읽기/쓰기 데이터 액세스를 제공 하는 메서드를 구현 합니다.<br /><br /> **DataFactory** 개체는 스크립팅에 안전 하지 않습니다.|  
|[스페이스 (RDS)](./dataspace-object-rds.md)|중간 계층에 있는 사용자 지정 비즈니스 개체에 대 한 클라이언트 쪽 프록시를 만듭니다.<br /><br /> **스페이스** 개체는 스크립팅에 안전 합니다.|  
|[IRDSService 인터페이스(RDS)](./irdsservice-interface-rds.md)|개체의 지원 되는 버전에서 요청 된 인터페이스에 대 한 포인터를 반환 하는 데 사용 되는 [InvokeService (RDS)](./invokeservice-rds.md) 메서드를 노출 합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [RDS API 참조](./rds-api-reference.md)