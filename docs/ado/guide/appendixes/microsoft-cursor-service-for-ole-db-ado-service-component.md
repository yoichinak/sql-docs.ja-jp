---
description: OLE DB 用 Microsoft Cursor Service (ADO サービスコンポーネント)
title: Microsoft Cursor Service for OLE DB (ADO サービスコンポーネント) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], cursor service for OLE DB
- cursor service for OLE DB [ADO]
ms.assetid: 420d0989-7cfb-4c66-a7b5-f4199d13165d
author: rothja
ms.author: jroth
ms.openlocfilehash: 02eaad96593af153b1692beed4bcf846ff92ab7f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991093"
---
# <a name="microsoft-cursor-service-for-ole-db-overview"></a>OLE DB 用 Microsoft Cursor Service の概要
Microsoft Cursor Service for OLE DB は、データプロバイダーのカーソルサポート機能を補足します。 その結果、ユーザーは、すべてのデータプロバイダーの比較的一様な機能を認識します。

 カーソルサービスは動的プロパティを使用可能にし、特定のメソッドの動作を拡張します。 たとえば、"動的に [最適化](../../reference/ado-api/optimize-property-dynamic-ado.md) " プロパティを使用すると、 [Find](../../reference/ado-api/find-method-ado.md) メソッドなどの特定の操作を容易にするために一時インデックスを作成できます。

 カーソルサービスにより、すべての場合にバッチ更新がサポートされます。 また、静的カーソルなど、データプロバイダーが使用できるカーソルの数が少ない場合に、動的カーソルなど、より多くの機能を持つカーソルの種類をシミュレートします。

## <a name="keyword"></a>キーワード
 このサービスコンポーネントを呼び出すには、 [レコードセット](../../reference/ado-api/recordset-object-ado.md) または [接続](../../reference/ado-api/connection-object-ado.md) オブジェクトの [カーソルの場所](../../reference/ado-api/cursorlocation-property-ado.md) プロパティを **adUseClient**に設定します。

```vb
connection.CursorLocation=adUseClient
recordset.CursorLocation=adUseClient
```

## <a name="dynamic-properties"></a>動的プロパティ
 OLE DB のカーソルサービスが呼び出されると、次の動的プロパティが **レコードセット** オブジェクトの [properties](../../reference/ado-api/properties-collection-ado.md) コレクションに追加されます。 **接続**および**レコードセット**オブジェクトの動的プロパティの完全な一覧は、「 [ADO 動的プロパティインデックス](../../reference/ado-api/ado-dynamic-property-index.md)」に記載されています。 関連する OLE DB プロパティ名 (適切な場合) は、ADO プロパティ名の後にかっこで囲まれています。

 一部の動的プロパティに対する変更は、カーソルサービスが呼び出された後に、基になるデータソースからは認識されません。 たとえば、**レコードセット**の*コマンドタイムアウト*プロパティを設定しても、基になるデータプロバイダーには表示されません。

```vb

Recordset1.CursorLocation = adUseClient     'invokes cursor service
Recordset1.Open "authors", _
    "Provider=SQLOLEDB;Data Source=DBServer;User Id=MyUserID;" & _
    "Password=MyPassword;Initial Catalog=pubs;",,adCmdTable
Recordset1.Properties.Item("Command Time out") = 50
' 'Command Time out' property on DBServer is still default (30).

```

 アプリケーションでカーソルサービスが必要であるのに、基になるプロバイダーで動的プロパティを設定する必要がある場合は、カーソルサービスを呼び出す前にプロパティを設定します。 Command オブジェクトのプロパティ設定は、カーソル位置に関係なく、常に基になるデータプロバイダーに渡されます。 したがって、コマンドオブジェクトを使用して、いつでもプロパティを設定できます。

> [!NOTE]
>  動的プロパティ DBPROP_SERVERDATAONINSERT は、基になるデータプロバイダーでサポートされている場合でも、cursor service ではサポートされていません。

