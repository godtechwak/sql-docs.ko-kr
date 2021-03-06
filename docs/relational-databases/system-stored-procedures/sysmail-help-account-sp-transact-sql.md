---
description: sysmail_help_account_sp(Transact-SQL)
title: sysmail_help_account_sp (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_account_sp_TSQL
- sysmail_help_account_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_account_sp
ms.assetid: 87c7c39c-8e05-4e68-9272-45f908809c3b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 711b0d317b600b455fc4d3d0d80e17e1a9ddf7c3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541059"
---
# <a name="sysmail_help_account_sp-transact-sql"></a>sysmail_help_account_sp(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  암호를 제외하고 데이터베이스 메일 계정에 대한 정보를 나열합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sysmail_help_account_sp [ [ @account_id = ] account_id | [ @account_name = ] 'account_name' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @account_id = ] account_id` 정보를 나열할 계정의 계정 ID입니다. *account_id* 은 **int**이며 기본값은 NULL입니다.  
  
`[ @account_name = ] 'account_name'` 정보를 나열할 계정의 이름입니다. *account_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 아래에 나열된 열을 포함한 결과 집합을 반환합니다.  
  
| 열 이름 | 데이터 형식 | Description |
| ----------- | --------- | ----------- |
|**account_id**|**int**|계정의 ID입니다.|  
|**name**|**sysname**|계정 이름입니다.|  
|**description**|**nvarchar(256)**|계정에 대한 설명입니다.|  
|**email_address**|**nvarchar(128)**|메시지를 보내는 전자 메일 주소입니다.|  
|**display_name**|**nvarchar(128)**|계정의 표시 이름입니다.|  
|**replyto_address**|**nvarchar(128)**|이 계정에서 보낸 메시지에 회신하는 주소입니다.|  
|**servertype**|**sysname**|계정에 대한 전자 메일 서버의 유형입니다.|  
|**서버**|**sysname**|계정에 대한 전자 메일 서버의 이름입니다.|  
|**port**|**int**|사용되는 전자 메일 서버의 포트 번호입니다.|  
|**이름**|**nvarchar(128)**|전자 메일 서버에서 인증을 사용하는 경우 전자 메일 서버 로그인에 사용할 사용자 이름입니다. **Username** 이 NULL 인 경우 데이터베이스 메일는이 계정에 대 한 인증을 사용 하지 않습니다.|  
|**use_default_credentials**|**bit**|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 자격 증명을 사용하여 메일을 SMTP 서버로 보낼지 여부를 지정합니다. **use_default_credentials** 은 bit 이며 기본값은 없습니다. 이 매개 변수가 1이면 데이터베이스 메일에서는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 서비스의 자격 증명을 사용합니다. 이 매개 변수가 0 이면 데이터베이스 메일는 SMTP 서버의 인증에 ** \@ 사용자 이름과** ** \@ 암호** 를 사용 합니다. ** \@ 사용자 이름** 및 ** \@ 암호가** NULL 이면 데이터베이스 메일 익명 인증을 사용 합니다. 이 매개 변수를 지정하기 전에 해당 SMTP 관리자에게 문의하십시오.|  
|**enable_ssl**|**bit**|데이터베이스 메일 TLS (Transport Layer Security)를 사용 하 여 통신을 암호화할지 여부를 지정 합니다 (이전에는 SSL (SSL(Secure Sockets Layer))). SMTP 서버에 TLS가 필요한 경우이 옵션을 사용 합니다. **enable_ssl** 은 bit 이며 기본값은 없습니다. 1은 TLS를 사용 하는 데이터베이스 메일 통신을 암호화 합니다. 0은 TLS 암호화 없이 메일을 전송 데이터베이스 메일 나타냅니다.|  
  
## <a name="remarks"></a>설명  
 *Account_id* 또는 *account_name* 를 제공 하지 않으면 Microsoft SQL Server 인스턴스의 모든 데이터베이스 메일 계정에 대 한 정보가 **sysmail_help_account** 나열 됩니다.  
  
 **Sysmail_help_account_sp** 저장 프로시저는 **msdb** 데이터베이스에 있으며 **dbo** 스키마가 소유 합니다. 현재 데이터베이스가 **msdb**가 아닌 경우 세 부분으로 된 이름을 사용 하 여 프로시저를 실행 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저에 대 한 실행 권한은 기본적으로 **sysadmin** 고정 서버 역할의 멤버로 사용 됩니다.  
  
## <a name="examples"></a>예제  
 **1. 모든 계정에 대한 정보 나열**  
  
 다음 예에서는 인스턴스의 모든 계정에 대한 계정 정보를 나열합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp ;  
```  
  
 다음은 줄 길이에 맞추어 편집된 결과 집합 예입니다.  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- --------------------------------------- ------------------------- -------------------------------- --------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
149         Audit Account                Account for audit e-mail.               audit@Adventure-Works.com Automated Mailer (Audit)         NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
```  
  
 **2. 특정 계정에 대한 정보 나열**  
  
 다음 예에서는 `AdventureWorks Administrator`라는 계정에 대해 계정 정보를 나열합니다.  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp  
    @account_name = 'AdventureWorks Administrator' ;  
```  
  
 다음은 줄 길이에 맞추어 편집된 결과 집합 예입니다.  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- ------------------------------------------------------ ------------------------- ---------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL     0                       0       
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 메일](../../relational-databases/database-mail/database-mail.md)   
 [데이터베이스 메일 계정 만들기](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [Transact-sql&#41;&#40;저장 프로시저 데이터베이스 메일 ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
