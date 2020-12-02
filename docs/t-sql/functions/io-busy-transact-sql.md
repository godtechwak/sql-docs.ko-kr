---
description: '&#x40;&#x40;IO_BUSY(Transact-SQL)'
title: '@@IO_BUSY(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@IO_BUSY'
- '@@IO_BUSY_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- ticks [SQL Server]
- I/O [SQL Server], time spent performing operations
- '@@IO_BUSY function'
- output operations [SQL Server]
- input operations [SQL Server]
- time [SQL Server], I/O operations
ms.assetid: 3c26770c-41ae-4e34-8c82-7bef920ffbca
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2b6aa8b3ccdc0dfb6584f6138059de6686326dca
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124665"
---
# <a name="x40x40io_busy-transact-sql"></a>&#x40;&#x40;IO_BUSY(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 마지막으로 시작한 이후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 입력 및 출력 작업에 소요된 시간을 반환합니다. 결과는 CPU 시간 단위("틱")로 표시되며 모든 CPU에 대해 누적됩니다. 따라서 실제 경과 시간을 초과할 수 있습니다. @@TIMETICKS를 곱하여 마이크로초로 변환합니다.  
  
> [!NOTE]  
>  @@CPU_BUSY 또는 @@IO_BUSY로 반환된 시간이 누적 CPU 시간의 약 49일을 초과할 경우 산술 오버플로 경고를 받게 됩니다. 이 경우 @@CPU_BUSY, @@IO_BUSY 및 @@IDLE 변수 값은 정확하지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
@@IO_BUSY  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 **integer**  
  
## <a name="remarks"></a>설명  
 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통계를 포함한 보고서를 표시하려면 sp_monitor를 실행합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 시작 시간과 현재 시간 사이에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 입/출력 작업을 수행한 시간을 밀리초 단위로 반환합니다. 값을 마이크로초로 변환할 때 산술 오버플로가 발생하지 않도록 값 중 하나를 **float** 데이터 형식으로 변환합니다.  
  
```sql  
SELECT @@IO_BUSY*@@TIMETICKS AS 'IO microseconds',   
   GETDATE() AS 'as of';  
```  
  
 일반적인 결과 집합은 다음과 같습니다.  
  
```  
  
IO microseconds as of                   
--------------- ----------------------  
4552312500      12/5/2006 10:23:00 AM   
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.dm_os_sys_info&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [@@CPU_BUSY&#40;Transact-SQL&#41;](../../t-sql/functions/cpu-busy-transact-sql.md)   
 [sp_monitor&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [시스템 통계 함수 &#40;Transact-SQL&#41;](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  
