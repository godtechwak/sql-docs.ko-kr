---
description: 사용자 지정 태스크에서 이벤트 발생 및 정의
title: 사용자 지정 태스크에서 이벤트 발생 및 정의 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SSIS events, custom
- status information [SQL Server], task events
- custom tasks [Integration Services], events
- SSIS custom tasks, events
- IDTSComponentEvents interface
- events [Integration Services], custom
- events [Integration Services], runtime
- custom events [Integration Services]
- SSIS events, runtime
- IDTSEvents interface
ms.assetid: e0898aa1-e90c-4c4e-99d4-708a76efddfd
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 69f2f6c7f27f4a199ff96661595bb03b3eaafb62
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88477381"
---
# <a name="raising-and-defining-events-in-a-custom-task"></a>사용자 지정 태스크에서 이벤트 발생 및 정의

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 런타임 엔진에서는 태스크의 유효성 검사 및 실행 시 태스크의 진행 상태에 대한 정보를 제공하는 이벤트의 컬렉션을 제공합니다. <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> 인터페이스는 이러한 이벤트를 정의하며 <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Validate%2A> 및 <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Execute%2A> 메서드에 대한 매개 변수로 태스크에 제공됩니다.  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSEvents> 인터페이스에 정의되며 태스크 대신 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>에서 발생시키는 다른 이벤트 집합도 있습니다. <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>에서는 유효성 검사 및 실행 전후에 이벤트를 발생시키는 반면 태스크에서는 실행 및 유효성 검사 도중에 이벤트를 발생시킵니다.  
  
## <a name="creating-custom-events"></a>사용자 지정 이벤트 만들기  
 사용자 지정 태스크 개발자는 <xref:Microsoft.SqlServer.Dts.Runtime.EventInfo> 메서드의 재정의된 구현에서 새 <xref:Microsoft.SqlServer.Dts.Runtime.Task.InitializeTask%2A>를 만들어 새 사용자 지정 이벤트를 정의할 수 있습니다. 생성된 <xref:Microsoft.SqlServer.Dts.Runtime.EventInfo>는 <xref:Microsoft.SqlServer.Dts.Runtime.EventInfos.Add%2A> 메서드를 사용하여 **EventInfos** 컬렉션에 추가됩니다. <xref:Microsoft.SqlServer.Dts.Runtime.EventInfos.Add%2A> 메서드의 서명은 다음과 같습니다.  
  
 `public void Add(string eventName, string description, bool allowEventHandlers, string[] parameterNames, TypeCode[] parameterTypes, string[] parameterDescriptions);`  
  
 다음 코드 샘플에서는 두 개의 사용자 지정 이벤트를 만들고 해당 속성을 설정하는 사용자 지정 태스크의 **InitializeTask** 메서드를 보여 줍니다. 그런 다음 새 이벤트를 <xref:Microsoft.SqlServer.Dts.Runtime.EventInfos> 컬렉션에 추가합니다.  
  
 첫 번째 사용자 지정 이벤트에는 "**OnBeforeIncrement**"라는 *eventName* 과 "**Fires after the initial value is updated.**"라는 *description* 이 있습니다. 다음 매개 변수인 **true** 값은 이 이벤트에서 이벤트를 처리하기 위해 이벤트 처리기 컨테이너를 만들 수 있도록 허용해야 함을 나타냅니다. 이벤트 처리기는 패키지, 시퀀스, ForLoop, ForEachLoop 등의 다른 컨테이너와 같이 태스크에 패키지의 구조와 서비스를 제공하는 컨테이너입니다. *allowEventHandlers* 매개 변수가 **true** 이면 해당 이벤트에 대한 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 개체가 생성됩니다. 그러면 해당 이벤트에 대해 정의된 모든 매개 변수를 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>의 변수 컬렉션에 있는 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>에서 사용할 수 있습니다.  
  
```csharp  
public override void InitializeTask(Connections connections,  
   VariableDispenser variables, IDTSInfoEvents events,  
   IDTSLogging log, EventInfos eventInfos,  
   LogEntryInfos logEntryInfos, ObjectReferenceTracker refTracker)  
{  
    this.eventInfos = eventInfos;  
    string[] paramNames = new string[1];  
    TypeCode[] paramTypes = new TypeCode[1]{TypeCode.Int32};  
    string[] paramDescriptions = new string[1];  
  
    paramNames[0] = "InitialValue";  
    paramDescriptions[0] = "The value before it is incremented.";  
  
    this.eventInfos.Add("OnBeforeIncrement",   
      "Fires before the task increments the value.",  
      true,paramNames,paramTypes,paramDescriptions);  
    this.onBeforeIncrement = this.eventInfos["OnBeforeIncrement"];  
  
    paramDescriptions[0] = "The value after it has been incremented.";  
    this.eventInfos.Add("OnAfterIncrement",  
      "Fires after the initial value is updated.",  
      true,paramNames, paramTypes,paramDescriptions);  
    this.onAfterIncrement = this.eventInfos["OnAfterIncrement"];  
}  
```  
  
