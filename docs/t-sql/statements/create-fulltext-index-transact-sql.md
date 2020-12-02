---
description: CREATE FULLTEXT INDEX(Transact-SQL)
title: CREATE FULLTEXT INDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FULLTEXT_INDEX_TSQL
- CREATE_FULLTEXT_INDEX_TSQL
- CREATE FULLTEXT INDEX
- FULLTEXT INDEX
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], creating
- index creation [SQL Server], CREATE FULLTEXT INDEX statement
- CREATE FULLTEXT INDEX statement
ms.assetid: 8b80390f-5f8b-4e66-9bcc-cabd653c19fd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: eac401156014952142c39851b1e703605997c245
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128003"
---
# <a name="create-fulltext-index-transact-sql"></a>CREATE FULLTEXT INDEX(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스의 테이블 또는 인덱싱된 뷰에서 전체 텍스트 인덱스를 만듭니다. 테이블 또는 인덱싱된 뷰당 하나의 전체 텍스트 인덱스만 허용되고 각 전체 텍스트 인덱스는 하나의 테이블 또는 인덱싱된 뷰에 적용됩니다. 전체 텍스트 인덱스는 최대 1024개의 열을 포함할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
CREATE FULLTEXT INDEX ON table_name  
   [ ( { column_name   
             [ TYPE COLUMN type_column_name ]  
             [ LANGUAGE language_term ]   
             [ STATISTICAL_SEMANTICS ]  
        } [ ,...n]   
      ) ]  
    KEY INDEX index_name   
    [ ON <catalog_filegroup_option> ]  
    [ WITH [ ( ] <with_option> [ ,...n] [ ) ] ]  
[;]  
  
<catalog_filegroup_option>::=  
 {  
    fulltext_catalog_name   
 | ( fulltext_catalog_name, FILEGROUP filegroup_name )  
 | ( FILEGROUP filegroup_name, fulltext_catalog_name )  
 | ( FILEGROUP filegroup_name )  
 }  
  
<with_option>::=  
 {  
   CHANGE_TRACKING [ = ] { MANUAL | AUTO | OFF [, NO POPULATION ] }   
 | STOPLIST [ = ] { OFF | SYSTEM | stoplist_name }  
 | SEARCH PROPERTY LIST [ = ] property_list_name   
 }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*table_name*       
전체 텍스트 인덱스에 있는 열을 포함하는 테이블 또는 인덱싱된 뷰의 이름입니다.  
  
*column_name*       
전체 텍스트 인덱스에 포함된 열의 이름입니다. **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml** 및 **varbinary(max)** 타입의 열만 전체 텍스트 검색을 위해 인덱싱될 수 있습니다. 여러 열을 지정하려면 다음과 같이 *column_name* 절을 반복합니다.  
  
CREATE FULLTEXT INDEX ON *table_name* (*column_name1* [...], *column_name2* [...]) ...  
  
TYPE COLUMN *type_column_name*       
**varbinary(max)** 또는 **image** 문서에 대한 문서 종류를 보유하는 데 사용하는 테이블 열 *type_column_name* 의 이름을 지정합니다. 유형 열이라고 하는 이 열에는 사용자 제공 파일 확장명(.doc, .pdf, .xls 등)이 포함됩니다. 형식 열은 **char**, **nchar**, **varchar** 또는 **nvarchar** 형식이어야 합니다.  
  
형식 열 *type_column_name* 은 *column_name* 이 **varbinary(max)** 또는 **image** 열을 지정하여 데이터가 이진 데이터로 저장되는 경우에만 지정합니다. 그렇지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류가 반환됩니다.  
  
> [!NOTE]  
> 인덱싱할 때 전체 텍스트 엔진은 각 테이블 행의 유형 열에 있는 약어를 사용하여 *column_name* 의 문서에 사용할 전체 텍스트 검색 필터를 식별합니다. 이 필터는 문서를 이진 스트림으로 로드하고 서식 정보를 제거하며 문서의 텍스트를 단어 분리기 구성 요소로 보냅니다. 자세한 내용은 [고급 분석 확장 구성 및 관리](../../relational-databases/search/configure-and-manage-filters-for-search.md)를 참조하세요.  
  
