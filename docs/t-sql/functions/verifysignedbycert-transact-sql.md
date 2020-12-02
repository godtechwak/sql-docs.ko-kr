---
description: VERIFYSIGNEDBYCERT(Transact-SQL)
title: VERIFYSIGNEDBYCERT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- VERIFYSIGNEDBYCERT
- VERIFYSIGNEDBYCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- digitally signed data for changes [SQL Server]
- verifying digitally signed data for changes
- testing digitally signed data for changes
- checking digitally signed data for changes
- VERIFYSIGNEDBYCERT
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 4e041f33-60c4-4190-91c7-220d51dd6c8f
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2524b2e828615ee1e413f36bd77cd8ebc3fa8b77
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91380563"
---
# <a name="verifysignedbycert-transact-sql"></a>VERIFYSIGNEDBYCERT(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  디지털 서명된 데이터가 서명된 후 변경되었는지 여부를 테스트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
VerifySignedByCert( Cert_ID , signed_data , signature )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *Cert_ID*  
 데이터베이스에 있는 인증서의 ID입니다. *Cert_ID* 는 **int** 입니다.  
  
 *signed_data*  
 인증서로 서명된 데이터를 포함하는 **nvarchar**, **char**, **varchar** 또는 **nchar** 형식의 변수입니다.  
  
 *서명*  
 서명된 데이터에 첨부된 서명입니다. *signature* 는 **varbinary** 입니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
 서명된 데이터가 변경되지 않았으면 1을, 변경되었으면 0을 반환합니다.  
  
## <a name="remarks"></a>설명  
 **VerifySignedBycert** 는 지정한 인증서의 공개 키를 사용하여 데이터의 서명을 해독하고 해독된 값을 데이터의 새로 계산된 MD5 해시와 비교합니다. 값이 일치하면 서명이 유효하게 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 인증서에 대한 VIEW DEFINITION 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-verifying-that-signed-data-has-not-been-tampered-with"></a>A. 서명된 데이터가 변경되지 않았는지 확인  
 다음 예에서는 `Signed_Data`의 정보가 `Shipping04`라는 인증서로 서명된 후 변경되었는지 테스트합니다. 서명은 `DataSignature`에 저장됩니다. 인증서 `Shipping04`는 데이터베이스 내의 인증서 ID를 반환하는 `Cert_ID`로 전달됩니다. `VerifySignedByCert`가 1을 반환하면 서명이 올바른 것입니다. `VerifySignedByCert`가 0을 반환하면 `Signed_Data`의 데이터는 `DataSignature`를 생성하는 데 사용된 데이터와 다릅니다. 이 경우 `Signed_Data`가 서명된 후 변경되었거나 `Signed_Data`가 다른 인증서로 서명된 것입니다.  
  
```sql
SELECT Data, VerifySignedByCert( Cert_Id( 'Shipping04' ),  
    Signed_Data, DataSignature ) AS IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
### <a name="b-returning-only-records-that-have-a-valid-signature"></a>B. 유효한 서명을 가진 레코드만 반환  
 이 쿼리에서는 인증서 `Shipping04`를 사용하여 서명된 이후 변경되지 않은 레코드만 반환합니다.  
  
```sql
SELECT Data FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByCert( Cert_Id( 'Shipping04' ), Data,   
    DataSignature ) = 1   
AND Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)   
 [SIGNBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/signbycert-transact-sql.md)   
 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
