---
description: ADO のプロパティ
title: ADO のプロパティ |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- properties [ADO]
- ADO properties
ms.assetid: 0ac0d1a7-6c7a-4f4c-b115-428935e0f98b
author: rothja
ms.author: jroth
ms.openlocfilehash: a8a53f4b901209a1ef59be6ca2eb8b531bc52d7c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976283"
---
# <a name="ado-properties"></a>ADO のプロパティ

|プロパティ|説明|  
|-|-|  
|[AbsolutePage](./absolutepage-property-ado.md)|現在のレコードが存在するページを示します。|  
|[AbsolutePosition](./absoluteposition-property-ado.md)|**レコードセット**オブジェクトの現在のレコードの位置を表す序数を示します。|  
|[ActiveCommand](./activecommand-property-ado.md)|関連付けられた**レコードセット**オブジェクトを作成した**Command**オブジェクトを示します。|  
|[ActiveConnection](./activeconnection-property-ado.md)|指定した**コマンド**、**レコードセット**、または**レコード**オブジェクトが現在どの**接続**オブジェクトに属しているかを示します。|  
|[ActualSize](./actualsize-property-ado.md)|フィールドの値の実際の長さを示します。|  
|[属性](./attributes-property-ado.md)|オブジェクトの1つまたは複数の特性を示します。|  
|[BOF と EOF](./bof-eof-properties-ado.md)|**BOF** は、現在のレコード位置が、レコードセットオブジェクトの最初のレコードの前にあることを示します。<br /><br /> **EOF** は、レコードセットオブジェクトの最後のレコードの後に現在のレコード位置があることを示します。|  
|[ブックマーク](./bookmark-property-ado.md)|**レコードセット**オブジェクト内の現在のレコードを一意に識別するブックマークを示します。または、**レコードセット**オブジェクトの現在のレコードを、有効なブックマークによって識別されるレコードに設定します。|  
|[CacheSize](./cachesize-property-ado.md)|メモリ内にローカルにキャッシュされているレコード **セット** オブジェクトのレコードの数を示します。|  
|[章](./chapter-property-ado.md)|**ADORecordsetConstruction**オブジェクトから OLE DB**チャプター**オブジェクトを取得します。値の設定もできます。|  
|[集合](./charset-property-ado.md)|テキスト **ストリーム** の内容を変換する文字セットを示します。|  
|[CommandStream](./commandstream-property-ado.md)|**Command**オブジェクトへの入力として使用されるストリームを示します。|  
|[CommandText](./commandtext-property-ado.md)|プロバイダーに対して発行されるコマンドのテキストを示します。|  
|[CommandTimeOut](./commandtimeout-property-ado.md)|コマンドの実行中に、試行を終了してエラーを生成するまでの待機時間を示します。|  
|[CommandType](./commandtype-property-ado.md)|**Command**オブジェクトの種類を示します。|  
|[ConnectionString プロパティ](./connectionstring-property-ado.md)|データソースへの接続を確立するために使用される情報を示します。|  
|[ConnectionTimeout](./connectiontimeout-property-ado.md)|接続の確立中に、試行を終了してエラーを生成するまでの待機時間を示します。|  
|[Count](./count-property-ado.md)|コレクション内のオブジェクトの数を示します。|  
|[CursorLocation](./cursorlocation-property-ado.md)|カーソルサービスの場所を示します。|  
|[CursorType](./cursortype-property-ado.md)|**レコードセット**オブジェクトで使用されるカーソルの種類を示します。|  
|[DataMember](./datamember-property.md)|**DataSource**プロパティによって参照されるオブジェクトから取得されるデータメンバーの名前を示します。|  
|[DataSource](./datasource-property-ado.md)|**レコードセット**オブジェクトとして表されるデータを格納するオブジェクトを示します。|  
|[DefaultDatabase](./defaultdatabase-property.md)|**接続**オブジェクトの既定のデータベースを示します。|  
|[DefinedSize](./definedsize-property.md)|**フィールド**オブジェクトのデータ容量を示します。|  
|[説明](./description-property.md)|**エラー**オブジェクトについて説明します。|  
|[レクト](./dialect-property.md)|**CommandText**または**commandstream**プロパティを解析するためにプロバイダーが使用する構文と一般規則を示します。|  
|[方向](./direction-property.md)|**パラメーター**が入力パラメーター、出力パラメーター、またはその両方を表すか、またはパラメーターがストアドプロシージャからの戻り値であるかを示します。|  
|[EditMode](./editmode-property.md)|現在のレコードの編集状態を示します。|  
|[EOS](./eos-property.md)|現在の位置がストリームの末尾にあるかどうかを示します。|  
|[Assert](./filter-property.md)|**レコードセット**内のデータのフィルターを示します。|  
|[HelpContext と HelpFile](./helpcontext-helpfile-properties.md)|**エラー**オブジェクトに関連付けられたヘルプファイルとトピックを示します。<br /><br /> **HelpContextID** は、ヘルプファイルのトピックのコンテキスト ID を **Long 型** の値として返します。<br /><br /> **HelpFile** は、ヘルプファイルの完全に解決されたパスに評価される **文字列** 値を返します。|  
|[Index](./index-property.md)|**レコードセット**オブジェクトに現在適用されているインデックスの名前を示します。|  
|[IsolationLevel](./isolationlevel-property.md)|**接続**オブジェクトの分離レベルを示します。|  
|[Item](./item-property-ado.md)|名前または序数を指定して、コレクションの特定のメンバーを示します。|  
|[LineSeparator](./lineseparator-property-ado.md)|テキスト **ストリーム** オブジェクトの行区切り記号として使用されるバイナリ文字を示します。|  
|[LockType](./locktype-property-ado.md)|編集中にレコードに配置されたロックの種類を示します。|  
|[MarshalOptions](./marshaloptions-property-ado.md)|サーバーにマーシャリングされるレコードを示します。|  
|[数](./maxrecords-property-ado.md)|クエリから **レコードセット** に返されるレコードの最大数を示します。|  
|[モード](./mode-property-ado.md)|**接続**、**レコード**、または**ストリーム**オブジェクトのデータを変更するために使用できるアクセス許可を示します。|  
|[名前](./name-property-ado.md)|オブジェクトの名前を示します。|  
|[NativeError](./nativeerror-property-ado.md)|特定の **エラー** オブジェクトのプロバイダー固有のエラーコードを示します。|  
|[Number](./number-property-ado.md)|**エラー**オブジェクトを一意に識別する番号を示します。|  
|[NumericScale](./numericscale-property-ado.md)|**パラメーター**または**フィールド**オブジェクトの数値の小数点以下桁数を示します。|  
|[OriginalValue](./originalvalue-property-ado.md)|変更が行われる前にレコード内に存在していた **フィールド** の値を示します。|  
|[PageCount](./pagecount-property-ado.md)|**Recordset**オブジェクトに格納されているデータのページ数を示します。|  
|[PageSize](./pagesize-property-ado.md)|レコード **セット**内の1ページを表すレコードの数を示します。|  
|[ParentRow](./parentrow-property-ado.md)|行の親が ADO **Record**オブジェクトに変換されるように、 **ADORecordConstruction**オブジェクトの OLE DB **row**オブジェクトのコンテナーを設定します。|  
|[ParentURL](./parenturl-property-ado.md)|現在の**レコード**オブジェクトの親**レコード**を指す絶対 URL 文字列を示します。|  
|[Position](./position-property-ado.md)|**ストリーム**オブジェクト内の現在の位置を示します。|  
|[[精度]](./precision-property-ado.md)|**パラメーター**オブジェクトまたは数値**フィールド**オブジェクトの数値の有効桁数を示します。|  
|[Prepared](./prepared-property-ado.md)|コンパイルされたバージョンのコマンドを実行前に保存するかどうかを示します。|  
|[プロバイダー](./provider-property-ado.md)|**接続**オブジェクトのプロバイダーの名前を示します。|  
|[RecordCount](./recordcount-property-ado.md)|**レコードセット**オブジェクト内のレコードの数を示します。|  
|[RecordType](./recordtype-property-ado.md)|**レコード**オブジェクトの種類を示します。|  
|[行](./row-property-ado.md)|**ADORecordConstruction**オブジェクトからの OLE DB **Row**オブジェクトを取得します。値の設定もできます。|  
|[RowPosition](./rowposition-property-ado.md)|**ADORecordsetConstruction**オブジェクトからの OLE DB **rowposition**オブジェクトを取得します。値の設定もできます。|  
|[[行セット]](./rowset-property-ado.md)|**ADORecordsetConstruction**オブジェクトの/から OLE DB**行セット**オブジェクトを取得します。値の設定もできます。|  
|[ソース (ADO エラー)](./source-property-ado-error.md)|最初にエラーを生成したオブジェクトまたはアプリケーションの名前を示します。|  
|[ソース (ADO レコード)](./source-property-ado-record.md)|**レコード**オブジェクトによって表されるエンティティを示します。|  
|[変換元 (ADO レコードセット)](./source-property-ado-recordset.md)|**レコードセット**オブジェクトのデータのソースを示します。|  
|[SQLState](./sqlstate-property.md)|特定の **エラー** オブジェクトの SQL 状態を示します。|  
|[State](./state-property-ado.md)|オブジェクトの状態が開いているか閉じられているかにかかわらず、適用可能なすべてのオブジェクトを示します。 オブジェクトの現在の状態が接続、実行中、または取得中かどうかにかかわらず、非同期メソッドを実行するすべての適用可能なオブジェクトに対してを示します。|  
|[状態 (ADO フィールド)](./status-property-ado-field.md)|**フィールド**オブジェクトの状態を示します。|  
|[状態 (ADO レコードセット)](./status-property-ado-recordset.md)|バッチ更新やその他の一括操作に関する現在のレコードの状態を示します。|  
|[StayInSync](./stayinsync-property.md)|親の行位置が変更されたときに、基になる子レコード (つまり、*チャプター*) への参照が変更されるかどうかを階層**レコードセット**オブジェクトで示します。|  
|[Stream プロパティ](./stream-property.md)|**ADOStreamConstruction**オブジェクトからの OLE DB**ストリーム**オブジェクトを取得します。値の設定もできます。|  
|[Type](./type-property-ado.md)|**パラメーター**、**フィールド**、または**プロパティ**オブジェクトの操作の種類またはデータ型を示します。|  
|[型 (ADO ストリーム)](./type-property-ado-stream.md)|**ストリーム**に格納されているデータの型 (バイナリまたはテキスト) を示します。|  
|[UnderlyingValue](./underlyingvalue-property.md)|**Field**オブジェクトのデータベースの現在の値を示します。|  
|[値](./value-property-ado.md)|**フィールド**、**パラメーター**、または**プロパティ**オブジェクトに割り当てられた値を示します。|  
|[Version](./version-property-ado.md)|ADO のバージョン番号を示します。|  
  
## <a name="see-also"></a>参照  
 [ADO API リファレンス](./ado-api-reference.md)   
 [ADO コレクション](./ado-collections.md)   
 [ADO の動的プロパティ](./ado-dynamic-properties.md)   
 [ADO 列挙定数](./ado-enumerated-constants.md)   
 [付録 B: ADO エラー](../../guide/appendixes/appendix-b-ado-errors.md)   
 [ADO イベント](./ado-events.md)   
 [ADO メソッド](./ado-methods.md)   
 [ADO オブジェクトモデル](./ado-object-model.md)   
 [ADO のオブジェクトとインターフェイス](./ado-objects-and-interfaces.md)