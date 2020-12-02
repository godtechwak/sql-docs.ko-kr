---
description: KEY_NAME(Transact-SQL)
title: KEY_NAME(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- KEY_NAME_TSQL
- KEY_NAME
dev_langs:
- TSQL
helpviewer_keywords:
- KEY_NAME function
ms.assetid: 7b693e5d-2325-4bf9-9b45-ad6a23374b41
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9ccc9a860218a6fa39596faaee78908eedf6907a
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91115992"
---
# <a name="key_name-transact-sql"></a>KEY_NAME(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  대칭 키 GUID 또는 ciphertext에서 대칭 키의 이름을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
KEY_NAME ( ciphertext | key_guid )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *ciphertext*  
 대칭 키로 암호화되는 텍스트입니다. *cyphertext* 는 **varbinary(8000)** 형식입니다.  
  
 *key_guid*  
 대칭 키의 GUID입니다. *key_guid* 는 **uniqueidentifier** 형식입니다.  
  
## <a name="returned-types"></a>반환 형식  
 **varchar(128)**  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터는 사용자가 소유하고 있거나 일부 사용 권한이 부여된 보안 개체에 대해서만 메타데이터를 볼 수 있도록 제한됩니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-displaying-the-name-of-a-symmetric-key-using-the-key_guid"></a>A. key_guid를 사용하여 대칭 키의 이름 표시  
 **master** 데이터베이스에는 ##MS_ServiceMasterKey##라는 대칭 키가 있습니다. 다음 예에서는 sys.symmetric_keys 동적 관리 뷰에서 해당 키의 GUID를 가져오고, 이를 변수에 할당한 다음 해당 변수를 KEY_NAME 함수로 전달하여 GUID에 해당하는 이름을 반환하는 방법을 보여 줍니다.  
  
```sql  
USE master;  
GO  
DECLARE @guid uniqueidentifier ;  
SELECT @guid = key_guid FROM sys.symmetric_keys  
WHERE name = '##MS_ServiceMasterKey##' ;  
-- Demonstration of passing a GUID to KEY_NAME to receive a name  
SELECT KEY_NAME(@guid) AS [Name of Key];  
```  
  
### <a name="b-displaying-the-name-of-a-symmetric-key-using-the-cipher-text"></a>B. ciphertext를 사용하여 대칭 키의 이름 표시  
 다음 예에서는 대칭 키를 만들고 데이터를 테이블에 채우는 전체 과정을 보여 줍니다. 그런 다음 암호화된 텍스트를 전달할 때 KEY_NAME이 키 이름을 반환하는 방법을 보여 줍니다.  
  
```sql 
-- Create a symmetric key  
CREATE SYMMETRIC KEY TestSymKey   
   WITH ALGORITHM = AES_128,  
   KEY_SOURCE = 'The square of the hypotenuse is equal to the sum of the squares of the sides',  
   IDENTITY_VALUE = 'Pythagoras'  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y' ;  
GO  
-- Create a table for the demonstration  
CREATE TABLE DemoKey  
(IDCol INT IDENTITY PRIMARY KEY,  
SecretCol VARBINARY(256) NOT NULL)  
GO  
-- Open the symmetric key if not already open  
OPEN SYMMETRIC KEY TestSymKey   
    DECRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
-- Insert a row into the DemoKey table  
DECLARE @key_GUID uniqueidentifier;  
SELECT @key_GUID = key_guid FROM sys.symmetric_keys  
WHERE name LIKE 'TestSymKey' ;  
INSERT INTO DemoKey(SecretCol)  
VALUES ( ENCRYPTBYKEY (@key_GUID, 'EncryptedText'))  
GO  
-- Verify the DemoKey data  
SELECT * FROM DemoKey;  
GO  
-- Decrypt the data  
DECLARE @ciphertext VARBINARY(256);  
SELECT @ciphertext = SecretCol  
FROM DemoKey WHERE IDCol = 1 ;  
SELECT CAST (  
DECRYPTBYKEY( @ciphertext)  
AS VARCHAR(100) ) AS SecretText ;  
-- Use KEY_NAME to view the name of the key  
SELECT KEY_NAME(@ciphertext) AS [Name of Key] ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [ENCRYPTBYKEY&#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEYAUTOASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykeyautoasymkey-transact-sql.md)  
  
  
