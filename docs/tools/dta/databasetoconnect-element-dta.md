---
title: DatabaseToConnect 요소(DTA)
description: dta 유틸리티에서 DatabaseToConnect 요소는 워크로드를 튜닝할 때 데이터베이스 엔진 튜닝 관리자가 연결하는 첫 번째 데이터베이스를 지정합니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 1d03125d005d1374f75799813a355c5165713bfc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85732113"
---
# <a name="databasetoconnect-element-dta"></a>DatabaseToConnect 요소(DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

작업 튜닝 시 데이터베이스 엔진 튜닝 관리자가 연결되는 첫 번째 데이터베이스를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특성|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 길이 제한 없음|  
|**기본값**|없음|  
|**발생 빈도**|(선택 사항) 각 **TuningOptions** 요소에 한 번만 사용할 수 있습니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[TuningOptions 요소&#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**자식 요소**|None|  
  
## <a name="remarks"></a>설명  
 **DatabaseToConnect** 를 사용하여 데이터베이스 엔진 튜닝 관리자가 튜닝 세션을 시작할 때 연결되는 첫 번째 데이터베이스의 이름을 지정할 수 있습니다. 이 요소에서는 데이터베이스를 하나만 지정할 수 있습니다. 여러 데이터베이스 이름을 지정할 경우 데이터베이스 엔진 튜닝 관리자는 오류를 반환합니다.  
  
## <a name="example"></a>예제  
 사용 예제를 보려면 [인라인 워크로드가 포함된 XML 입력 파일 예제&#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
