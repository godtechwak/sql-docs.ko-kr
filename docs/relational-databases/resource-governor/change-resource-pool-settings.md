---
title: 리소스 풀 설정 변경 | Microsoft 문서
description: SQL Server Management Studio 또는 Transact-SQL을 사용하여 리소스 풀 설정을 변경하는 방법을 알아봅니다. 이 작업에는 CONTROL SERVER 권한이 필요합니다.
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool alter
- resource pools [SQL Server], alter
ms.assetid: 49438285-a011-4dac-bd4f-f35cd90fda61
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: ff9f9de71985cc853022da27ec1990fb1ac3d1ce
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96504858"
---
# <a name="change-resource-pool-settings"></a>리소스 풀 설정 변경
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 리소스 풀 설정을 변경할 수 있습니다.  
  
-   **시작하기 전 주의 사항:**  [제한 사항](#LimitationsRestrictions), [사용 권한](#Permissions)  
  
-   **리소스 풀 설정을 변경하려면 다음을 사용합니다.**  [SQL Server Management Studio](#ChgRPProp), [Transact-SQL](#ChgRPTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 제한 사항  
 최대 CPU 비율은 최소 CPU 비율보다 크거나 같아야 합니다. 최대 메모리 비율은 최소 메모리 비율보다 크거나 같아야 합니다.  
  
 모든 리소스 풀에 대한 최대 CPU 비율과 최소 CPU 비율의 합은 100을 초과할 수 없습니다.  
  
###  <a name="permissions"></a><a name="Permissions"></a> 권한  
 리소스 풀 설정을 변경하려면 CONTROL SERVER 권한이 필요합니다.  
  
##  <a name="change-resource-pool-settings-using-sql-server-management-studio"></a><a name="ChgRPProp"></a> SQL Server Management Studio를 사용하여 리소스 풀 설정 변경  
 **을 사용하여 리소스 풀 설정을 변경하려면(!!) [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 개체 탐색기를 열고 **리소스 풀** 이 나타날 때까지 **관리** 노드를 계속 확장합니다.  
  
2.  수정할 리소스 풀을 마우스 오른쪽 단추로 클릭하고 **속성** 을 클릭합니다.  
  
3.  **리소스 관리자 속성** 페이지의 **리소스 풀** 표에서 리소스 풀의 행이 자동으로 선택되어 있지 않으면 선택합니다.  
  
4.  변경할 행의 셀을 클릭 또는 두 번 클릭한 다음 새 값을 입력합니다.  
  
5.  **확인** 을 클릭하여 변경 내용을 저장합니다.  

##  <a name="change-resource-pool-settings-using-transact-sql"></a><a name="ChgRPTSQL"></a> Transact-SQL을 사용하여 리소스 풀 설정 변경  
 **을 사용하여 리소스 풀 설정을 변경하려면(!!) [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  변경할 속성 값을 지정하여 **ALTER RESOURCE POOL** 또는 **ALTER EXTERNAL RESOURCE POOL** 문을 실행합니다.  
  
2.  **ALTER RESOURCE GOVERNOR RECONFIGURE** 문을 실행합니다.  
  
### <a name="example-transact-sql"></a>예제(Transact-SQL)  
 다음 예에서는 `poolAdhoc`이라는 리소스 풀에 대한 최대 CPU 비율 설정을 변경합니다.  
  
```  
ALTER RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)   
 [리소스 관리자 사용](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [리소스 풀 만들기](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [리소스 풀 삭제](../../relational-databases/resource-governor/delete-a-resource-pool.md)   
 [리소스 관리자 작업 그룹](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [리소스 관리자 분류자 함수](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR&#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)  
  
  