|プロパティ名|説明|
|-------------------|-----------------|
|自動再計算 (DBPROP_ADC_AUTORECALC)|データシェイプサービスで作成されたレコードセットの場合、この値は計算列および集計列を計算する頻度を示します。 既定値 (値 = 1) は、データ整形サービスによって値が変更されたと判断されるたびに再計算されます。 値が0の場合、計算列または集計列は、階層が最初に構築されたときにのみ計算されます。|
|バッチサイズ (DBPROP_ADC_BATCHSIZE)|データストアに送信される前にバッチ処理できる update ステートメントの数を示します。 バッチ内のステートメントが多くなるほど、データストアへのラウンドトリップが減少します。|
|子行のキャッシュ (DBPROP_ADC_CACHECHILDROWS)|データシェイプサービスで作成されたレコードセットの場合、この値は、子レコードセットが後で使用できるようにキャッシュに格納されているかどうかを示します。|
|カーソルエンジンのバージョン (DBPROP_ADC_CEVER)|使用されているカーソルサービスのバージョンを示します。|
|変更の状態を維持する (DBPROP_ADC_MAINTAINCHANGESTATUS)|複数のテーブルの結合で1つ以上の行を再同期するために使用されるコマンドのテキストを示します。|
|[最適化](../../reference/ado-api/optimize-property-dynamic-ado.md)|インデックスを作成する必要があるかどうかを示します。 **True**に設定されている場合、は、特定の操作の実行を向上させるために、インデックスの一時的な作成を承認します。|
|[名前のリシェイプ](../../reference/ado-api/reshape-name-property-dynamic-ado.md)|**レコードセット**の名前を示します。 現在の、またはそれ以降のデータシェイプコマンド内で参照できます。|
|[再同期コマンド](../../reference/ado-api/resync-command-property-dynamic-ado.md)|[一意のテーブル](../../reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)プロパティが有効な場合に、再[同期](../../reference/ado-api/resync-method.md)メソッドによって使用されるカスタムコマンド文字列を示します。|
|[一意のカタログ](../../reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**一意のテーブル**プロパティで参照されるテーブルを含むデータベースの名前を示します。|
|[一意のスキーマ](../../reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|**一意のテーブル**プロパティで参照されるテーブルの所有者の名前を示します。|
|[Unique Table](../../reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md)|挿入、更新、または削除によって変更できる複数のテーブルから作成された **レコードセット** 内の1つのテーブルの名前を示します。|
|更新条件 (DBPROP_ADC_UPDATECRITERIA)|更新中に発生した競合の処理に使用される **where** 句内のフィールドを示します。|
|再[同期の更新](../../reference/ado-api/update-resync-property-dynamic-ado.md)(DBPROP_ADC_UPDATERESYNC)|**一意のテーブル**プロパティが有効な場合に、 [UpdateBatch](../../reference/ado-api/updatebatch-method.md)メソッド (およびその動作) の後に再**同期**メソッドが暗黙的に呼び出されるかどうかを示します。|

 **プロパティ**コレクションのインデックスとして名前を指定して、動的プロパティを設定または取得することもできます。 たとえば、 [Optimize](../../reference/ado-api/optimize-property-dynamic-ado.md) 動的プロパティの現在の値を取得して印刷し、次のように新しい値を設定します。

```vb
Debug.Print rs.Properties("Optimize")
rs.Properties("Optimize") = True
```

## <a name="built-in-property-behavior"></a>組み込みプロパティの動作
 OLE DB 用の Cursor Service は、特定の組み込みプロパティの動作にも影響します。

|プロパティ名|説明|
|-------------------|-----------------|
|[CursorType](../../reference/ado-api/cursortype-property-ado.md)|**レコードセット**で使用できるカーソルの種類を補足します。|
|[LockType](../../reference/ado-api/locktype-property-ado.md)|**レコードセット**で使用可能なロックの種類を補足します。 バッチ更新を有効にします。|
|[Sort](../../reference/ado-api/sort-property.md)|**レコードセット**が並べ替えられる1つ以上のフィールド名と、各フィールドを昇順と降順のどちらで並べ替えるかを指定します。|

## <a name="method-behavior"></a>メソッドの動作
 OLE DB 用の Cursor Service は、 [Field](../../reference/ado-api/field-object.md) オブジェクトの [Append](../../reference/ado-api/append-method-ado.md) メソッドの動作に有効または影響を及ぼします。 **レコードセット** オブジェクトの [Open](../../reference/ado-api/open-method-ado-recordset.md)、 [Resync](../../reference/ado-api/resync-method.md)、 [UpdateBatch](../../reference/ado-api/updatebatch-method.md)、および [Save](../../reference/ado-api/save-method.md) メソッドがあります。