---
description: getCharacterStream 메서드(int)
title: getCharacterStream 메서드(int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getCharacterStream (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4f9f230d-be4c-469a-b3dc-f24531429aae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fae765e165eaefd67caf5f07e32c4d61f479c74a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436865"
---
# <a name="getcharacterstream-method-int"></a>getCharacterStream 메서드(int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  이 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) 개체의 현재 행에서 지정된 열 인덱스의 값을 java.io.Reader 개체로 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public java.io.Reader getCharacterStream(int columnIndex)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *columnIndex*  
  
 열 인덱스를 나타내는 **int**입니다.  
  
## <a name="return-value"></a>반환 값  
 Reader 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getCharacterStream 메서드는 java.sql.ResultSet 인터페이스의 getCharacterStream 메서드에 의해 지정됩니다.  
  
 이 메서드는 nchar, nvarchar, nvarchar(max) 및 ntext와 같은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 유니코드 문자 데이터 형식만 읽습니다. ASCII 문자 형식을 비롯한 다른 모든 데이터 형식에서는 예외가 발생합니다. ASCII 데이터 형식을 읽으려면 [getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md) 메서드를 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [getCharacterStream 메서드&#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)   
 [SQLServerResultSet 멤버](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet 클래스](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
