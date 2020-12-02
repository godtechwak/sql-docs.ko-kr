---
description: FULLTEXTCATALOGPROPERTY(Transact-SQL)
title: FULLTEXTCATALOGPROPERTY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FULLTEXTCATALOGPROPERTY_TSQL
- FULLTEXTCATALOGPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- full-text catalogs [SQL Server], properties
- FULLTEXTCATALOGPROPERTY function
- status information [SQL Server], full-text catalogs
ms.assetid: f841dc79-2044-4863-aff0-56b8bb61f250
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 83213da53228a39b3642f9563aecd5d365d02355
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91116050"
---
# <a name="fulltextcatalogproperty-transact-sql"></a>FULLTEXTCATALOGPROPERTY(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 전체 텍스트 카탈로그 속성에 대한 정보를 반환합니다.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
FULLTEXTCATALOGPROPERTY ('catalog_name' ,'property')  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
  
> [!NOTE]  
>  이후 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 **LogSize** 및 **PopulateStatus** 속성이 제거됩니다. 향후 개발 작업에서는 이 속성을 사용하지 않도록 하고 현재 이 속성을 사용하는 애플리케이션은 수정하십시오.  
  
_catalog\_name_  
전체 텍스트 카탈로그의 이름이 포함된 식입니다.  
  
_property_  
전체 텍스트 카탈로그 속성의 이름이 포함된 식입니다. 다음은 속성과 반환되는 정보에 대한 설명입니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**AccentSensitivity**|악센트 구분 설정입니다.<br /><br /> 0 = 악센트 구분 안 함<br /><br /> 1 = 악센트 구분|  
|**IndexSize**|전체 텍스트 카탈로그의 논리 크기(MB)입니다. 의미 키 구 및 문서 유사 인덱스의 크기를 포함합니다.<br /><br /> 자세한 내용은 이 항목의 뒷부분에 나오는 "주의"를 참조하십시오.|  
|**ItemCount**|카탈로그의 모든 전체 텍스트, 키 구 및 문서 유사성 인덱스를 포함하여 인덱싱된 항목의 수입니다.|  
|**LogSize**|이전 버전과의 호환성을 위해서만 지원됩니다. 항상 0을 반환합니다.<br /><br /> [!INCLUDE[msCoName](../../includes/msconame-md.md)] 검색 서비스 전체 텍스트 카탈로그와 연결된 오류 로그의 결합된 집합 크기(바이트)입니다.|  
|**MergeStatus**|마스터 병합의 진행 여부를 나타냅니다.<br /><br /> 0 = 마스터 병합이 진행되고 있지 않습니다.<br /><br /> 1 = 마스터 병합이 진행되고 있습니다.|  
|**PopulateCompletionAge**|마지막 전체 텍스트 인덱스 채우기가 완료된 시간과 01/01/1990 00:00:00 사이의 차이(초)입니다.<br /><br /> 전체 탐색 및 증분 탐색에 대해서만 업데이트됩니다. 채우기가 발생하지 않은 경우 0을 반환합니다.|  
|**PopulateStatus**|0 = 유휴 상태<br /><br /> 1 = 전체 채우기 진행 중<br /><br /> 2 = 일시 중지됨<br /><br /> 3 = 정체됨<br /><br /> 4 = 복구 중<br /><br /> 5 = 종료<br /><br /> 6 = 증분 채우기 진행 중<br /><br /> 7 = 인덱스 작성 중<br /><br /> 8 = 디스크가 꽉 참. 일시 중지됨<br /><br /> 9 = 변경 내용 추적 중|  
|**UniqueKeyCount**|전체 텍스트 카탈로그에서 고유 키 번호입니다.|  
|**ImportStatus**|전체 텍스트 카탈로그를 가져올 것인지 여부를 나타냅니다.<br /><br /> 0 = 전체 텍스트 카탈로그를 가져오지 않습니다.<br /><br /> 1 = 전체 텍스트 카탈로그를 가져옵니다.|  
  
