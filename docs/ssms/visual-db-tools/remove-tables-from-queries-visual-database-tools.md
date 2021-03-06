---
description: 쿼리에서 테이블 제거(Visual Database Tools)
title: 쿼리에서 테이블 제거
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting tables
- removing tables
- dropping tables
- queries [SQL Server], tables
ms.assetid: 8fea0b4f-99b7-4050-8d6f-a97ffb839619
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 6c92732dc2cb4fcd817a8c954fa9d29048cd57bd
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038678"
---
# <a name="remove-tables-from-queries-visual-database-tools"></a>쿼리에서 테이블 제거(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
쿼리에서 테이블이나 모든 테이블 반환 개체를 제거할 수 있습니다.  
  
> [!NOTE]  
> 테이블이나 테이블 반환 개체를 제거해도 데이터베이스에서 실제로 삭제되는 항목은 없으며 현재 쿼리에서 해당 항목이 제거될 뿐입니다. 데이터베이스에서 테이블을 제거하는 자세한 내용은 [방법: 데이터베이스에서 테이블 삭제](../../relational-databases/tables/delete-tables-database-engine.md)를 참조하세요.  
  
### <a name="to-remove-a-table-or-table-structured-object"></a>테이블이나 테이블 구조 개체를 제거하려면  
  
-   **다이어그램 창**에서 테이블, 뷰, 사용자 정의 함수, 동의어 또는 쿼리를 선택한 다음 Delete 키를 누르거나, 개체를 마우스 오른쪽 단추로 클릭한 다음 대화 상자가 나타나면 **제거** 를 선택합니다. 여러 개체를 한번에 선택하거나 제거할 수 있습니다.  
  
    또는  
  
-   **SQL 창**에서 개체에 대한 모든 참조를 제거합니다.  
  
테이블이나 테이블 반환 개체를 제거할 때 쿼리 및 뷰 디자이너에서는 해당 테이블이나 테이블 반환 개체가 관련된 조인을 자동으로 제거하고 **SQL 창** 과 **조건 창**에서 개체의 열에 대한 참조를 제거합니다. 그러나 해당 개체가 관련된 복합 식이 쿼리에 포함되어 있으면 개체가 자동으로 제거되지 않습니다. 이 경우 개체를 제거하려면 해당 개체에 대한 모든 참조를 제거해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리에 테이블 추가](../../ssms/visual-db-tools/add-tables-to-queries-visual-database-tools.md)  
[테이블 별칭 만들기](../../ssms/visual-db-tools/create-table-aliases-visual-database-tools.md)  
[검색 기준 지정](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[쿼리 결과 요약](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[쿼리 관련 기본 작업 수행](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
