---
description: '&#x40;&#x40;옵션(Transact-SQL)'
title: '@@OPTIONS(Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@OPTIONS'
- '@@OPTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, current SET options
- '@@OPTIONS function'
- current SET options
ms.assetid: 3d5c7f6e-157b-4231-bbb4-4645a11078b3
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: aba9b19dd9788eef4f322db198dd7f8f3789a8c8
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128392"
---
# <a name="x40x40options-transact-sql"></a>&#x40;&#x40;옵션(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  현재 SET 옵션에 대한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
@@OPTIONS  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>반환 형식
 **integer**  
  
## <a name="remarks"></a>설명  
 옵션은 **SET** 명령을 사용하는 경우 또는 **sp_configure user options** 값에서 나올 수 있습니다. **SET** 명령으로 구성한 세션 값은 **sp_configure** 옵션을 재정의합니다. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]와 같은 많은 도구가 집합 옵션을 자동으로 구성합니다. 각 사용자는 구성을 나타내는 @@OPTIONS 함수를 가집니다.  
  
 SET 문을 사용하여 특정 사용자 세션에 대한 언어와 쿼리 처리 옵션을 변경할 수 있습니다. **\@\@OPTIONS** 는 ON 또는 OFF로 설정된 옵션만 검색할 수 있습니다.  
  
 **\@\@OPTIONS** 함수는 10진수 정수로 변환된 옵션의 비트맵을 반환합니다. 비트 설정은 [사용자 옵션 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md) 항목의 표에 나와 있는 위치에 저장됩니다.  
  
 **\@\@OPTIONS** 값을 해독하려면 **\@\@OPTIONS** 에서 반환한 정수를 이진으로 변환한 다음, [사용자 옵션 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)의 표에서 값을 검색합니다. 예를 들어 `SELECT @@OPTIONS;`에서 `5496` 값을 반환하는 경우 Windows 프로그래머 계산기(**calc.exe**)를 사용하여 10진수 `5496`을 이진으로 변환하세요. 결과는 `1010101111000`입니다. 가장 오른쪽의 문자(이진 1, 2, 4)는 0으로, 표의 맨 앞 세 항목이 해제된 상태를 나타냅니다. 표에서 해당 항목은 **DISABLE_DEF_CNST_CHK**, **IMPLICIT_TRANSACTIONS**, **CURSOR_CLOSE_ON_COMMIT** 입니다. 다음 항목(`1000` 위치의 **ANSI_WARNINGS**)이 설정되어 있습니다. 비트맵에서 계속 왼쪽으로 작동하다가 옵션 목록의 아래로 이동합니다. 가장 왼쪽 옵션이 0이면 유형 변환에 의해 잘립니다. 비트맵 `1010101111000`은 실제로 `001010101111000`으로 모두 15개의 옵션을 나타냅니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-demonstration-of-how-changes-affect-behavior"></a>A. 변경이 동작에 미치는 영향 설명  
 다음 예에서는 두 가지 **CONCAT_NULL_YIELDS_NULL** 옵션 설정으로 연결 동작의 차이점을 설명합니다.  
  
```sql  
SELECT @@OPTIONS AS OriginalOptionsValue;  
SET CONCAT_NULL_YIELDS_NULL OFF;  
SELECT 'abc' + NULL AS ResultWhen_OFF, @@OPTIONS AS OptionsValueWhen_OFF;  
  
SET CONCAT_NULL_YIELDS_NULL ON;  
SELECT 'abc' + NULL AS ResultWhen_ON, @@OPTIONS AS OptionsValueWhen_ON;  
```  
  
### <a name="b-testing-a-client-nocount-setting"></a>B. 클라이언트 NOCOUNT 설정 테스트  
 다음 예에서는 `NOCOUNT``ON`을 설정한 후 `@@OPTIONS`의 값을 테스트합니다. `NOCOUNT``ON` 옵션은 세션 내의 모든 문 실행 시 영향 받은 행의 수를 표시하는 메시지를 요청 클라이언트로 다시 보내지 않도록 합니다. `@@OPTIONS`의 값은 `512`(0x0200)로 설정되며 이는 NOCOUNT 옵션을 나타냅니다. 이 예에서는 클라이언트에서 NOCOUNT 옵션을 사용할 수 있는지 테스트합니다. 이러한 방법은 예를 들어 클라이언트에서 성능 차이를 추적하는 데 도움이 될 수 있습니다.  
  
```sql  
SET NOCOUNT ON  
IF @@OPTIONS & 512 > 0   
RAISERROR ('Current user has SET NOCOUNT turned on.', 1, 1)  
```  
  
## <a name="see-also"></a>참고 항목  
 [구성 함수&#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [user options 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)  
  
  
