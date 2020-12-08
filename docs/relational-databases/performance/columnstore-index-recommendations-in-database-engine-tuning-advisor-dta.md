---
title: Columnstore 인덱스 권장 사항 - DTA(데이터베이스 엔진 튜닝 관리자)
description: 데이터베이스 엔진 튜닝 관리자가 워크로드를 분석하여 SQL Server의 데이터베이스에서 빌드할 rowstore 및 columnstore 인덱스를 권장하는 방식을 알아봅니다.
ms.custom: seo-dt-2019
ms.date: 01/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor, columnstore index
- Database Engine Tuning Advisor, columnstore and rowstore indexes
ms.assetid: 9fba1139-82cb-4244-a41f-4337a7d0c132
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 441b0c37a39efaf02ff00d64b893896cd3fe8f6f
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505377"
---
# <a name="columnstore-index-recommendations-in-database-engine-tuning-advisor-dta"></a>DTA(데이터베이스 엔진 튜닝 관리자)의 Columnstore 인덱스 권장 사항
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

 
  데이터 웨어하우징 및 분석 워크로드는 기존의 rowstore 인덱스뿐만 아니라 [columnstore 인덱스](../../t-sql/statements/create-columnstore-index-transact-sql.md)를 활용할 수 있습니다. 데이터베이스에 대해 작성할 rowstore 및 columnstore 인덱스 선택은 애플리케이션의 워크로드에 따라 달라집니다. SQL Server 2016의 [DTA(데이터베이스 엔진 튜닝 관리자)](../../relational-databases/performance/database-engine-tuning-advisor.md)는 워크로드를 분석하고 데이터베이스에 작성할 적절한 rowstore 및 columnstore 인덱스 조합을 권장할 수 있습니다. 
  
 이 기능은 SQL Server Management Studio 버전 **16.4** 이상에서 사용할 수 있습니다. 
  
## <a name="how-to-enable-columnstore-index-recommendations-in-database-engine-tuning-advisor-gui"></a>데이터베이스 엔진 튜닝 관리자 GUI에서 columnstore 인덱스 권장 사항을 사용하도록 설정하는 방법

  
  1. 데이터베이스 엔진 튜닝 관리자를 시작하고 새 튜닝 세션을 엽니다.
  
  2. **일반** 창에서 튜닝할 데이터베이스 및 워크로드를 선택합니다.
  
  3. 튜닝 옵션 창에서 **columnstore 인덱스 권장** 확인란을 선택합니다(아래 그림 참조).
  ![DTA Columnstore 인덱스 튜닝 옵션](../../relational-databases/performance/media/dta-columnstore-indexes-tuning-option.gif)
 
  4. 다른 튜닝 옵션을 선택하고 **분석 시작** 단추를 클릭합니다.
  
  5. 튜닝이 완료되면 **권장 사항** 창에서 columnstore 인덱스를 포함하여 모든 권장 사항을 확인합니다(아래 그림 참조).      
  ![DTA columnstore 인덱스 권장 사항](../../relational-databases/performance/media/dta-columnstore-index-recommendation.gif)
  
  6. **정의** 하이퍼링크를 클릭하여 권장 인덱스를 만들 수 있는 SQL DDL(데이터 정의 언어) 문을 확인합니다. 기본적으로 DTA는 columnstore 인덱스를 식별하기 쉽도록 columnstore 인덱스의 이름에 접미사 **col** 을 사용합니다(아래 그림 참조).
  ![DTA columnstore 인덱스 정의](../../relational-databases/performance/media/dta-columnstore-index-definition.gif) 
  
  
  ## <a name="how-to-enable-columnstore-index-recommendations-in-dtaexe-utility"></a>dta.exe 유틸리티에서 columnstore 인덱스 권장 사항을 사용하도록 설정하는 방법

dta.exe 명령줄 유틸리티를 사용할 때 columnstore 권장 사항을 사용하도록 설정하려면 **-fc** 명령줄 매개 변수를 사용합니다.

dta.exe 명령줄 유틸리티에 대한 자세한 내용은 [dta 유틸리티](../../tools/dta/dta-utility.md)를 참조하세요.

## <a name="see-also"></a>참고 항목
[Columnstore 인덱스 가이드](../../relational-databases/indexes/columnstore-indexes-overview.md)       
[데이터베이스 엔진 튜닝 관리자](../../relational-databases/performance/database-engine-tuning-advisor.md)      
[자습서: 데이테베이스 엔진 튜닝 관리자](../../tools/dta/tutorial-database-engine-tuning-advisor.md)



  

