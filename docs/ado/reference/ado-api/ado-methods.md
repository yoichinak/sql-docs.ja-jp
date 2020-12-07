---
description: ADO メソッド
title: ADO メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, methods
- methods [ADO]
ms.assetid: a38c5670-ba28-44f3-bd5b-fcb46880e904
author: rothja
ms.author: jroth
ms.openlocfilehash: 13e126f070f188e47582227fabf4a1e37d6901a3
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976373"
---
# <a name="ado-methods"></a>ADO メソッド

|方法|説明|  
|-|-|  
|[AddNew](./addnew-method-ado.md)|更新可能な **レコードセット** オブジェクトの新しいレコードを作成します。|  
|[Append](./append-method-ado.md)|オブジェクトをコレクションに追加します。 コレクションが **フィールド**の場合は、コレクションに追加する前に新しい **Field** オブジェクトを作成できます。|  
|[AppendChunk](./appendchunk-method-ado.md)|大きなテキストまたはバイナリデータ **フィールド**、または **パラメーター** オブジェクトにデータを追加します。|  
|[BeginTrans、CommitTrans、RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md)|は、次のように、 **接続** オブジェクト内のトランザクション処理を管理します。<br /><br /> **BeginTrans** -新しいトランザクションを開始します。<br /><br /> **CommitTrans** -変更を保存し、現在のトランザクションを終了します。 また、新しいトランザクションを開始することもできます。<br /><br /> **RollbackTrans** -すべての変更を取り消し、現在のトランザクションを終了します。 また、新しいトランザクションを開始することもできます。|  
|[キャンセル](./cancel-method-ado.md)|保留中の非同期メソッド呼び出しの実行を取り消します。|  
|[CancelBatch](./cancelbatch-method-ado.md)|保留中のバッチ更新をキャンセルします。|  
|[CancelUpdate](./cancelupdate-method-ado.md)|**Update**メソッドを呼び出す前に、**レコードセット**オブジェクトの現在または新しい行、または**レコード**オブジェクトの**Fields**コレクションに対して行われたすべての変更を取り消します。|  
|[Clear](./clear-method-ado.md)|**エラーコレクションから**すべての**エラー**オブジェクトを削除します。|  
|[複製](./clone-method-ado.md)|既存の**レコード**セットオブジェクトから、重複する**レコードセット**オブジェクトを作成します。 必要に応じて、複製が読み取り専用であることを指定します。|  
|[閉じる](./close-method-ado.md)|開いているオブジェクトとすべての依存オブジェクトを閉じます。|  
|[CompareBookmarks](./comparebookmarks-method-ado.md)|2つのブックマークを比較し、それらの相対値を示す値を返します。|  
|[CopyRecord](./copyrecord-method-ado.md)|ファイルまたはディレクトリ、およびその内容を別の場所にコピーします。|  
|[CopyTo](./copyto-method-ado.md)|**ストリーム**内の指定した文字数またはバイト数 (**型**によって異なる) を別の**ストリーム**オブジェクトにコピーします。|  
|[CreateParameter](./createparameter-method-ado.md)|指定されたプロパティを持つ新しい **パラメーター** オブジェクトを作成します。|  
|[Delete (ADO Parameters コレクション)](./delete-method-ado-parameters-collection.md)|**Parameters**コレクションからオブジェクトを削除します。|  
|[Delete (ADO Fields コレクション)](./delete-method-ado-fields-collection.md)|**フィールド**コレクションからオブジェクトを削除します。|  
|[Delete (ADO レコードセット)](./delete-method-ado-recordset.md)|現在のレコードまたはレコードのグループを削除します。|  
|[DeleteRecord](./deleterecord-method-ado.md)|ファイルまたはディレクトリ、およびそのすべてのサブディレクトリを削除します。|  
|[Execute (ADO コマンド)](./execute-method-ado-command.md)|**CommandText**プロパティで指定されたクエリ、SQL ステートメント、またはストアドプロシージャを実行します。|  
|[Execute (ADO Connection)](./execute-method-ado-connection.md)|指定されたクエリ、SQL ステートメント、ストアドプロシージャ、またはプロバイダー固有のテキストを実行します。|  
|[Find](./find-method-ado.md)|**レコードセット**内で、指定した条件を満たす行を検索します。|  
|[フラッシュ](./flush-method-ado.md)|ADO バッファーに残っている **ストリーム** の内容を、 **ストリーム** が関連付けられている基になるオブジェクトに強制的に適用します。|  
|[get_OLEDBCommand メソッド](./get-oledbcommand-method.md)|基になる OLEDB コマンドを返します。最初に ADO コマンドで設定されたパラメーター情報を OLEDB コマンドに反映します。|  
|[GetChildren](./getchildren-method-ado.md)|この**レコード**によって表されるディレクトリ内のファイルとサブディレクトリを表す行を含む**レコードセット**を返します。|  
|[GetChunk](./getchunk-method-ado.md)|大きなテキストまたはバイナリデータ **フィールド** オブジェクトの内容のすべて、または一部を返します。|  
|[GetDataProviderDSO メソッド](./getdataproviderdso-method.md)|基になる OLEDB データソースオブジェクトをシェイププロバイダーから取得します。|  
|[GetRows](./getrows-method-ado.md)|**レコードセット**オブジェクトの複数のレコードを配列に取得します。|  
|[GetString](./getstring-method-ado.md)|**レコードセット**を文字列として返します。|  
|[LoadFromFile](./loadfromfile-method-ado.md)|既存のファイルの内容を **ストリーム**に読み込みます。|  
|[移動](./move-method-ado.md)|**レコードセット**オブジェクト内の現在のレコードの位置を移動します。|  
|[MoveFirst、MoveLast、MoveNext、および MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)|指定したレコード **セット** オブジェクト内の最初、最後、次、または前のレコードに移動し、そのレコードを現在のレコードにします。|  
|[MoveRecord](./moverecord-method-ado.md)|ファイルまたはディレクトリとその内容を別の場所に移動します。|  
|[NextRecordset](./nextrecordset-method-ado.md)|一連のコマンドを進めて、現在の **レコードセット** オブジェクトをクリアし、次の **レコードセット** を返します。|  
|[開く (ADO 接続)](./open-method-ado-connection.md)|データソースへの接続を開きます。|  
|[Open (ADO レコード)](./open-method-ado-record.md)|既存の **レコード** オブジェクトを開くか、新しいファイルまたはディレクトリを作成します。|  
|[Open (ADO レコードセット)](./open-method-ado-recordset.md)|カーソルを開きます。|  
|[Open (ADO Stream)](./open-method-ado-stream.md)|**ストリーム**オブジェクトを開き、バイナリデータまたはテキストデータのストリームを操作します。|  
|[OpenSchema](./openschema-method.md)|プロバイダーからデータベーススキーマ情報を取得します。|  
|[put_OLEDBCommand メソッド](./put-oledbcommand-method.md)|このメソッドは操作を実行しません。常に S_OK を返します。|  
|[読み取り](./read-method.md)|**ストリーム**オブジェクトから指定されたバイト数を読み取ります。|  
|[ReadText](./readtext-method.md)|テキスト **ストリーム** オブジェクトから指定された数の文字を読み取ります。|  
|[[更新]](./refresh-method-ado.md)|プロバイダーによって使用可能なオブジェクトを反映するように、コレクション内のオブジェクトを更新します。|  
|[Requery](./requery-method.md)|オブジェクトの基になっているクエリを再実行することによって、 **レコードセット** オブジェクトのデータを更新します。|  
|[再同期](./resync-method.md)|基になるデータベースから、現在の**レコードセット**オブジェクトまたは**レコード**オブジェクトの**Fields**コレクションのデータを更新します。|  
|[および](./save-method.md)|ファイルまたは**ストリーム**オブジェクトに**レコードセット**を保存します。|  
|[SaveToFile](./savetofile-method.md)|**ストリーム**のバイナリコンテンツをファイルに保存します。|  
|[Seek](./seek-method.md)|**レコードセット**のインデックスを検索して、指定した値と一致する行をすばやく検索し、現在の行の位置をその行に変更します。|  
|[SetEOS](./seteos-method.md)|ストリームの末尾である位置を設定します。|  
|[SkipLine](./skipline-method.md)|テキストストリームを読み取るときに、1行全体をスキップします。|  
|[統計](./stat-method.md)|開いているストリームに関する統計情報を取得します。|  
|[サポート](./supports-method.md)|指定した **レコードセット** オブジェクトが特定の種類の機能をサポートするかどうかを判断します。|  
|[アップデート](./update-method.md)|レコード**セット**オブジェクトの現在の行、または**レコード**オブジェクトの**Fields**コレクションに対して行ったすべての変更を保存します。|  
|[UpdateBatch](./updatebatch-method.md)|すべての保留中のバッチ更新をディスクに書き込みます。|  
|[書き込み](./write-method.md)|バイナリデータを **ストリーム** オブジェクトに書き込みます。|  
|[WriteText](./writetext-method.md)|指定したテキスト文字列を **ストリーム** オブジェクトに書き込みます。|  
  
## <a name="see-also"></a>参照  
 [ADO API リファレンス](./ado-api-reference.md)   
 [ADO コレクション](./ado-collections.md)   
 [ADO の動的プロパティ](./ado-dynamic-properties.md)   
 [ADO 列挙定数](./ado-enumerated-constants.md)   
 [付録 B: ADO エラー](../../guide/appendixes/appendix-b-ado-errors.md)   
 [ADO イベント](./ado-events.md)   
 [ADO オブジェクトモデル](./ado-object-model.md)   
 [ADO オブジェクトとインターフェイス](./ado-objects-and-interfaces.md)   
 [ADO のプロパティ](./ado-properties.md)