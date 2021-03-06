---
description: sys.xml_schema_elements(Transact-SQL)
title: sys.xml_schema_elements (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_elements
- sys.xml_schema_elements_TSQL
- xml_schema_elements
- xml_schema_elements_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_elements catalog view
ms.assetid: 190ed0cd-0c5e-4607-9db4-9e77cacf17d7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 008fb9d5d8beb5f746d02be3357eb1e73ae58ea9
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543974"
---
# <a name="sysxml_schema_elements-transact-sql"></a>sys.xml_schema_elements(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Symbol_space** **E**의 형식인 XML 스키마 구성 요소별 행을 반환 합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|**--**|[sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md)에서 열을 상속 합니다.|  
|**is_default_fixed**|**bit**|1 = 기본값이 고정 값입니다. XML 인스턴스에서 이 값을 무시할 수 없습니다.<br /><br /> 0 = 기본값이 요소에 대해 고정 값이 않습니다(기본값).|  
|**is_abstract**|**bit**|1 = 요소가 추상적이며 인스턴스 문서에서 사용할 수 없습니다. 인스턴스 문서에 요소의 대체 그룹 멤버가 나타나야 합니다.<br /><br /> 0 = 요소가 추상적이지 않습니다(기본값).|  
|**is_nillable**|**bit**|1 = 요소가 nillable입니다.<br /><br /> 0 = 요소가 nillable이 (기본값)|  
|**must_be_qualified**|**bit**|1 = 요소가 명시적으로 정규화된 네임스페이스여야 합니다.<br /><br /> 0 = 요소가 암시적으로 정규화된 네임스페이스여야 (기본값)|  
|**is_extension_blocked**|**bit**|1 = 확장 유형 인스턴스로의 대체가 차단됩니다.<br /><br /> 0 = 확장 유형으로의 대체가 (기본값)|  
|**is_restriction_blocked**|**bit**|1 = 제한 유형 인스턴스로의 대체가 차단됩니다.<br /><br /> 0 = 제한 유형으로의 대체가 (기본값)|  
|**is_substitution_blocked**|**bit**|1 = 대체 그룹 인스턴스를 사용할 수 없습니다.<br /><br /> 0 = 대체 그룹으로의 대체가 (기본값)|  
|**is_final_extension**|**bit**|1 = 확장 유형 인스턴스로의 대체가 허용되지 않습니다.<br /><br /> 0 = 확장 유형 인스턴스에서 대체가 (기본값)|  
|**is_final_restriction**|**bit**|1 = 제한 유형 인스턴스로의 대체가 허용되지 않습니다.<br /><br /> 0 = 제한 유형 인스턴스에서 대체가 (기본값)|  
|**default_value**|**nvarchar (4000)**|요소의 기본값입니다. 기본값을 제공하지 않으면 NULL입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Xml 스키마 &#40;XML 형식 시스템&#41; 카탈로그 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