```vb  
Public Overrides Sub InitializeTask(ByVal connections As Connections, _  
ByVal variables As VariableDispenser, ByVal events As IDTSInfoEvents, _  
ByVal log As IDTSLogging, ByVal eventInfos As EventInfos, _  
ByVal logEntryInfos As LogEntryInfos, ByVal refTracker As ObjectReferenceTracker)   
  
    Dim paramNames(0) As String  
    Dim paramTypes(0) As TypeCode = {TypeCode.Int32}  
    Dim paramDescriptions(0) As String  
  
    Me.eventInfos = eventInfos  
  
    paramNames(0) = "InitialValue"  
    paramDescriptions(0) = "The value before it is incremented."  
  
    Me.eventInfos.Add("OnBeforeIncrement", _  
      "Fires before the task increments the value.", _  
      True, paramNames, paramTypes, paramDescriptions)  
    Me.onBeforeIncrement = Me.eventInfos("OnBeforeIncrement")  
  
    paramDescriptions(0) = "The value after it has been incremented."  
    Me.eventInfos.Add("OnAfterIncrement", _  
      "Fires after the initial value is updated.", True, _  
      paramNames, paramTypes, paramDescriptions)  
    Me.onAfterIncrement = Me.eventInfos("OnAfterIncrement")  
  
End Sub  
```  
  
## <a name="raising-custom-events"></a>사용자 지정 이벤트 발생  
 사용자 지정 이벤트는 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireCustomEvent%2A> 메서드를 호출하면 발생합니다. 다음 코드 줄은 사용자 지정 이벤트를 발생시킵니다.  
  
```csharp  
componentEvents.FireCustomEvent(this.onBeforeIncrement.Name,  
   this.onBeforeIncrement.Description, ref arguments,  
   null, ref bFireOnBeforeIncrement);  
```  
  
```vb  
componentEvents.FireCustomEvent(Me.onBeforeIncrement.Name, _  
Me.onBeforeIncrement.Description, arguments, _  
Nothing,  bFireOnBeforeIncrement)  
```  
  
## <a name="sample"></a>예제  
 다음 예에서는 **InitializeTask** 메서드에서 사용자 지정 이벤트를 정의하고 이 사용자 지정 이벤트를 <xref:Microsoft.SqlServer.Dts.Runtime.EventInfos> 컬렉션에 추가한 다음 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireCustomEvent%2A> 메서드를 호출하여 **Execute** 메서드 실행 중 사용자 지정 이벤트를 발생시키는 태스크를 보여 줍니다.  
  
```csharp  
[DtsTask(DisplayName = "CustomEventTask")]  
    public class CustomEventTask : Task  
    {  
        public override DTSExecResult Execute(Connections connections,   
          VariableDispenser variableDispenser, IDTSComponentEvents componentEvents,  
           IDTSLogging log, object transaction)  
        {  
            bool fireAgain;  
            object[] args = new object[1] { "The value of the parameter." };  
            componentEvents.FireCustomEvent( "MyCustomEvent",   
              "Firing the custom event.", ref args,  
              "CustomEventTask" , ref fireAgain );  
            return DTSExecResult.Success;  
        }  
  
        public override void InitializeTask(Connections connections,  
          VariableDispenser variableDispenser, IDTSInfoEvents events,  
          IDTSLogging log, EventInfos eventInfos,  
          LogEntryInfos logEntryInfos, ObjectReferenceTracker refTracker)  
        {  
            string[] names = new string[1] {"Parameter1"};  
            TypeCode[] types = new TypeCode[1] {TypeCode.String};  
            string[] descriptions = new string[1] {"Parameter description." };  
  
            eventInfos.Add("MyCustomEvent",  
             "Fires when my interesting event happens.",  
             true, names, types, descriptions);  
  
        }  
   }  
```  
  
```vb  
<DtsTask(DisplayName = "CustomEventTask")> _   
    Public Class CustomEventTask  
     Inherits Task  
        Public Overrides Function Execute(ByVal connections As Connections, _  
          ByVal variableDispenser As VariableDispenser, _  
          ByVal componentEvents As IDTSComponentEvents, _  
          ByVal log As IDTSLogging, ByVal transaction As Object) _  
          As DTSExecResult  
  
            Dim fireAgain As Boolean  
            Dim args() As Object =  New Object(1) {"The value of the parameter."}  
  
            componentEvents.FireCustomEvent("MyCustomEvent", _  
              "Firing the custom event.", args, _  
              "CustomEventTask" ,  fireAgain)  
            Return DTSExecResult.Success  
        End Function  
  
        Public Overrides  Sub InitializeTask(ByVal connections As Connections, _  
          ByVal variableDispenser As VariableDispenser,  
          ByVal events As IDTSInfoEvents,  
          ByVal log As IDTSLogging, ByVal eventInfos As EventInfos, ByVal logEnTryInfos As LogEnTryInfos, ByVal refTracker As ObjectReferenceTracker)  
  
            Dim names() As String =  New String(1) {"Parameter1"}  
            Dim types() As TypeCode =  New TypeCode(1) {TypeCode.String}  
            Dim descriptions() As String =  New String(1) {"Parameter description."}  
  
            eventInfos.Add("MyCustomEvent", _  
              "Fires when my interesting event happens.", _  
              True, names, types, descriptions)  
  
        End Sub  
  
    End Class  
```  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services&#40;SSIS&#41; 이벤트 처리기](../../../integration-services/integration-services-ssis-event-handlers.md)   
 [패키지에 이벤트 처리기 추가](https://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)  
  
  