LANGUAGE *language_term*       
*column_name* 에 저장된 데이터의 언어입니다.  
  
*language_term* 은 선택적이며 언어의 LCID(로캘 ID)에 해당하는 문자열, 정수 또는 16진수 값으로 지정할 수 있습니다. 값을 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 기본 언어가 사용됩니다.  
  
*language_term* 이 지정되면 언어가 **char**, **nchar**, **varchar**, **nvarchar**, **text** 및 **ntext** 에 저장된 인덱스 데이터에 사용될 것입니다. 이 언어는 열에 대한 전체 텍스트 조건자의 일부로 *language_term* 을 지정하지 않을 경우 쿼리할 때 기본 언어로 사용됩니다.  
  
문자열로 지정하는 경우 *language_term* 은 syslanguages 시스템 테이블의 별칭 열 값에 해당합니다. 문자열은 **‘** _language\_term_ **’** 과 같이 작은따옴표로 묶어야 합니다. 정수로 지정하는 경우 *language_term* 은 언어를 식별하는 실제 LCID입니다. 16진수 값으로 지정하는 경우 *language_term* 은 0x로 시작하는 16진수 LCID 값입니다. 16진수 값은 선행 0을 포함하여 8자리 수를 초과할 수 없습니다.  
  
값이 DBCS(더블바이트 문자 집합) 형식인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 값을 유니코드로 변환합니다.  
  
단어 분리기 및 형태소 분석기와 같은 리소스는 *language_term* 으로 지정된 언어에 사용해야 합니다. 이러한 리소스가 지정된 언어를 지원하지 않는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 오류를 반환합니다.  
  
sp_configure 저장 프로시저를 사용하여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 기본 전체 텍스트 언어에 대한 정보에 액세스할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)백업 및 복원의 기본적인 백업 미디어 관련 용어를 소개합니다.  
  
BLOB이 아닌 열과 XML이 아닌 열에 여러 언어로 된 텍스트 데이터가 포함되어 있거나 열에 저장된 텍스트의 언어를 알 수 없는 경우 중립(0x0) 언어 리소스를 사용하는 것이 적합할 수 있습니다. 그러나 중립(0x0) 언어 리소스를 사용할 때 발생할 수 있는 결과를 먼저 이해해야 합니다. 중립(0x0) 언어 리소스를 사용할 경우의 결과 및 가능한 해결 방법에 대한 내용은 [전체 텍스트 색인 생성시 언어 선택](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md)을 참조하세요.  
  
XML 유형 또는 BLOB 유형의 열로 저장된 문서의 경우 인덱싱 시에 문서 내의 언어 인코딩이 사용됩니다. 예를 들어 XML 열에서는 XML 문서의 **xml:lang** 특성으로 언어를 식별합니다. 쿼리할 때 *language_term* 이 전체 텍스트 쿼리의 일부로 지정되지 않은 경우에는 *language_term* 에 지정된 이전 값이 전체 텍스트 쿼리의 기본 언어로 사용됩니다.  
  
STATISTICAL_SEMANTICS       
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상). 
  
