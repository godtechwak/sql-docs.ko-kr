---
description: cdc.index_columns(Transact-SQL)
title: cdc. index_columns (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.index_columns_TSQL
- cdc.index_columns
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.index_columns
ms.assetid: 256ec8a5-3031-40a8-9fdb-99db42ea453d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5cf09c3a66a3db1b7275dfe8017d953aaf57b42d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544645"
---
# <a name="cdcindex_columns-transact-sql"></a>cdc.index_columns(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  변경 테이블과 관련된 각 인덱스 열에 대해 하나의 행을 반환합니다. 인덱스 열은 변경 데이터 캡처에서 원본 테이블의 행을 고유하게 식별하는 데 사용됩니다. 기본적으로 원본 테이블의 기본 키 열이 포함되지만 원본 테이블에서 변경 데이터 캡처가 사용되는 경우 원본 테이블에 고유한 인덱스가 지정되어 있으면 해당 인덱스의 열이 대신 사용됩니다. 순 변경 추적이 설정된 경우에는 원본 테이블에 기본 키 또는 고유 인덱스가 있어야 합니다. 자세한 내용은 [sp_cdc_enable_table &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)을 참조 하십시오.  
  
 시스템 테이블은 직접 쿼리하지 않는 것이 좋습니다. 대신, [sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) 저장 프로시저를 실행 합니다.  

  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|변경 테이블의 ID입니다.|  
|**column_name**|**sysname**|인덱스 열의 이름입니다.|  
|**index_ordinal**|**tinyint**|인덱스 내에 있는 열의 서수(1부터 시작)입니다.|  
|**column_id**|**int**|원본 테이블에 있는 열의 ID입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [change_tables &#40;Transact-sql&#41;](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md)  
  
  
