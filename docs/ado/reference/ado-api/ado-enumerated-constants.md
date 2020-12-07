---
description: ADO の列挙定数
title: ADO 列挙定数 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerated constants [ADO]
ms.assetid: c97ed131-1a93-463c-9e61-22f029b0c474
author: rothja
ms.author: jroth
ms.openlocfilehash: c3c19b98cbb000abc93755c3de43ac5420db164d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976483"
---
# <a name="ado-enumerated-constants"></a>ADO の列挙定数
デバッグを支援するために、ADO 列挙体には各定数の値が一覧表示されます。 ただし、この値は純粋にアドバイザリであり、あるリリースの ADO から別のリリースに変更される可能性があります。 コードは、各列挙定数の実際の値ではなく、名前のみに依存する必要があります。  
  
|定数|説明|  
|-|-|  
|[ADCPROP_ASYNCTHREADPRIORITY_ENUM](./adcprop-asyncthreadpriority-enum.md)|RDS **レコードセット** オブジェクトの場合は、データを取得する非同期スレッドの実行の優先度を指定します。|  
|[ADCPROP_AUTORECALC_ENUM](./adcprop-autorecalc-enum.md)|**MSDataShape**プロバイダーが階層**レコードセット**の集計列と計算列を再計算するタイミングを指定します。|  
|[ADCPROP_UPDATECRITERIA_ENUM](./adcprop-updatecriteria-enum.md)|**レコードセット**オブジェクトを使用してデータソースの行をオプティミスティック更新するときに、競合を検出するために使用できるフィールドを指定します。|  
|[ADCPROP_UPDATERESYNC_ENUM](./adcprop-updateresync-enum.md)|**UpdateBatch**メソッドの後に暗黙の再**同期**メソッド操作が続くかどうかを指定します。それを行う場合は、その操作のスコープを指定します。|  
|[AffectEnum](./affectenum.md)|操作の影響を受けるレコードを指定します。|  
|[BookmarkEnum](./bookmarkenum.md)|操作の開始位置を示すブックマークを指定します。|  
|[CommandTypeEnum](./commandtypeenum.md)|コマンド引数をどのように解釈するかを指定します。|  
|[CompareEnum](./compareenum.md)|ブックマークによって表される2つのレコードの相対位置を指定します。|  
|[ConnectModeEnum](./connectmodeenum.md)|**接続**のデータを変更したり、**レコード**を開いたり、**レコード**および**ストリーム**オブジェクトの**Mode**プロパティの値を指定したりするために使用できるアクセス許可を指定します。|  
|[ConnectOptionEnum](./connectoptionenum.md)|**接続オブジェクト**の**Open**メソッドが、接続が確立された (同期的に) かそれより前 (非同期) に戻る必要があるかどうかを指定します。|  
|[ConnectPromptEnum](./connectpromptenum.md)|ODBC データソースへの接続を開くときに、ダイアログボックスを表示して、不足しているパラメーターを確認するかどうかを指定します。|  
|[CopyRecordOptionsEnum](./copyrecordoptionsenum.md)|**Copyrecord**メソッドの動作を指定します。|  
|[CursorLocationEnum](./cursorlocationenum.md)|カーソルエンジンの場所を指定します。|  
|[CursorOptionEnum](./cursoroptionenum.md)|**サポート**メソッドがテストする必要がある機能を指定します。|  
|[CursorTypeEnum](./cursortypeenum.md)|**レコードセット**オブジェクトで使用されるカーソルの種類を指定します。|  
|[DataTypeEnum](./datatypeenum.md)|**フィールド**、**パラメーター**、または**プロパティ**のデータ型を指定します。|  
|[EditModeEnum](./editmodeenum.md)|レコードの編集状態を指定します。|  
|[ErrorValueEnum](./errorvalueenum.md)|ADO ランタイムエラーの種類を指定します。|  
|[EventReasonEnum](./eventreasonenum.md)|イベントの発生原因となった理由を指定します。|  
|[EventStatusEnum](./eventstatusenum.md)|イベントの実行の現在の状態を指定します。|  
|[ExecuteOptionEnum](./executeoptionenum.md)|プロバイダーがコマンドを実行する方法を指定します。|  
|[FieldEnum](./fieldenum.md)|**レコード**オブジェクトの**fields**コレクションで参照される特殊なフィールドを指定します。|  
|[FieldAttributeEnum](./fieldattributeenum.md)|**Field**オブジェクトの1つまたは複数の属性を指定します。|  
|[FieldStatusEnum](./fieldstatusenum.md)|**フィールド**オブジェクトの状態を指定します。|  
|[FilterGroupEnum](./filtergroupenum.md)|レコード **セット**からフィルター選択するレコードのグループを指定します。|  
|[GetRowsOptionEnum](./getrowsoptionenum.md)|レコード **セット**から取得するレコードの数を指定します。|  
|[IsolationLevelEnum](./isolationlevelenum.md)|**接続**オブジェクトのトランザクション分離レベルを指定します。|  
|[LineSeparatorsEnum](./lineseparatorsenum.md)|テキスト **ストリーム** オブジェクトの行区切り記号として使用される文字を指定します。|  
|[LockTypeEnum](./locktypeenum.md)|編集中にレコードに適用されるロックの種類を指定します。|  
|[MarshalOptionsEnum](./marshaloptionsenum.md)|サーバーに返すレコードを指定します。|  
|[MoveRecordOptionsEnum](./moverecordoptionsenum.md)|**Record**オブジェクトの**MoveRecord**メソッドの動作を指定します。|  
|[ObjectStateEnum](./objectstateenum.md)|オブジェクトが開いているか閉じられているか、データソースに接続しているか、コマンドを実行しているか、データをフェッチしているかを指定します。|  
|[ParameterAttributesEnum](./parameterattributesenum.md)|**パラメーター**オブジェクトの属性を指定します。|  
|[ParameterDirectionEnum](./parameterdirectionenum.md)|**パラメーター**が入力パラメーター、出力パラメーター、またはその両方を表すか、またはパラメーターがストアドプロシージャからの戻り値であるかを指定します。|  
|[PersistFormatEnum](./persistformatenum.md)|**レコードセット**を保存する形式を指定します。|  
|[PositionEnum](./positionenum.md)|レコード **セット**内のレコードポインターの現在位置を指定します。|  
|[PropertyAttributesEnum](./propertyattributesenum.md)|**プロパティ**オブジェクトの属性を指定します。|  
|[RecordCreateOptionsEnum](./recordcreateoptionsenum.md)|**Record**オブジェクト**Open**メソッドに対して、既存の**レコード**を開くか、新しい**レコード**を作成するかを指定します。|  
|[RecordOpenOptionsEnum](./recordopenoptionsenum.md)|**レコード**を開くためのオプションを指定します。 これらの値は、OR 演算子を使用して組み合わせることができます。|  
|[RecordStatusEnum](./recordstatusenum.md)|バッチ更新やその他の一括操作に関して、レコードの状態を指定します。|  
|[RecordTypeEnum](./recordtypeenum.md)|**レコード**オブジェクトの種類を指定します。|  
|[ResyncEnum](./resyncenum.md)|再 **同期**の呼び出しによって基になる値を上書きするかどうかを指定します。|  
|[SaveOptionsEnum](./saveoptionsenum.md)|**ストリーム**オブジェクトから保存するときにファイルを作成するか上書きするかを指定します。 値は AND 演算子と組み合わせることができます。|  
|[SchemaEnum](./schemaenum.md)|**OpenSchema**メソッドによって取得されるスキーマ**レコードセット**の種類を指定します。 レコード **セット**内のレコード検索の方向を指定します。|  
|[SearchDirectionEnum](./searchdirectionenum.md)|レコード **セット**内のレコード検索の方向を指定します。 実行する **シーク** の種類を指定します。|  
|[SeekEnum](./seekenum.md)|実行する **シーク** の種類を指定します。 **ストリーム**オブジェクトを開くためのオプションを指定します。 値は AND 演算子と組み合わせることができます。|  
|[StreamOpenOptionsEnum](./streamopenoptionsenum.md)|**ストリーム**オブジェクトを開くためのオプションを指定します。 値は AND 演算子と組み合わせることができます。 ストリーム全体または次の行を **ストリーム** オブジェクトから読み取るかどうかを指定します。|  
|[StreamReadEnum](./streamreadenum.md)|ストリーム全体または次の行を **ストリーム** オブジェクトから読み取るかどうかを指定します。 **ストリーム**オブジェクトに格納されているデータの型を指定します。|  
|[StreamTypeEnum](./streamtypeenum.md)|**ストリーム**オブジェクトに格納されているデータの型を指定します。 **ストリーム**オブジェクトに書き込まれる文字列に行の区切り記号を追加するかどうかを指定します。|  
|[StreamWriteEnum](./streamwriteenum.md)|**ストリーム**オブジェクトに書き込まれる文字列に行の区切り記号を追加するかどうかを指定します。 **レコードセット**を文字列として取得する場合の形式を指定します。|  
|[StringFormatEnum](./stringformatenum.md)|**レコードセット**を文字列として取得する場合の形式を指定します。 **接続**オブジェクトのトランザクション属性を指定します。|  
|[XactAttributeEnum](./xactattributeenum.md)|**接続**オブジェクトのトランザクション属性を指定します。|  
  
## <a name="see-also"></a>参照  
 [ADO API リファレンス](./ado-api-reference.md)   
 [ADO コレクション](./ado-collections.md)   
 [ADO の動的プロパティ](./ado-dynamic-properties.md)   
 [付録 B: ADO エラー](../../guide/appendixes/appendix-b-ado-errors.md)   
 [ADO イベント](./ado-events.md)   
 [ADO メソッド](./ado-methods.md)   
 [ADO オブジェクトモデル](./ado-object-model.md)   
 [ADO オブジェクトとインターフェイス](./ado-objects-and-interfaces.md)   
 [ADO のプロパティ](./ado-properties.md)