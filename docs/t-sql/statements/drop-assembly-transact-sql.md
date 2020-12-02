---
description: DROP ASSEMBLY(Transact-SQL)
title: DROP ASSEMBLY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP ASSEMBLY
- DROP_ASSEMBLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing assemblies
- DROP ASSEMBLY statement
- deleting assemblies
- assemblies [CLR integration], removing
- dropping assemblies
- WITH NO DEPENDENTS option
ms.assetid: 452d181a-a8e6-44a3-975d-29966d01b18d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 601d7bdff19c6e6d8f4daec58c28c048891bcc82
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96131330"
---
# <a name="drop-assembly-transact-sql"></a>DROP ASSEMBLY(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스에서 어셈블리 및 모든 관련 파일을 제거합니다. 어셈블리는 [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md)를 사용하여 만들고 [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md)를 사용하여 수정할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
DROP ASSEMBLY [ IF EXISTS ] assembly_name [ ,...n ]  
[ WITH NO DEPENDENTS ]  
[ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *IF EXISTS*  
 **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
 이미 있는 경우에만 테이블을 조건부로 삭제합니다.  
  
 *assembly_name*  
 삭제할 어셈블리의 이름입니다.  
  
 WITH NO DEPENDENTS  
 지정하면 *assembly_name* 만 삭제되고 어셈블리에서 참조하는 종속 어셈블리는 삭제되지 않습니다. 지정하지 않으면 DROP ASSEMBLY가 *assembly_name* 과 모든 종속 어셈블리를 삭제합니다.  
  
## <a name="remarks"></a>설명  
 어셈블리를 삭제하면 데이터베이스에서 어셈블리와 원본 코드 및 디버그 파일 등의 모든 관련 파일이 제거됩니다.  
  
 WITH NO DEPENDENTS를 지정하지 않으면 DROP ASSEMBLY가 *assembly_name* 과 모든 종속 어셈블리를 삭제합니다. 종속 어셈블리를 삭제하려는 시도가 실패하면 DROP ASSEMBLY가 오류를 반환합니다.  
  
 어셈블리가 데이터베이스에 있는 다른 어셈블리에서 참조되거나 현재 데이터베이스의 CLR(공용 언어 런타임) 함수, 프로시저, 트리거, 사용자 정의 형식 또는 집계에서 사용되면 DROP ASSEMBLY가 오류를 반환합니다.  
  
 DROP ASSEMBLY는 현재 실행되고 있는 어셈블리를 참조하는 코드를 방해하지 않습니다. 그러나 DROP ASSEMBLY를 실행한 후에는 어셈블리 코드를 호출하려는 모든 시도가 실패합니다.  
  
## <a name="permissions"></a>사용 권한  
 어셈블리 소유권이나 어셈블리에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `HelloWorld` 어셈블리가 이미 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 생성된 것으로 가정합니다.  
  
```sql  
DROP ASSEMBLY Helloworld ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)   
 [ALTER ASSEMBLY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [어셈블리에 대한 정보 가져오기](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
