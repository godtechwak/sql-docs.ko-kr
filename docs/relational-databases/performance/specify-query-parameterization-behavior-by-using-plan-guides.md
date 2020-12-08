---
title: 계획 지침을 사용하여 쿼리 매개 변수화 동작 설정
description: SQL Server의 쿼리에서 리터럴 값이 매개 변수로 대체되는 매개 변수화를 위한 옵션을 살펴봅니다.
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- TEMPLATE plan guide
- PARAMETERIZATION FORCED option
- PARAMETERIZATION option
- PARAMETERIZATION SIMPLE option
- parameterization [SQL Server]
- overriding parameterization behavior
- plan guides [SQL Server], parameterization
- parameterized queries [SQL Server]
ms.assetid: f0f738ff-2819-4675-a8c8-1eb6c210a7e6
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: d4aa6359d3de9ff2106e4e82ebc27a62f15a2efa
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505011"
---
# <a name="specify-query-parameterization-behavior-by-using-plan-guides"></a>계획 지침을 사용하여 쿼리 매개 변수화 동작 지정
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  PARAMETERIZATION 데이터베이스 옵션이 SIMPLE로 설정된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 최적화 프로그램은 쿼리를 매개 변수화하도록 선택할 수 있습니다. 즉, 쿼리에 포함된 모든 리터럴 값은 매개 변수로 대체됩니다. 이 프로세스를 단순 매개 변수화라고 합니다. SIMPLE 매개 변수화가 적용되면 매개 변수화할 쿼리와 매개 변수화하지 않을 쿼리를 제어할 수 없습니다. 그러나 PARAMETERIZATION 데이터베이스 옵션을 FORCED로 설정하여 데이터베이스의 모든 쿼리가 매개 변수화되도록 지정할 수 있습니다. 이 프로세스를 강제 매개 변수화라고 합니다.  
  
 다음 방법으로 계획 지침을 사용하여 데이터베이스의 매개 변수화 동작을 무시할 수 있습니다.  
  
-   PARAMETERIZATION 데이터베이스 옵션을 SIMPLE로 설정하면 특정 쿼리 클래스에 강제 매개 변수화가 시도되도록 지정할 수 있습니다. 이렇게 하려면 매개 변수가 있는 쿼리 형식에 대한 TEMPLATE 계획 지침을 만들고 PARAMETERIZATION FORCED 쿼리 힌트를 [sp_create_plan_guide](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md) 저장 프로시저에 지정합니다. 모든 쿼리 대신 쿼리의 특정 클래스에만 강제 매개 변수화를 사용하여 이러한 종류의 계획 지침을 고려할 수 있습니다. 단순 매개 변수화에 대한 자세한 내용은 [쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md#SimpleParam)를 참조하세요. 
  
-   PARAMETERIZATION 데이터베이스 옵션을 FORCED로 설정하면 특정 쿼리 클래스에 대해 강제 매개 변수화가 아닌 단순 매개 변수화만 시도되도록 지정할 수 있습니다. 이렇게 하려면 매개 변수가 강제로 지정된 쿼리 형식에 대한 TEMPLATE 계획 지침을 만들고 PARAMETERIZATION SIMPLE 쿼리 힌트를 **sp_create_plan_guide** 에 지정합니다.  강제 매개 변수화에 대한 자세한 내용은 [쿼리 처리 아키텍처 가이드](../../relational-databases/query-processing-architecture-guide.md#ForcedParam)를 참조하세요. 
  
 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 다음 쿼리를 검토하십시오.  
  
```sql  
SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
FROM Production.ProductModel AS pm   
    INNER JOIN Production.ProductInventory AS pi   
        ON pm.ProductModelID = pi.ProductID   
WHERE pi.ProductID = 101   
GROUP BY pi.ProductID, pi.Quantity HAVING SUM(pi.Quantity) > 50;  
```  
  
 데이터베이스 관리자는 데이터베이스의 모든 쿼리에 대해 강제 매개 변수화를 사용하지 않기로 결정했습니다. 그러나 구문상으로는 위의 쿼리와 동일하지만 해당 상수 리터럴 값만 다른 모든 쿼리에 대해 컴파일 비용이 발생하지 않기를 바랍니다. 즉, 이러한 종류의 쿼리에 대한 쿼리 계획을 다시 사용할 수 있도록 쿼리를 매개 변수화하려고 합니다. 이 경우 다음 단계를 완료합니다.  
  
1.  매개 변수가 있는 쿼리 형식을 검색합니다. **sp_create_plan_guide** 에서 사용하기 위해 이 값을 얻는 안정적인 한 가지 방법은 [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) 시스템 저장 프로시저를 사용하는 것입니다.  
  
2.  PARAMETERIZATION FORCED 쿼리 힌트를 지정하여 매개 변수가 있는 쿼리 형식에 대한 계획 지침을 만듭니다.  

    > [!IMPORTANT]  
    >  쿼리를 매개 변수화하는 과정의 일부로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 리터럴 값 및 크기에 따라 리터럴 값을 바꾸는 매개 변수에 데이터 유형을 할당합니다. 같은 프로세스가 **sp_get_query_template** 의 **\@stmt** 출력 매개 변수에 전달된 상수 리터럴 값에서 발생합니다. **sp_create_plan_guide\@ 의** **params** 인수에 지정된 데이터 유형이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 의해 매개 변수화된 쿼리의 데이터 유형과 일치해야 하므로 쿼리에 사용할 수 있는 매개 변수 값의 전체 범위를 포함하는 계획 지침을 두 개 이상 만들어야 할 수 있습니다.  

다음 스크립트는 매개 변수가 있는 쿼리를 얻고 이에 대한 계획 지침을 만들기 위해 사용할 수 있습니다.  
  
```sql  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total   
      FROM Production.ProductModel AS pm   
      INNER JOIN Production.ProductInventory AS pi ON pm.ProductModelID = pi.ProductID   
      WHERE pi.ProductID = 101   
      GROUP BY pi.ProductID, pi.Quantity   
      HAVING sum(pi.Quantity) > 50',  
    @stmt OUTPUT,   
    @params OUTPUT;  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
마찬가지로 강제 매개 변수화가 이미 설정된 데이터베이스에서 예제 쿼리 및 구문상 동일한 기타 쿼리(해당 상수 리터럴 값 제외)가 단순 매개 변수화 규칙에 따라 매개 변수화되었는지 확인할 수 있습니다. 이렇게 하려면 OPTION 절에 PARAMETERIZATION FORCED 대신 PARAMETERIZATION SIMPLE을 지정합니다.  
  
> [!NOTE]  
>  TEMPLATE 계획 지침은 문을 하나의 문으로만 구성되어 있는 일괄 처리에 제출된 쿼리와 일치시킵니다. 다중 문 일괄 처리 내에 있는 문은 TEMPLATE 계획 지침에 일치시킬 수 없습니다.
