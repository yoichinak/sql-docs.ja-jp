---
description: ADO のオブジェクトとインターフェイス
title: ADO オブジェクトとインターフェイス |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, objects and interfaces
- objects [ADO]
ms.assetid: d0b7e254-c89f-4406-b846-a060ef038c30
author: rothja
ms.author: jroth
ms.openlocfilehash: 80391605a0480d8967afb1e0240168a393f09363
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976313"
---
# <a name="ado-objects-and-interfaces"></a>ADO のオブジェクトとインターフェイス
これらのオブジェクト間のリレーションシップは、 [ADO オブジェクトモデル](./ado-object-model.md)で表現されます。  
  
 各オブジェクトは、対応するコレクションに含めることができます。 たとえば、 [エラー](./error-object.md) オブジェクトを [エラー](./errors-collection-ado.md) コレクションに含めることができます。 詳細については、「 [ADO コレクション](./ado-collections.md) 」または「特定のコレクションに関するトピック」を参照してください。  
  
|オブジェクトまたはインターフェイス|説明|  
|-|-|  
|[IADOCommandConstruction](/previous-versions/windows/desktop/aa965677(v=vs.85))|ADOCommand オブジェクトから基になる OLEDB コマンドを取得するために使用します。|  
|[ADORecordConstruction](./adorecordconstruction-interface.md)|C/c + + アプリケーションの OLE DB **Row**オブジェクトから ADO**レコード**オブジェクトを構築します。|  
|[ADORecordsetConstruction](./adorecordsetconstruction-interface.md)|C/c + + アプリケーションの OLE DB**行**セットオブジェクトから ADO**レコードセット**オブジェクトを構築します。|  
|[ADOStreamConstruction インターフェイス](./adostreamconstruction-interface.md)|C/c + + アプリケーションの OLE DB **IStream**オブジェクトから ADO**ストリーム**オブジェクトを構築します。|  
|[コマンド](./command-object-ado.md)|データソースに対して実行する特定のコマンドを定義します。<br /><br /> **コマンド**オブジェクトは、スクリプト作成には安全ではありません。|  
|[接続](./connection-object-ado.md)|データ ソースへの開いた接続を表します。<br /><br /> **接続**オブジェクトは、スクリプトに対して安全です。|  
|[IDSOShapeExtensions インターフェイス](./idsoshapeextensions-interface.md)|図形プロバイダーの基になる OLEDB データソースオブジェクトを取得します。|  
|[Error](./error-object.md)|プロバイダーに関連する1つの操作に関連するデータアクセスエラーの詳細が含まれています。<br /><br /> **エラー**オブジェクトは、スクリプト作成には安全ではありません。|  
|[フィールド](./field-object.md)|共通のデータ型のデータ列を表します。|  
|[パラメーター](./parameter-object.md)|パラメーター化クエリまたはストアドプロシージャに基づいて **Command** オブジェクトに関連付けられたパラメーターまたは引数を表します。<br /><br /> **パラメーター**オブジェクトは、スクリプト作成には安全ではありません。|  
|[プロパティ](./property-object-ado.md)|プロバイダーによって定義される ADO オブジェクトの動的特性を表します。|  
|[レコード](./record-object-ado.md)|**レコードセット**の行、またはファイルシステム内のディレクトリまたはファイルを表します。 **レコード**オブジェクトは、スクリプトに対して安全です。|  
|[レコードセット](./recordset-object-ado.md)|ベーステーブルからのレコードのセット、または実行されたコマンドの結果を表します。 **レコードセット**オブジェクトは、常に、セット内の1つのレコードのみを現在のレコードとして参照します。<br /><br /> **レコードセット**オブジェクトは、スクリプトに対して安全です。|  
|[Stream](./stream-object-ado.md)|データのバイナリストリームを表します。<br /><br /> **ストリーム**オブジェクトは、スクリプトに対して安全です。|  
  
## <a name="see-also"></a>参照  
 [ADO API リファレンス](./ado-api-reference.md)   
 [ADO コレクション](./ado-collections.md)   
 [ADO の動的プロパティ](./ado-dynamic-properties.md)   
 [ADO 列挙定数](./ado-enumerated-constants.md)   
 [付録 B: ADO エラー](../../guide/appendixes/appendix-b-ado-errors.md)   
 [ADO イベント](./ado-events.md)   
 [ADO メソッド](./ado-methods.md)   
 [ADO オブジェクトモデル](./ado-object-model.md)   
 [ADO のプロパティ](./ado-properties.md)