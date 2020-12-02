---
title: Oracle 게시자의 데이터 형식 매핑
description: SSMS(SQL Server Management Studio)를 사용하여 SQL Server에서 Oracle 게시자의 데이터 형식 매핑을 지정하는 방법을 설명합니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], data type mapping
- data types [SQL Server replication], Oracle publishing
- mapping data types [SQL Server replication]
ms.assetid: f172d631-3b8c-4912-bd0f-568366cd9870
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a58c4a27a90a36acc47c3338b39a802a2209060d
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130982"
---
# <a name="specify-data-type-mappings-for-an-oracle-publisher"></a>Oracle 게시자에 대한 데이터 형식 매핑 지정
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]의 Oracle 게시자에 대한 데이터 형식 매핑을 지정하는 방법에 대해 설명합니다. Oracle 게시자에 대해 기본 데이터 형식 매핑 집합이 제공되지만 특정 게시에 대해 다른 매핑을 지정해야 할 수 있습니다.  
  
 **항목 내용**  
  
-   **다음을 사용하여 Oracle게시자에 대한 데이터 형식 매핑을 지정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **아티클 속성 - \<Article>** 대화 상자의 **데이터 매핑** 탭에서 데이터 형식 매핑을 지정합니다. 이 옵션은 새 게시 마법사의 **아티클** 페이지 및 **게시 속성 - \<Publication>** 대화 상자에서 사용할 수 있습니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [Oracle 데이터베이스에서 게시 만들기](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md) 및 [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-specify-a-data-type-mapping"></a>데이터 형식 매핑을 지정하려면  
  
1.  새 게시 마법사의 **아티클** 페이지 또는 **게시 속성 - \<Publication>** 대화 상자에서 테이블을 선택한 다음 **아티클 속성** 을 클릭합니다.  
  
2.  **선택한 테이블 아티클 속성 설정** 을 클릭합니다.  
  
3.  **아티클 속성 - \<Article>** 대화 상자의 **데이터 매핑** 탭에서 **구독자 데이터 형식** 열의 매핑을 선택합니다.  
  
    -   하나의 매핑만 사용할 수 있는 데이터 형식의 경우 속성 표의 열이 읽기 전용입니다.  
  
    -   일부 형식의 경우 두 개 이상의 매핑을 선택할 수 있습니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 는 애플리케이션에 다른 매핑이 필요 하지 않는 한 기본 매핑을 사용할 것을 권장합니다. 자세한 내용은 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)을 참조하세요.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 사용자 지정 데이터 형식 매핑을 프로그래밍 방식으로 지정할 수 있습니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외의 DBMS(데이터베이스 관리 시스템) 간에 데이터 형식을 매핑할 때 사용되는 기본 매핑도 설정할 수 있습니다. 자세한 내용은 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)을 참조하세요.  
  
#### <a name="to-define-custom-data-type-mappings-when-creating-an-article-belonging-to-an-oracle-publication"></a>Oracle 게시에 속한 아티클을 작성할 때 사용자 지정 데이터 형식 매핑을 정의하려면  
  
1.  Oracle 게시가 아직 없는 경우 만듭니다.  
  
2.  배포자에서 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)을 실행합니다. **\@use_default_datatypes** 에 **0** 값을 지정합니다. 자세한 내용은 [아티클을 정의](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
3.  배포자에서 [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) 를 실행하여 게시된 아티클의 열에 대한 기존 매핑을 확인합니다.  
  
4.  배포자에서 [sp_changearticlecolumndatatype](../../../relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql.md)을 실행합니다. **\@publisher** 에 Oracle 게시자의 이름을 지정하고 **\@publication**, **\@article** 및 **\@column** 을 지정하여 게시된 열을 정의합니다. **\@type** 에 매핑할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식의 이름을 지정하고 해당되는 경우 **\@length**, **\@precision** 및 **\@scale** 을 지정합니다.  
  
5.  배포자에서 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)를 실행합니다. 이렇게 하면 Oracle 게시에서 스냅샷을 생성하는 데 사용되는 뷰가 만들어집니다.  
  
#### <a name="to-specify-a-mapping-as-the-default-mapping-for-a-data-type"></a>매핑을 데이터 형식에 대한 기본 매핑으로 지정하려면  
  
1.  (옵션) 데이터베이스의 배포자에서 [sp_getdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md)을 실행합니다. **\@source_dbms**, **\@source_type**, **\@destination_dbms**, **\@destination_version** 을 지정하고 원본 DBMS를 식별하는 데 필요한 기타 매개 변수를 지정합니다. 대상 DBMS의 현재 매핑된 데이터 형식에 대한 정보는 출력 매개 변수를 사용하여 반환됩니다.  
  
2.  (옵션) 데이터베이스의 배포자에서 [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)을 실행합니다. **\@source_dbms** 를 지정하고 결과 집합을 필터링하는 데 필요한 기타 매개 변수를 지정합니다. 결과 집합에서 원하는 매핑에 대한 **mapping_id** 의 값을 확인합니다.  
  
3.  데이터베이스의 배포자에서 [sp_setdefaultdatatypemapping](../../../relational-databases/system-stored-procedures/sp-setdefaultdatatypemapping-transact-sql.md)을 실행합니다.  
  
    -   2단계에서 얻은 **mapping_id** 의 원하는 값을 아는 경우 **\@mapping_id** 에 이 값을 지정합니다.  
  
    -   **mapping_id** 를 모르는 경우 **\@source_dbms**, **\@source_type**, **\@destination_dbms**, **\@destination_type** 매개 변수 및 기존 매핑을 식별하는 데 필요한 기타 매개 변수를 지정합니다.  
  
#### <a name="to-find-valid-data-types-for-a-given-oracle-data-type"></a>지정된 Oracle 데이터 형식에 대한 유효한 데이터 형식을 찾으려면  
  
1.  데이터베이스의 배포자에서 [sp_helpdatatypemap](../../../relational-databases/system-stored-procedures/sp-helpdatatypemap-transact-sql.md)을 실행합니다. **\@source_dbms** 의 값을 **ORACLE** 로 지정하고 결과 집합을 필터링하는 데 필요한 기타 매개 변수를 지정합니다.  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 열을 Oracle 데이터 형식 NUMBER로 변경하여 기본 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 형식 대신 **ssNoVersion** 숫자 데이터 형식 **float** 의 Oracle 게시자에 대한 데이터 형식 매핑을 지정하는 방법에 대해 설명합니다.  
  
 [!code-sql[HowTo#sp_changecolumndatatype](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_1.sql)]  
  
 다음 쿼리 예에서는 Oracle 9 데이터 형식 **CHAR** 에 대한 기본 및 대체 매핑을 반환합니다.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_char](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_2.sql)]  
  
 다음 쿼리 예에서는 소수 자릿수 또는 전체 자릿수 없이 지정된 경우 Oracle 9 데이터 형식 **NUMBER** 에 대한 기본 매핑을 반환합니다.  
  
 [!code-sql[HowTo#sp_helpcolumndatatype_number](../../../relational-databases/replication/codesnippet/tsql/specify-data-type-mappin_3.sql)]  
  
## <a name="see-also"></a>참고 항목  
 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [다른 유형의 데이터베이스 복제](../../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Oracle 게시자 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)  
  
  
