---
description: Connection (Visual C++ 構文用の ADO)
title: 接続 (ADO for Visual C++ 構文) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- Connection collection [ADO], ADO for Visual C++ syntax
ms.assetid: cb5e1e15-c5b4-44ab-892f-bf1ae601d0a5
author: rothja
ms.author: jroth
ms.openlocfilehash: 3458c35012535e454fa3ccad52834faebd439131
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974953"
---
# <a name="connection-ado-for-visual-c-syntax"></a>Connection (Visual C++ 構文用の ADO)
## <a name="methods"></a>メソッド  
  
```  
BeginTrans(long *TransactionLevel)  
CommitTrans(void)  
RollbackTrans(void)  
Cancel(void)  
Close(void)  
Execute(BSTR CommandText, VARIANT *RecordsAffected, long Options, _ADORecordset **ppiRset)  
Open(BSTR ConnectionString, BSTR UserID, BSTR Password, long Options)  
OpenSchema(SchemaEnum Schema, VARIANT Restrictions, VARIANT SchemaID, _ADORecordset **pprset)  
```  
  
## <a name="properties"></a>プロパティ  
  
```  
get_Attributes(long *plAttr)  
put_Attributes(long lAttr)  
get_CommandTimeout(LONG *plTimeout)  
put_CommandTimeout(LONG lTimeout)  
get_ConnectionString(BSTR *pbstr)  
put_ConnectionString(BSTR bstr)  
get_ConnectionTimeout(LONG *plTimeout)  
put_ConnectionTimeout(LONG lTimeout)  
get_CursorLocation(CursorLocationEnum *plCursorLoc)  
put_CursorLocation(CursorLocationEnum lCursorLoc)  
get_DefaultDatabase(BSTR *pbstr)  
put_DefaultDatabase(BSTR bstr)  
get_IsolationLevel(IsolationLevelEnum *Level)  
put_IsolationLevel(IsolationLevelEnum Level)  
get_Mode(ConnectModeEnum *plMode)  
put_Mode(ConnectModeEnum lMode)  
get_Provider(BSTR *pbstr)  
put_Provider(BSTR Provider)  
get_State(LONG *plObjState)  
get_Version(BSTR *pbstr)  
get_Errors(ADOErrors **ppvObject)  
```  
  
## <a name="events"></a>イベント  
  
```  
BeginTransComplete(LONG TransactionLevel, ADOError *pError, EventStatusEnum *adStatus, _ADOConnection *pConnection)  
CommitTransComplete(ADOError *pError, EventStatusEnum *adStatus, _ADOConnection *pConnection)  
ConnectComplete(ADOError *pError, EventStatusEnum *adStatus, _ADOConnection *pConnection)  
Disconnect(EventStatusEnum *adStatus, _ADOConnection *pConnection)  
ExecuteComplete(LONG RecordsAffected, ADOError *pError, EventStatusEnum *adStatus, _ADOCommand *pCommand, _ADORecordset *pRecordset, _ADOConnection *pConnection)  
InfoMessage(ADOError *pError, EventStatusEnum *adStatus, _ADOConnection *pConnection)  
RollbackTransComplete(ADOError *pError, EventStatusEnum *adStatus, _ADOConnection *pConnection)  
WillConnect(BSTR *ConnectionString, BSTR *UserID, BSTR *Password, long *Options, EventStatusEnum *adStatus, _ADOConnection *pConnection)  
WillExecute(BSTR *Source, CursorTypeEnum *CursorType, LockTypeEnum *LockType, long *Options, EventStatusEnum *adStatus, _ADOCommand *pCommand, _ADORecordset *pRecordset, _ADOConnection *pConnection)  
```  
  
## <a name="see-also"></a>参照  
 [Connection オブジェクト (ADO)](./connection-object-ado.md)