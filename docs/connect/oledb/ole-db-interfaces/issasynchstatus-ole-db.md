---
title: ISSAsynchStatus(OLE DB 드라이버) | Microsoft Docs
description: OLE DB Driver for SQL Server가 ISSAsynchStatus 인터페이스를 사용하여 SQL Server 비동기 작업을 지원하는 방법을 알아봅니다.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAsynchStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSAsynchStatus interface
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1cc7d83cd9d014e863493365345b8f399f2ee713
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862182"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus(OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  **ISSAsynchStatus** 인터페이스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 비동기 작업에 대한 지원을 제공합니다. 핵심 OLE DB 인터페이스인 **IDBAsynchStatus**에서 상속되는 선택적 인터페이스입니다. **ISSAsynchStatus** 는 **IDBAsynchStatus** 에서 상속된 **Abort**및 **GetStatus** 메서드 이외에도 비동기 작업이 완료되거나 제한 시간이 초과될 때까지 대기하는 데 사용되는 새 메서드를 제공합니다.  
  
|방법|Description|  
|------------|-----------------|  
|[ISSAsynchStatus::Abort&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-abort-ole-db.md)|비동기적으로 실행 중인 작업을 취소합니다.|  
|[ISSAsynchStatus::GetStatus&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|비동기적으로 실행 중인 작업의 상태를 반환합니다.|  
|[ISSAsynchStatus::WaitForAsynchCompletion&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|비동기적으로 실행 중인 작업이 완료되거나 제한 시간이 초과될 때까지 대기합니다.|  
  
## <a name="remarks"></a>설명  
 **ISSAsynchStatus::GetStatus** 메서드의 **ISSAsynchStatus** 구현은 **IDBAsynchStatus::GetStatus** 메서드와 같지만 데이터 원본 개체의 초기화가 중단된 경우 DB_E_CANCELED 대신 E_UNEXPECTED를 반환한다는 점만 다릅니다(단, **ISSAsynchStatus::WaitForAsynchCompletion** 은 DB_E_CANCELED를 반환함). 이는 중단 작업 이후 데이터 원본 개체가 평소의 상태로 유지되지 않아 추가적인 초기화 작업이 시도될 수 있기 때문입니다.  
  
 다음 메서드를 사용하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서 비동기적인 실행을 사용할 수 있습니다.  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>참고 항목  
 [인터페이스&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [비동기 작업 수행](../../oledb/features/performing-asynchronous-operations.md)  
  
  