통계 의미 체계 인덱싱의 일부인 추가 키 구 및 문서 유사성 인덱스를 만듭니다. 자세한 내용은 [의미 체계 검색&#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md)을 참조하세요.  
  
KEY INDEX *index_name*       
*table_name* 에서 고유 키 인덱스의 이름입니다. KEY INDEX는 고유하며 Null을 허용하지 않는 단일 키 열이어야 합니다. 전체 텍스트 고유 키에 대해 가장 작은 고유 키 인덱스를 선택합니다.  최상의 성능을 위해 전체 텍스트 키에 정수 데이터 형식을 사용하는 것이 좋습니다.  
  
*fulltext_catalog_name*       
전체 텍스트 인덱스에 사용되는 전체 텍스트 카탈로그입니다. 카탈로그는 데이터베이스에 이미 있어야 합니다. 이 절은 옵션입니다. 지정하지 않으면 기본 카탈로그가 사용됩니다. 기본 카탈로그가 없으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 오류를 반환합니다.  
  
FILEGROUP *filegroup_name*       
주어진 파일 그룹에 지정된 전체 텍스트 인덱스를 만듭니다. 파일 그룹은 이미 존재해야 합니다. FILEGROUP 절을 지정하지 않으면 전체 텍스트 인덱스가 기본 테이블 또는 뷰와 같은 파일 그룹(분할되지 않은 테이블의 경우)에 배치되거나 주 파일 그룹(분할된 테이블의 경우)에 배치됩니다.  
  
 CHANGE_TRACKING [ = ] { MANUAL | **AUTO** | OFF [ , NO POPULATION ] }       
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 전체 텍스트 인덱스가 적용되는 테이블 열의 변경 내용(업데이트, 삭제 또는 삽입)을 해당 전체 텍스트 인덱스로 전파할지 여부를 지정합니다. WRITETEXT 및 UPDATETEXT를 통한 데이터 변경 내용은 전체 텍스트 인덱스에 반영되지 않고 변경 내용 추적 시 선택되지도 않습니다.  
  
MANUAL       
다음을 호출하면 추적된 변경 내용이 수동으로 전파되도록 지정합니다. ALTER FULLTEXT INDEX ... START UPDATE POPULATION [!INCLUDE[tsql](../../includes/tsql-md.md)] 문(*수동 채우기*). [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 사용하여 이 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 주기적으로 호출할 수 있습니다.  
  
**AUTO**       
기본 테이블에서 데이터가 수정되면 추적된 변경 내용이 자동으로 전파되도록 지정합니다(*자동 채우기*). 변경 내용은 자동으로 전파되지만 전체 텍스트 인덱스에 즉시 반영되지 않을 수 있습니다. 기본값은 AUTO입니다.  
  
OFF [ `,` NO POPULATION]       
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 인덱싱된 데이터의 변경 내용 목록을 유지하지 않도록 지정합니다. NO POPULATION을 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 생성된 인덱스를 완전히 채웁니다.  
  
NO POPULATION 옵션은 CHANGE_TRACKING이 OFF일 경우에만 사용할 수 있습니다. NO POPULATION을 지정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 인덱스를 만든 후 인덱스를 채우지 않습니다. 사용자가 ALTER FULLTEXT INDEX 명령에 START FULL POPULATION 또는 START INCREMENTAL POPULATION 절을 실행한 후에만 인덱스가 채워집니다.  
  
STOPLIST [ = ] { OFF | **SYSTEM** | *stoplist_name* }       
전체 텍스트 중지 목록을 인덱스와 연결합니다. 이 인덱스는 지정된 중지 목록에 속한 토큰으로 채워지지 않습니다. STOPLIST를 지정하지 않으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]이 시스템 전체 텍스트 중지 목록을 인덱스와 연결합니다.  
  
OFF       
중지 목록을 전체 텍스트 인덱스와 연결하지 않도록 지정합니다.  
  
**SYSTEM**       
기본 전체 텍스트 시스템 STOPLIST가 이 전체 텍스트 인덱스에 사용되도록 지정합니다.  
  
*stoplist_name*       
전체 텍스트 인덱스와 연결할 중지 목록의 이름을 지정합니다.  
  
SEARCH PROPERTY LIST [ = ] *property_list_name*       
**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 이상).  
  
검색 속성 목록을 인덱스와 연결합니다.  
 
OFF       
속성 목록을 전체 텍스트 인덱스와 연결하지 않도록 지정합니다.  
  