## <a name="return-types"></a>반환 형식  
**int**  
  
## <a name="exceptions"></a>예외  
오류가 발생하거나 호출자에게 개체를 볼 수 있는 권한이 없으면 NULL을 반환합니다.  
  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 사용자는 보안 개체의 메타데이터만 볼 수 있습니다. 이 보안 개체는 사용자가 소유하거나 사용 권한을 부여받은 보안 개체입니다. 사용자가 개체에 대한 권한이 없으면 FULLTEXTCATALOGPROPERTY와 같은 메타데이터를 내보내는 기본 제공 함수가 NULL을 반환할 수 있습니다. 자세한 내용은 [sp_help_fulltext_catalogs&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)를 참조하세요.  
  
## <a name="remarks"></a>설명  
FULLTEXTCATALOGPROPERTY('_catalog\_name_','**IndexSize**')는 [sys.fulltext_index_fragments](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)와 같이 상태가 4또는 6인 조각만 찾습니다. 이러한 조각은 논리적 인덱스의 일부입니다. **IndexSize** 속성은 논리적 인덱스 크기만 반환합니다. 

그러나 인덱스를 병합하는 동안 실제 인덱스 크기는 논리적 크기의 두 배일 수 있습니다. 병합하는 동안 전체 텍스트 인덱스가 사용하는 실제 크기를 찾으려면 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) 시스템 저장 프로시저를 사용하십시오. 이 프로시저는 전체 텍스트 인덱스와 연결된 모든 조각을 찾습니다. 

전체 텍스트 채우기가 실패할 수 있습니다. 전체 텍스트 카탈로그 파일의 크기를 제한하고 병합 프로세스를 위한 충분한 공간을 허용하지 않으면 작업이 실패할 수 있습니다. 이 경우 FULLTEXTCATALOGPROPERTY('_catalog\_name_','**IndexSize**')가 0을 반환하고 전체 텍스트 로그에 다음 오류가 기록됩니다.  
  
`Error: 30059, Severity: 16, State: 1. A fatal error occurred during a full-text population and caused the population to be cancelled. Population type is: FULL; database name is FTS_Test (id: 13); catalog name is t1_cat (id: 5); table name t1 (id: 2105058535). Fix the errors that are logged in the full-text crawl log. Then, resume the population. The basic Transact-SQL syntax for this is: ALTER FULLTEXT INDEX ON table_name RESUME POPULATION.`  
  
**PopulateStatus** 속성이 유휴 상태가 되는지 검사하여 애플리케이션이 타이트 루프에서 대기하지 않도록 해야 합니다. 유휴 상태가 되면 채우기가 완료된 것입니다. 이 검사를 수행하면 데이터베이스와 전체 텍스트 검색 프로세스에서 CPU 주기가 제거되고 시간이 초과됩니다. 일반적으로 OBJECTPROPERTYEX 시스템 함수의 테이블 수준 **TableFullTextPopulateStatus** 에서 해당 **PopulateStatus** 속성을 확인하는 것이 더 좋습니다. OBJECTPROPERTYEX에서 이 전체 텍스트 속성과 기타 새 전체 텍스트 속성은 전체 텍스트 인덱싱 테이블에 대한 보다 자세한 정보를 제공합니다. 자세한 내용은 [OBJECTPROPERTYEX&#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)를 참조하세요.  
  
## <a name="examples"></a>예  
다음 예에서는 `Cat_Desc`라는 전체 텍스트 카탈로그에서 전체 텍스트 인덱싱된 항목의 수를 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT fulltextcatalogproperty('Cat_Desc', 'ItemCount');  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
[FULLTEXTSERVICEPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/fulltextserviceproperty-transact-sql.md)   
[메타데이터 함수&#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
[sp_help_fulltext_catalogs&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)  
  
  
