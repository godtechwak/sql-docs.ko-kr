---
description: Parameters 컬렉션, Command 속성 예제(VB)
title: Parameters 컬렉션, Command 속성 예제 (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Command property [ADOX], Visual Basic example
ms.assetid: 7df1089e-69b7-476e-9244-19947c087351
author: rothja
ms.author: jroth
ms.openlocfilehash: a1cc5fd7560fc62475b3cd8a45451791b2dfeac9
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983834"
---
# <a name="parameters-collection-command-property-example-vb"></a>Parameters 컬렉션, Command 속성 예제(VB)
다음 [코드에서는 command 개체와](../ado-api/command-object-ado.md) 함께 [command](./command-property-adox.md) 속성을 사용 하 여 프로시저에 대 한 매개 변수 정보를 검색 하는 방법을 보여 줍니다.  
  
```  
' BeginParametersVB  
Sub Main()  
    On Error GoTo ProcedureParametersError  
  
    Dim cnn As New ADODB.Connection  
    Dim cmd As ADODB.Command  
    Dim prm As ADODB.Parameter  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Connection  
    cnn.Open _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Open the catalog  
    Set cat.ActiveConnection = cnn  
  
    ' Get the command object  
    Set cmd = cat.Procedures("CustomerById").Command  
  
    ' Retrieve Parameter information  
    cmd.Parameters.Refresh  
    For Each prm In cmd.Parameters  
        Debug.Print prm.Name & ":" & prm.Type  
    Next  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set cmd = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
ProcedureParametersError:  
  
    Set cat = Nothing  
    Set cmd = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndParametersVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [ActiveConnection 속성 (ADOX)](./activeconnection-property-adox.md)   
 [Catalog 개체 (ADOX)](./catalog-object-adox.md)   
 [Command 속성 (ADOX)](./command-property-adox.md)   
 [Procedure 개체 (ADOX)](./procedure-object-adox.md)   
 [Procedures 컬렉션(ADOX)](./procedures-collection-adox.md)