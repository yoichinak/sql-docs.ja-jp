---
description: ExecuteComplete イベント (ADO)
title: ExecuteComplete イベント (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- ExecuteComplete event [ADO]
ms.assetid: 62470d42-e511-494c-bec4-ad4591734b7b
author: rothja
ms.author: jroth
ms.openlocfilehash: 36e27f8a86fce348dbf2061a1c7be91f43be9adc
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973393"
---
# <a name="executecomplete-event-ado"></a>ExecuteComplete イベント (ADO)
**ExecuteComplete**イベントは、コマンドの実行が完了した後に呼び出されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
ExecuteComplete RecordsAffected, pError, adStatus, pCommand, pRecordset, pConnection  
```  
  
#### <a name="parameters"></a>パラメーター  
 *RecordsAffected*  
 コマンドの影響を受けるレコードの数を示す **Long 型** の値。  
  
 *pError*  
 [エラー](../../../ado/reference/ado-api/error-object.md)オブジェクトです。 **Adstatus**の値が**adstatuserrorて**いる場合に発生したエラーについて説明します。それ以外の場合は設定されません。  
  
 *adStatus*  
 [Eventstatusenum](../../../ado/reference/ado-api/eventstatusenum.md)状態の値です。 このイベントが呼び出されると、このパラメーターは、イベントの原因となった操作が成功した場合は **Adstatusok** に、操作が失敗した場合は **Adstatuserrorの curred** に設定されます。  
  
 このイベントが返される前に、このパラメーターを **adStatusUnwantedEvent** に設定して、後続の通知が行われないようにします。  
  
 *pCommand*  
 実行された [コマンド](../../../ado/reference/ado-api/command-object-ado.md) オブジェクト。 **Connection.Exeかわいらしい**またはレコードセットを呼び出すときで**も、コマンドオブジェクトを含み**ます **。コマンド**を明示的に作成する必要は**ありません。** この場合、**コマンド**オブジェクトは ADO によって内部的に作成されます。  
  
 *pRecordset*  
 実行されたコマンドの結果である [レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md) オブジェクト。 この **レコードセット** は空にすることができます。 このイベントハンドラー内からは、このレコードセットオブジェクトを破棄しないでください。 これを行うと、存在しなくなったオブジェクトに ADO がアクセスしようとしたときにアクセス違反が発生します。  
  
 *pConnection*  
 [接続](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトです。 操作が実行された接続です。  
  
## <a name="remarks"></a>解説  
 接続が原因で**ExecuteComplete**イベントが発生する可能性があり**ます。** コマンドを[実行](../../../ado/reference/ado-api/execute-method-ado-connection.md)**します。**[Execute](../../../ado/reference/ado-api/execute-method-ado-command.md)、 **Recordset。** レコードセットを[開き](../../../ado/reference/ado-api/open-method-ado-recordset.md)**ます。**[Requery](../../../ado/reference/ado-api/requery-method.md)、または**レコードセット。**[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)メソッド。  
  
## <a name="see-also"></a>参照  
 [ADO Events モデルの例 (VC + +)](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO イベント ハンドラーの概要](../../../ado/guide/data/ado-event-handler-summary.md)
