---
description: Azure Blob 다운로드 작업
title: Azure Blob 다운로드 작업 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobdltask.f1
- sql14.dts.designer.afpblobdltask.f1
ms.assetid: 8a63bf44-71be-456d-9a5c-be7c31aff065
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6437172ce0336938ad17a8b49bdb81e6fc4a0177
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130590"
---
# <a name="azure-blob-download-task"></a>Azure Blob 다운로드 작업

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


Azure Blob 다운로드 작업을 사용하면 SSIS 패키지에서 Azure Blob Storage의 파일을 다운로드할 수 있습니다.

**Azure Blob 다운로드 태스크** 를 추가하려면 이 작업을 SSIS 디자이너로 끌어서 놓고 두 번 클릭하거나 마우스 오른쪽 단추를 클릭하고 **편집** 을 클릭하여 다음과 같은 **Azure Blob 다운로드 태스크 편집기** 대화 상자를 표시합니다.  
  
 **Azure Blob 다운로드 태스크** 는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.  
  
 다음 표에서는 이 대화 상자의 필드에 대해 설명합니다.  

|**필드**|**설명**|  
|---|---|
|AzureStorageConnection|기존 Azure Storage 연결 관리자를 지정하거나 Blob 파일이 호스트되는 위치를 가리키는 Azure Storage 계정을 참조하는 스토리지 연결 관리자를 새로 만듭니다.|  
|BlobContainer|다운로드할 Blob 파일을 포함하는 Blob 컨테이너의 이름을 지정합니다.|  
|BlobDirectory|다운로드할 Blob 파일을 포함하는 Blob 디렉터리를 지정합니다. blob 디렉터리는 가상 계층 구조입니다.|  
|SearchRecursively|하위 디렉터리 안에서 재귀적으로 검색할 것인지 여부를 지정합니다.|  
|LocalDirectory|다운로드한 Blob 파일을 저장할 로컬 디렉터리를 지정합니다.|  
|FileName|지정된 이름 패턴의 파일을 선택할 이름 필터를 지정합니다. 예를 들어 `MySheet*.xls\*`는 `MySheet001.xls` 및 `MySheetABC.xlsx`와 같은 파일을 포함합니다.|  
|TimeRangeFrom/TimeRangeTo|시간 범위 필터를 지정합니다. **TimeRangeFrom** 에서 **TimeRangeTo** 사이에 수정된 파일이 포함됩니다.|  
