---
description: GRANT 전체 텍스트 사용 권한(Transact-SQL)
title: GRANT 전체 텍스트 사용 권한(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], full-text
- full-text search [SQL Server], permissions
- full-text catalogs [SQL Server], permissions
- full-text stoplist [SQL Server], permissions
- GRANT statement, full-text permissions
ms.assetid: fdb64e09-222a-47fe-b08b-999264ca261d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d966e11f3bb545ec4ac71a412958fc36de6885ee
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91497751"
---
# <a name="grant-full-text-permissions-transact-sql"></a>GRANT 전체 텍스트 사용 권한(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  전체 텍스트 카탈로그 또는 전체 텍스트 중지 목록에 대한 사용 권한을 부여합니다.  
  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
GRANT permission [ ,...n ] ON  
    FULLTEXT   
        {  
           CATALOG :: full-text_catalog_name  
           |  
           STOPLIST :: full-text_stoplist_name  
        }  
    TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *permission*  
 사용 권한의 이름입니다. 보안 개체에 대한 사용 권한의 올바른 매핑에 대해서는 이 항목 뒷부분의 "주의" 섹션에 설명되어 있습니다.  
  
 ON FULLTEXT CATALOG **::**_full-text_catalog_name_  
 사용 권한을 부여할 전체 텍스트 카탈로그를 지정합니다. 범위 한정자 **::** 가 필요합니다.  
  
 ON FULLTEXT STOPLIST **::**_full-text_stoplist_name_  
 사용 권한을 부여할 전체 텍스트 중지 목록을 지정합니다. 범위 한정자 **::** 가 필요합니다.  
  
 *database_principal*  
 사용 권한을 부여할 보안 주체를 지정합니다. 다음 중 하나  
  
-   데이터베이스 사용자  
-   데이터베이스 역할  
-   애플리케이션 역할  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
-   인증서에 매핑된 데이터베이스 사용자  
-   비대칭 키에 매핑된 데이터베이스 사용자  
-   서버 보안 주체에 매핑되지 않은 데이터베이스 사용자  
  
GRANT OPTION  
 지정된 사용 권한을 다른 보안 주체에게 부여할 수 있는 권한도 이 보안 주체에 제공됨을 나타냅니다.  
  
AS *granting_principal*  
 이 쿼리를 실행하는 보안 주체가 사용 권한을 부여하는 권한을 부여할 수 있는 다른 보안 주체를 지정합니다. 다음 중 하나  
  
-   데이터베이스 사용자  
-   데이터베이스 역할  
-   애플리케이션 역할  
-   Windows 로그인에 매핑된 데이터베이스 사용자  
-   Windows 그룹에 매핑된 데이터베이스 사용자  
-   인증서에 매핑된 데이터베이스 사용자  
-   비대칭 키에 매핑된 데이터베이스 사용자  
-   서버 보안 주체에 매핑되지 않은 데이터베이스 사용자  
  
## <a name="remarks"></a>설명  
  
## <a name="fulltext-catalog-permissions"></a>FULLTEXT CATALOG 사용 권한  
 전체 텍스트 카탈로그는 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 다음 표에는 전체 텍스트 카탈로그에 대해 부여할 수 있는 가장 제한적인 특정 사용 권한이 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한과 함께 나열되어 있습니다.  
  
|전체 텍스트 카탈로그 사용 권한|전체 텍스트 카탈로그 사용 권한에 포함되는 사용 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|-----------------------------------|----------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="fulltext-stoplist-permissions"></a>FULLTEXT STOPLIST 사용 권한  
 전체 텍스트 중지 목록은 사용 권한 계층에서 부모 데이터베이스에 포함된 데이터베이스 수준 보안 개체입니다. 다음 표에는 전체 텍스트 중지 목록에 대해 부여할 수 있는 가장 제한적인 특정 사용 권한과, 의미상 이러한 사용 권한을 포함하는 보다 일반적인 사용 권한이 함께 나열되어 있습니다.  
  
|전체 텍스트 중지 목록 사용 권한|전체 텍스트 중지 목록 사용 권한에 포함되는 사용 권한|데이터베이스 사용 권한에 포함된 사용 권한|  
|------------------------------------|-----------------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>사용 권한  
 사용 권한을 부여한 사용자 또는 AS 옵션으로 지정한 보안 주체에게 GRANT OPTION을 통한 사용 권한이 있거나 부여할 사용 권한을 포함하는 상위 사용 권한이 있어야 합니다.  
  
 AS 옵션을 사용하는 경우 다음과 같은 추가 요구 사항이 적용됩니다.  
  
|AS *granting_principal*|필요한 추가 사용 권한|  
|------------------------------|------------------------------------|  
|데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|Windows 로그인에 매핑된 데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|Windows 그룹에 매핑된 데이터베이스 사용자|Windows 그룹의 멤버 자격, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|인증서에 매핑된 데이터베이스 사용자|db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|비대칭 키에 매핑된 데이터베이스 사용자|db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|서버 보안 주체에 매핑되지 않은 데이터베이스 사용자|사용자에 대한 IMPERSONATE 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|데이터베이스 역할|역할에 대한 ALTER 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
|애플리케이션 역할|역할에 대한 ALTER 사용 권한, db_securityadmin 고정 데이터베이스 역할의 멤버 자격, db_owner 고정 데이터베이스 역할의 멤버 자격 또는 sysadmin 고정 서버 역할의 멤버 자격|  
  
 개체 소유자는 소유하고 있는 개체에 대한 사용 권한을 부여할 수 있습니다. 보안 개체에 대한 CONTROL 사용 권한을 가진 보안 주체는 해당 보안 개체에 대한 사용 권한을 부여할 수 있습니다.  
  
 sysadmin 고정 서버 역할의 멤버와 같이 CONTROL SERVER 사용 권한이 부여된 사용자는 서버의 모든 보안 개체에 대한 사용 권한을 부여할 수 있습니다. db_owner 고정 데이터베이스 역할의 멤버와 같이 데이터베이스에 대한 CONTROL 사용 권한이 부여된 사용자는 데이터베이스의 모든 보안 개체에 대한 사용 권한을 부여할 수 있습니다. 스키마에 대한 CONTROL 권한이 부여된 사용자는 스키마 내의 모든 개체에 대한 사용 권한을 부여할 수 있습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-granting-permissions-to-a-full-text-catalog"></a>A. 전체 텍스트 카탈로그에 사용 권한 부여  
 다음 예에서는 `Ted`에게 전체 텍스트 카탈로그 `CONTROL`에 대한 `ProductCatalog` 사용 권한을 부여합니다.  
  
```sql  
GRANT CONTROL  
    ON FULLTEXT CATALOG :: ProductCatalog  
    TO Ted ;  
```  
  
### <a name="b-granting-permissions-to-a-stoplist"></a>B. 중지 목록에 대한 사용 권한 부여  
 다음 예에서는 `Mary`에게 전체 텍스트 중지 목록 `VIEW DEFINITION`에 대한 `ProductStoplist` 사용 권한을 부여합니다.  
  
```sql  
GRANT VIEW DEFINITION  
    ON FULLTEXT STOPLIST :: ProductStoplist  
    TO Mary ;  
```  
  
## <a name="see-also"></a>관련 항목  
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE FULLTEXT CATALOG&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CREATE FULLTEXT STOPLIST&#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [HAS_PERMS_BY_NAME&#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [사용 권한&#40;데이터베이스 엔진&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.fn_builtin_permissions&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [sys.fulltext_catalogs&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)  
  
  
