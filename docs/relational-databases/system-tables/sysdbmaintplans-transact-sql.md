---
description: sysdbmaintplans(Transact-SQL)
title: sysdbmaintplans (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdbmaintplans_TSQL
- sysdbmaintplans
dev_langs:
- TSQL
helpviewer_keywords:
- sysdbmaintplans system table
ms.assetid: 0363296a-3082-48a9-9eb5-a1020b2f541a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 160abf3a360d18e3ba83df0f11cc9982984df049
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89517025"
---
# <a name="sysdbmaintplans-transact-sql"></a>sysdbmaintplans(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 테이블은 이전 버전의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 업그레이드된 인스턴스에 대한 기존 정보를 유지하기 위해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 포함됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 이 테이블의 내용을 변경하지 않습니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
 [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|데이터베이스 유지 관리 계획 ID입니다.|  
|**plan_name**|**sysname**|데이터베이스 유지 관리 계획 이름입니다.|  
|**date_created**|**datetime**|데이터베이스 유지 관리 계획을 만든 날짜입니다.|  
|**소유자도**|**sysname**|데이터베이스 유지 관리 계획의 소유자입니다.|  
|**max_history_rows**|**int**|시스템 테이블에 있는 데이터베이스 유지 관리 계획을 기록하는 데 사용하도록 지정된 최대 행 수입니다.|  
|**remote_history_server**|**sysname**|기록 보고서를 작성할 원격 서버의 이름입니다.|  
|**max_remote_history_rows**|**int**|기록 보고서를 작성할 수 있는 원격 서버의 시스템 테이블에서 지정된 최대 행 수입니다.|  
|**user_defined_1**|**int**|기본값은 NULL입니다.|  
|**user_defined_2**|**nvarchar (100)**|기본값은 NULL입니다.|  
|**user_defined_3**|**datetime**|기본값은 NULL입니다.|  
|**user_defined_4**|**uniqueidentifier**|기본값은 NULL입니다.|  
|**log_shipping**|**bit**|로그 전달 상태입니다.<br /><br /> **0** = 사용 안 함 **1** = 사용|  
  
  