*property_list_name*       
전체 텍스트 인덱스와 연결할 검색 속성 목록의 이름을 지정합니다.  
  
## <a name="remarks"></a>설명  
전체 텍스트 인덱스에 대한 자세한 내용은 [전체 텍스트 인덱스 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-indexes.md)를 참조하세요.  
  
**xml** 열에서는 XML 요소의 내용을 인덱싱하지만 XML 태그를 무시하는 전체 텍스트 인덱스를 만들 수 있습니다. 특성 값은 숫자 값이 아니면 전체 텍스트 인덱싱됩니다. 요소 태그는 토큰 경계로 사용됩니다. 여러 언어를 포함하는 올바른 형식의 XML 또는 HTML 문서와 조각이 지원됩니다. 자세한 내용은 [XML 열에 전체 텍스트 검색 사용](../../relational-databases/xml/use-full-text-search-with-xml-columns.md)을 참조하세요.  
  
인덱스 키 열에는 정수 데이터 형식을 사용하는 것이 좋습니다. 이렇게 하면 쿼리 실행 시간이 최적화됩니다.  
  
## <a name="interactions-of-change-tracking-and-no-population-parameter"></a>변경 내용 추적과 NO POPULATION 매개 변수 간의 상호 작용  
 전체 텍스트 인덱스가 채워지는지 여부는 변경 내용 추적이 설정되어 있는지 여부와 ALTER FULLTEXT INDEX 문에 WITH NO POPULATION이 지정되어 있는지 여부에 따라 달라집니다. 다음 표에서는 이러한 상호 작용의 결과를 요약합니다.  
  
