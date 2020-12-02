---
description: ALTER SERVICE(Transact-SQL)
title: ALTER SERVICE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER SERVICE
- ALTER_SERVICE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- modifying services
- contracts [Service Broker], modifying
- ALTER SERVICE statement
- services [Service Broker], modifying
ms.assetid: 2b4608f7-bb2e-4246-aa29-b52c55995b3a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c6a9ed30e92358d269fa4d6c0e270bd4a16e3bdb
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126257"
---
# <a name="alter-service-transact-sql"></a>ALTER SERVICE(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  기존 서비스를 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql 
ALTER SERVICE service_name   
   [ ON QUEUE [ schema_name . ]queue_name ]   
   [ ( < opt_arg > [ , ...n ] ) ]  
[ ; ]  
  
<opt_arg> ::=  
   ADD CONTRACT contract_name | DROP CONTRACT contract_name  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *service_name*  
 변경할 서비스의 이름입니다. 서버, 데이터베이스 및 스키마 이름은 지정될 수 없습니다.  
  
 ON QUEUE [ _schema_name_**.** ] *queue_name*  
 이 서비스의 새 큐를 지정합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 이 서비스에 대한 모든 메시지를 현재 큐에서 새 큐로 이동합니다.  
  
 ADD CONTRACT *contract_name*  
 이 서비스에서 제공하는 계약 집합에 추가할 계약을 지정합니다.  
  
 DROP CONTRACT *contract_name*  
 이 서비스에서 제공하는 계약 집합에서 삭제할 계약을 지정합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 이 계약을 사용하는 이 서비스와의 기존 대화에 대해 오류 메시지를 보냅니다.  
  
## <a name="remarks"></a>설명  
 ALTER SERVICE 문이 서비스에서 계약을 삭제하면 이 서비스는 더 이상 해당 계약을 사용하는 대화의 대상이 될 수 없습니다. 따라서 [!INCLUDE[ssSB](../../includes/sssb-md.md)]는 해당 계약에 관한 새로운 대화를 이 서비스에 허용하지 않습니다. 계약을 사용하는 기존 대화는 영향을 받지 않습니다.  
  
 서비스에 대한 AUTHORIZATION을 변경하려면 ALTER AUTHORIZATION 문을 사용합니다.  
  
## <a name="permissions"></a>사용 권한  
 서비스 변경 권한은 기본적으로 서비스 소유자, **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할의 멤버 및 **sysadmin** 고정 서버 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-changing-the-queue-for-a-service"></a>A. 서비스 큐 변경  
 다음 예에서는 `//Adventure-Works.com/Expenses` 큐를 사용하도록 `NewQueue` 서비스를 변경합니다.  
  
```sql  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    ON QUEUE NewQueue ;  
```  
  
### <a name="b-adding-a-new-contract-to-the-service"></a>B. 서비스에 새 계약 추가  
 다음 예에서는 `//Adventure-Works.com/Expenses` 계약에 관한 대화를 허용하도록 `//Adventure-Works.com/Expenses` 서비스를 변경합니다.  
  
```sql  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
### <a name="c-adding-a-new-contract-to-the-service-dropping-existing-contract"></a>C. 서비스에 새 계약 추가 및 기존 계약 삭제  
 다음 예에서는 `//Adventure-Works.com/Expenses` 계약에 관한 대화를 허용하고 `//Adventure-Works.com/Expenses/ExpenseProcessing` 계약에 관한 대화를 허용하지 않도록 `//Adventure-Works.com/Expenses/ExpenseSubmission` 서비스를 변경합니다.  
  
```sql  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing],   
     DROP CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE SERVICE&#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [DROP SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
