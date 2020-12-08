---
title: Windows 애플리케이션 로그 보기(Windows) | Microsoft Docs
description: SQL Server가 Windows 애플리케이션 로그를 사용하도록 구성된 경우 각 세션은 해당 로그에 이벤트를 씁니다. Windows 애플리케이션 로그를 보는 방법을 알아봅니다.
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- application logs [SQL Server]
- logs [SQL Server], application
- monitoring Windows NT application log [SQL Server]
- Windows NT application logs [SQL Server]
- displaying logs
- monitoring [SQL Server], events
- logs [SQL Server], viewing
ms.assetid: 168a6c6e-12df-46a9-9904-55d63ca8fe14
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 714e1f694faac9bf72c09dbe60ff94d5cb99fb9a
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96504853"
---
# <a name="view-the-windows-application-log-windows-10"></a>Windows 애플리케이션 로그 보기(Windows 10)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Windows 애플리케이션 로그를 사용하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 구성된 경우 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 세션은 해당 로그에 새 이벤트를 씁니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와는 달리 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 시작할 때마다 새 애플리케이션 로그가 생성되지는 않습니다.  
  
## <a name="view-the-windows-application-log"></a>Windows 애플리케이션 로그 보기  
  
1. **검색 표시줄** 에 **이벤트 뷰어** 를 입력한 다음 **이벤트 뷰어** 데스크톱 앱을 선택합니다.
  
2. **이벤트 뷰어** 에서 **애플리케이션 및 서비스 로그** 를 엽니다.

3. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트는 **원본** 열에서 **MSSQLSERVER** 항목으로 식별됩니다(명명된 인스턴스는 **MSSQL$** _<instance_name>_ 으로 식별됨). SQL Server 에이전트 이벤트는 SQLSERVERAGENT 항목으로 식별됩니다. 명명된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 이벤트는 **SQLAgent$** \<*instance_name*>으로 식별됩니다. Microsoft Search 서비스 이벤트는 **Microsoft Search** 항목으로 식별됩니다.  
  
4. 다른 컴퓨터의 로그를 보려면 **이벤트 뷰어(로컬)** 를 마우스 오른쪽 단추로 클릭합니다. **다른 컴퓨터에 연결** 을 선택하고 필드를 입력하여 **컴퓨터 선택** 대화 상자를 완료합니다.  
  
5. 필요에 따라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트만 표시하려면 **보기** 메뉴에서 **필터** 를 선택합니다. **이벤트 소스** 목록에서 **MSSQLSERVER** 를 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 이벤트만 표시하려면 **이벤트 원본** 목록에서 **SQLSERVERAGENT** 를 선택합니다.  
  
6. 이벤트에 대한 자세한 내용을 보려면 해당 이벤트를 두 번 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 오류 로그 보기&#40;SQL Server Management Studio&#41;](../../relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)  
  
  
