---
title: 계획 지침에 정해진 쿼리 계획 적용 | Microsoft 문서
description: SQL Server에서 OBJECT 또는 SQL 유형의 계획 지침에 정해진 쿼리 계획을 적용하는 방법을 알아봅니다. 이 예제에서는 간단한 임시 SQL 문에 대한 계획 지침을 만듭니다.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: bbf401f9-af7c-48e7-8a43-bf25e8af2fd7
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 550933e8c8152bd021c871d4e466f1b9fafb3907
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505449"
---
# <a name="apply-a-fixed-query-plan-to-a-plan-guide"></a>계획 지침에 정해진 쿼리 계획 적용
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  OBJECT 또는 SQL 유형의 계획 지침에 정해진 쿼리 계획을 적용할 수 있습니다. 정해진 쿼리 계획을 적용하는 계획 지침은 최적화 프로그램에서 특정 쿼리에 대해 선택한 실행 계획보다 더 뛰어난 기존 실행 계획을 알고 있는 경우 유용합니다.  
  
 다음 예에서는 간단한 임시 SQL 문에 대한 계획 지침을 만듭니다. `@hints` 매개 변수에 직접 쿼리에 대한 XML 실행 계획을 지정하여 이 문에 대해 원하는 쿼리 계획을 계획 지침에 제공합니다. 예에서는 먼저 SQL 문을 실행하여 계획 캐시에 계획을 생성합니다. 이 예를 위해 생성된 계획이 원하는 계획이며 추가 쿼리 튜닝이 필요하지 않다고 가정합니다. 쿼리에 대한 XML 실행 계획은 `sys.dm_exec_query_stats`, `sys.dm_exec_sql_text`및 `sys.dm_exec_text_query_plan` 동적 관리 뷰를 쿼리하여 가져오고 `@xml_showplan` 변수에 할당됩니다. 그런 다음 `@xml_showplan` 변수는 `sp_create_plan_guide` 매개 변수의 `@hints` 문에 전달됩니다. 또는 [sp_create_plan_guide_from_handle](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md) 저장 프로시저를 사용하여 계획 캐시의 쿼리 계획에서 계획 지침을 만들 수 있습니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;  
GO  
DECLARE @xml_showplan nvarchar(max);  
SET @xml_showplan = (SELECT query_plan  
    FROM sys.dm_exec_query_stats AS qs   
    CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st  
    CROSS APPLY sys.dm_exec_text_query_plan(qs.plan_handle, DEFAULT, DEFAULT) AS qp  
    WHERE st.text LIKE N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;%');  
  
EXEC sp_create_plan_guide   
    @name = N'Guide1_from_XML_showplan',   
    @stmt = N'SELECT City, StateProvinceID, PostalCode FROM Person.Address ORDER BY PostalCode DESC;',   
    @type = N'SQL',  
    @module_or_batch = NULL,   
    @params = NULL,   
    @hints = @xml_showplan;  
GO  
```  
  
  
