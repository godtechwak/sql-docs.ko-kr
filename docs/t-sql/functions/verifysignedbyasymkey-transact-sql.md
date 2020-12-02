---
description: VERIFYSIGNEDBYASYMKEY(Transact-SQL)
title: VERIFYSIGNEDBYASYMKEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- VERIFYSIGNEDBYASYMKEY_TSQL
- VERIFYSIGNEDBYASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- verifying digitally signed data for changes
- VERIFYSIGNEDBYASYMKEY
- testing digitally signed data for changes
- checking digitally signed data for changes
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 9f7c6e0b-5ba4-4dbb-994d-5bd59f4908de
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4f2a75cf3da8220e861d8320b2454683c3b65a1f
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91380598"
---
# <a name="verifysignedbyasymkey-transact-sql"></a>VERIFYSIGNEDBYASYMKEY(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  디지털 서명된 데이터가 서명된 후 변경되었는지 여부를 테스트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
VerifySignedByAsymKey( Asym_Key_ID , clear_text , signature )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *Asym_Key_ID*  
 데이터베이스에 있는 비대칭 키 인증서의 ID입니다.  
  
 *clear_text*  
 확인할 일반 텍스트 데이터입니다.  
  
 *서명*  
 서명된 데이터에 첨부된 서명입니다. *signature* 는 **varbinary** 입니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
 서명이 일치하면 1을 반환하고 그렇지 않으면 0을 반환합니다.  
  
## <a name="remarks"></a>설명  
 **VerifySignedByAsymKey** 는 지정한 비대칭 키의 공개 키를 사용하여 데이터의 서명을 해독하고 해독된 값을 데이터의 새로 계산된 MD5 해시와 비교합니다. 값이 일치하면 서명이 유효하게 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 비대칭 키에 대한 VIEW DEFINITION 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-testing-for-data-with-a-valid-signature"></a>A. 유효한 서명이 있는 데이터 테스트  
 다음 예에서는 선택한 데이터가 `WillisKey74` 비대칭 키로 서명된 후 변경되지 않은 경우 1을 반환하고 데이터가 손상된 경우에는 0을 반환합니다.  
  
```sql
SELECT Data,  
     VerifySignedByAsymKey( AsymKey_Id( 'WillisKey74' ), SignedData,  
     DataSignature ) as IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data encrypted by asymmetric key ''WillisKey74''';  
GO  
RETURN;  
```  
  
### <a name="b-returning-a-result-set-that-contains-data-with-a-valid-signature"></a>B. 유효한 서명이 있는 데이터가 포함된 결과 집합 반환  
 다음 예에서는 `SignedData04` 비대칭 키로 서명된 후 변경되지 않은 데이터가 포함된 `WillisKey74`의 행을 반환합니다. 이 예에서는 `AsymKey_ID` 함수를 호출하여 데이터베이스에서 비대칭 키의 ID를 가져옵니다.  
  
```sql
SELECT Data   
FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByAsymKey( AsymKey_Id( 'WillisKey74' ), Data,  
     DataSignature ) = 1  
AND Description = N'data encrypted by asymmetric key ''WillisKey74''';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [ASYMKEY_ID&#40;Transact-SQL&#41;](../../t-sql/functions/asymkey-id-transact-sql.md)   
 [SIGNBYASYMKEY&#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