|변경 내용 추적|WITH NO POPULATION|결과|  
|---------------------|------------------------|------------|  
|설정 안 됨|지정되지 않음|인덱스에 대해 전체 채우기가 수행됩니다.|  
|설정 안 됨|지정됨|ALTER FULLTEXT INDEX...START POPULATION 문이 실행될 때까지 인덱스 채우기가 발생하지 않습니다.|  
|사용|지정됨|오류가 발생하고 인덱스가 변경되지 않습니다.|  
|사용|지정되지 않음|인덱스에 대해 전체 채우기가 수행됩니다.|  
  
 전체 텍스트 인덱스에 대한 자세한 내용은 [전체 텍스트 인덱스 채우기](../../relational-databases/search/populate-full-text-indexes.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 전체 텍스트 카탈로그에 대한 `REFERENCES` 권한과 테이블 뷰 또는 인덱싱된 뷰에 대한 `ALTER` 권한을 가지거나 `sysadmin` 고정 서버 역할, `db_owner` 또는 `db_ddladmin` 고정 데이터베이스 역할의 구성원이어야 합니다.  
  
`SET STOPLIST`를 지정한 경우 사용자가 지정된 중지 목록에 대한 REFERENCES 권한이 있어야 합니다. 이 사용 권한은 STOPLIST 소유자가 부여할 수 있습니다.  
  
> [!NOTE]  
> public에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 기본 중지 목록에 대한 REFERENCE 권한이 부여됩니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-creating-a-unique-index-a-full-text-catalog-and-a-full-text-index"></a>A. 고유 인덱스, 전체 텍스트 카탈로그 및 전체 텍스트 인덱스 만들기  
 다음 예에서는 `JobCandidateID` 예제 데이터베이스의 `HumanResources.JobCandidate` 테이블에 있는 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 열에 대해 고유 인덱스를 만듭니다. 그런 다음 기본 전체 텍스트 카탈로그 `ft`를 만듭니다. 마지막으로 `Resume` 카탈로그 및 시스템 중지 목록을 사용하여 `ft` 열에 대한 전체 텍스트 인덱스를 만듭니다.  
  
```sql  
CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
CREATE FULLTEXT CATALOG ft AS DEFAULT;  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
   KEY INDEX ui_ukJobCand   
   WITH STOPLIST = SYSTEM;  
GO  
```  
  
### <a name="b-creating-a-full-text-index-on-several-table-columns"></a>B. 여러 테이블 열에 대한 전체 텍스트 인덱스 만들기  
 다음 예에서는 `production_catalog` 예제 데이터베이스에 전체 텍스트 카탈로그 `AdventureWorks`를 만듭니다. 그런 다음 이 새 카탈로그를 사용하는 전체 텍스트 인덱스를 만듭니다. 전체 텍스트 인덱스는 `ReviewerName`의 `EmailAddress`, `Comments` 및 `Production.ProductReview` 열에 있습니다. 이 예에서는 각 열에 대해 해당 열의 데이터 언어인 영어 LCID `1033`을 지정합니다. 이 전체 텍스트 인덱스는 기존의 고유 키 인덱스인 `PK_ProductReview_ProductReviewID`를 사용합니다. 권장한 대로 이 인덱스 키는 정수 열 `ProductReviewID`에 있습니다.  
  
```sql  
CREATE FULLTEXT CATALOG production_catalog;  
GO  
CREATE FULLTEXT INDEX ON Production.ProductReview  
 (   
  ReviewerName  
     Language 1033,  
  EmailAddress  
     Language 1033,  
  Comments   
     Language 1033       
 )   
  KEY INDEX PK_ProductReview_ProductReviewID   
      ON production_catalog;   
GO  
```  
  
### <a name="c-creating-a-full-text-index-with-a-search-property-list-without-populating-it"></a>C. 채우지 않고 검색 속성 목록을 사용하여 전체 텍스트 인덱스 만들기  
 다음 예에서는 `Title` 테이블의 `DocumentSummary`, `Document` 및 `Production.Document` 열에서 전체 텍스트 인덱스를 만듭니다. 이 예에서는 열의 데이터 언어인 영어 LCID `1033`을 지정합니다. 이 전체 텍스트 인덱스는 기본 전체 텍스트 카탈로그 및 기존의 고유 키 인덱스 `PK_Document_DocumentID`를 사용합니다. 권장한 대로 이 인덱스 키는 정수 열 `DocumentID`에 있습니다.  
  
 이 예에서는 SYSTEM 중지 목록을 지정합니다. 또한 검색 속성 목록 `DocumentPropertyList`를 지정합니다. 이 검색 속성 목록을 만드는 예는 [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md)을 참조하십시오.  
  
 이 예에서는 채우기 작업을 수행하지 않고 변경 내용 추적이 해제되도록 지정하며 나중에 사용률이 낮은 시간에 ALTER FULLTEXT INDEX 문을 사용하여 새 인덱스에 대해 전체 채우기를 시작하고 변경 내용 자동 추적을 사용하도록 설정합니다.  
  
```sql  
CREATE FULLTEXT INDEX ON Production.Document  
  (   
  Title  
      Language 1033,   
  DocumentSummary  
      Language 1033,   
  Document   
      TYPE COLUMN FileExtension  
      Language 1033   
  )  
  KEY INDEX PK_Document_DocumentID  
          WITH STOPLIST = SYSTEM, SEARCH PROPERTY LIST = DocumentPropertyList, CHANGE_TRACKING OFF, NO POPULATION;  
   GO  
```  
  
 다음과 같이 나중에 사용률이 낮은 시간에 인덱스가 채워집니다.  
  
```sql  
ALTER FULLTEXT INDEX ON Production.Document SET CHANGE_TRACKING AUTO;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
[전체 텍스트 인덱스 만들기 및 관리](../../relational-databases/search/create-and-manage-full-text-indexes.md)       
[ALTER FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)       
[DROP FULLTEXT INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)       
[전체 텍스트 검색](../../relational-databases/search/full-text-search.md)       
[GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)       
[sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)       
[검색 속성 목록을 사용하여 문서 속성 검색](../../relational-databases/search/search-document-properties-with-search-property-lists.md)       
  
  
