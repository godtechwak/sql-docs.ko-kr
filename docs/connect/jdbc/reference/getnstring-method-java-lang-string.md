---
description: getNString 메서드(java.lang.String)
title: getNString 메서드(java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b351e999-85bf-498b-915a-f91d89134bce
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e76cfb9175b07d4d7bfae843f0011fe006abc05
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435215"
---
# <a name="getnstring-method-javalangstring"></a>getNString 메서드(java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Java 프로그래밍 언어인 문자열로 지정된 **NCHAR**, **NVARCHAR** 또는 **LONGNVARCHAR** 매개 변수 값을 검색합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
public final java.lang.String getNString(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>매개 변수  
 *parameterName*  
  
 매개 변수 이름이 들어 있는 **문자열**입니다.  
  
## <a name="return-value"></a>반환 값  
 String 개체입니다.  
  
## <a name="exceptions"></a>예외  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>설명  
 이 getNString 메서드는 java.sql.CallableStatement 인터페이스의 getNString 메서드에 의해 지정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [getNString 메서드(SQLServerCallableStatement)](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement 메서드](../../../connect/jdbc/reference/sqlservercallablestatement-methods.md)  
  
  
