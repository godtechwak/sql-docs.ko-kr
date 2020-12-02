---
description: 새 정책 만들기 또는 정책 열기 대화 상자, 일반 페이지
title: ‘새 정책 만들기’ 또는 ‘정책 열기’ 대화 상자, 일반 페이지
descripton: Describes the 'General Page' of the 'Create New Policy' and 'Open Policy' dialog boxes for Policy-Based Management in SQL Server Management Studio (SSMS).
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.policy.f1
- sql13.swb.dmf.policy.filter.f1
- sql13.swb.dmf.newgroup.f1
ms.assetid: c00bebd0-d04b-4c64-840e-8b7a2c603436
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 60997f5a657db79dc9e31c17c47f02bfc12b3cad
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127902"
---
# <a name="create-new-policy-or-open-policy-dialog-box-general-page"></a>새 정책 만들기 또는 정책 열기 대화 상자, 일반 페이지
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 대화 상자를 사용하여 새 정책 기반 관리 정책을 만들거나 기존 정책을 수정할 수 있습니다. **적용 대상** 및 **서버 제한** 영역을 필터로 사용하여 정책을 사용 가능한 모든 대상의 하위 집합으로 제한할 수 있습니다. 조건을 대상 필터로 사용하려면 조건이 물리적 패싯에 대해 정의되어야 하며 함수를 포함하지 않아야 하고 Like 연산자를 포함하지 않아야 합니다. 시스템에서 정책에 대한 개체 집합을 계산할 때 기본적으로 시스템 개체가 제외됩니다.  예를 들어, 정책의 개체 집합이 모든 테이블을 참조할 경우 시스템 테이블에 정책이 적용되지 않습니다. 사용자가 시스템 개체에 대해 정책을 평가하려면 개체 집합에 시스템 개체를 명시적으로 추가합니다. 그러나 모든 정책이 **일정 검사** 평가 모드에 대해 지원되더라도 성능상의 이유로 임의 개체 집합의 모든 정책이 **변경 내용 검사** 평가 모드에 대해 지원되지는 않습니다. 자세한 내용은 [https://docs.microsoft.com/archive/blogs/sqlpbm/policy-evaluation-modes](/archive/blogs/sqlpbm/policy-evaluation-modes)를 참조하세요.  
  
## <a name="options"></a>옵션  
 **이름**  
 새 정책의 경우 새 정책 이름을 입력합니다. 기존 정책의 경우 이름이 표시됩니다.  
  
 **Enabled**  
 정책을 설정하려면 **사용** 확인란을 선택합니다. 정책을 해제하려면 **사용** 확인란의 선택을 취소합니다. **사용** 상자는 정책 자동화에 적용됩니다. 이 상자는 정책의 자동화 시스템을 만들거나 제거합니다. Automation은 다음과 같은 메커니즘을 사용합니다.  
  
 **변경 시: 방지**  
 데이터베이스 트리거에서 정책 준수를 적용합니다.  
  
 **변경 시: 로그만**  
 알림 서비스 이벤트가 정책 준수를 검사합니다.  
  
 **예약 시**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업이 생성되어 일정에 따른 정책 준수를 검사합니다.  
  
 **요청 시** 평가 모드를 사용하여 실행되는 정책은 이 확인란을 사용하지 않습니다.  
  
 **조건 확인**  
 이 정책이 사용하는 정책 기반 관리 조건을 선택합니다. 관련 정책 기반 관리 패싯에 대한 서버의 모든 조건이 나열됩니다. 새 조건을 만들려면 **새 조건** 을 클릭합니다. 조건을 수정하려면 줄임표 단추(**...**)를 클릭합니다.  
  
 **적용 대상**  
 이 패싯에서 필터 식을 완성하는 데 사용할 수 있는 대상 유형을 선택합니다.  
  
 **평가 모드**  
 정책의 평가 모드를 선택합니다. 일부 정책은 검사되지만 적용될 수는 없습니다. 평가 모드는 다음과 같습니다.  
  
 **요청 시**  
 정책은 **평가** 대화 상자에서 실행할 때만 실행됩니다.  
  
 **예약 시**  
 주기적으로 정책을 평가하고 정책을 준수하지 않는 정책에 대한 로그 항목을 기록하고 보고서를 만듭니다. **일정** 상자를 설정합니다.  
  
 **변경 시: 로그만**  
 변경을 시도하면 이 옵션은 정책을 준수하지 않는 변경을 방지하지 않지만 정책 위반을 기록합니다.  
  
 **변경 시: 방지**  
 변경을 시도하면 이 옵션은 정책을 위반하는 변경을 방지합니다.  
  
 **일정**  
 **예약 시** 평가 모드를 선택하면 이 옵션이 나타납니다. 일정 이름을 입력하고 **선택** 을 클릭하여 목록에서 일정을 선택하거나 **새로 만들기** 를 클릭하여 새 일정을 만듭니다. 일정 영역을 설정하려면 **예약 시** 를 선택해야 합니다.  
  
 **서버 제한**  
 이 정책에 적합한 서버 유형을 선택합니다. **없음** 을 선택하거나, 가능한 서버를 필터링하는 조건을 선택할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [정책 기반 관리를 사용하여 서버 관리](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
