---
description: ISQLServerStatement 인터페이스
title: ISQLServerStatement 인터페이스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 7f83b514-6e76-4f37-baf3-a10db2010e7c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 037da22001317eaa8059e56671b712f151116487
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433455"
---
# <a name="isqlserverstatement-interface"></a>ISQLServerStatement 인터페이스
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  JDBC 문 기능의 기본 구현을 나타냅니다. 이 인터페이스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC 드라이버 3.0에서 추가되었습니다.  
  
 **패키지:** com.microsoft.sqlserver.jdbc  
  
 **확장:** java.sql.Statement  
  
## <a name="syntax"></a>구문  
  
```  
  
public interface ISQLServerStatement  
```  
  
## <a name="remarks"></a>설명  
 이 인터페이스는 [SQLServerStatement 클래스](../../../connect/jdbc/reference/sqlserverstatement-class.md)에 의해 구현됩니다.  
  
 이 인터페이스는 다음 [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 관련 메서드를 노출합니다.  
  
|메서드|자세한 내용은 다음을 참조하세요.|  
|------------|-------------------------------|  
|public String getResponseBuffering|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|  
|public void setResponseBuffering|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|  
  
## <a name="see-also"></a>참고 항목  
 [JDBC 드라이버 API 참조](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
