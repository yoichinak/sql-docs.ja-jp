---
description: Record オブジェクト (ADO)
title: Record オブジェクト (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Record
helpviewer_keywords:
- Record object [ADO]
ms.assetid: db83ed2c-a8e3-460c-8682-64667e4d5d01
author: rothja
ms.author: jroth
ms.openlocfilehash: 6066d43bfa52d65ee133fd748f76fc651fac7379
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989863"
---
# <a name="record-object-ado"></a>Record オブジェクト (ADO)
[レコードセット](./recordset-object-ado.md)またはデータプロバイダーの行、またはファイルやディレクトリなどの半構造化データプロバイダーによって返されるオブジェクトを表します。  
  
## <a name="remarks"></a>解説  
 **レコード**オブジェクトは1行のデータを表し、1行の**レコードセット**と概念的に似ています。 プロバイダーの機能によっては、 **レコード** オブジェクトが1行の **レコードセット**ではなく、プロバイダーから直接返される場合があります。たとえば、1つの行のみを選択する SQL クエリが実行された場合などです。 または、 **レコード** オブジェクトを **レコードセット** オブジェクトから直接取得することもできます。 または、 **レコード** をプロバイダーから、Microsoft Exchange OLE DB プロバイダーなどの半構造化データに直接返すことができます。  
  
 **レコードオブジェクト**に関連付けられているフィールドは、**レコード**オブジェクトの[フィールド](./fields-collection-ado.md)コレクションを使用して表示できます。 ADO では、**レコード**オブジェクトの**Fields**コレクションで、レコード**セット**、 **SafeArray**、スカラー値を含むオブジェクト値列を使用できます。  
  
 **レコード**オブジェクトが**レコードセット**内の行を表している場合、 [Source](./source-property-ado-record.md)プロパティを使用して元の**レコードセット**に戻ることができます。  
  
 **レコード**オブジェクトは、 [Microsoft OLE DB Provider for Internet Publishing](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)などの半構造化データプロバイダーが、ツリー構造の名前空間をモデル化するために使用することもできます。 ツリー内の各ノードは、関連付けられた列を持つ **レコード** オブジェクトです。 列は、そのノードの属性とその他の関連情報を表すことができます。 **レコード**オブジェクトは、リーフノードと、ツリー構造内の非リーフノードの両方を表すことができます。 非リーフノードには、そのコンテンツとして他のノードがありますが、リーフノードにはそのような内容が含まれていません。 リーフノードには通常、バイナリストリームのデータが含まれており、非リーフノードには既定のバイナリストリームが関連付けられている場合もあります。 **レコード**オブジェクトのプロパティは、ノードの種類を識別します。  
  
 また、 **レコード** オブジェクトは、階層的に整理されたデータを移動するための別の方法も表します。 大きなツリー構造内の特定のサブツリーのルートを表す **レコード** オブジェクトを作成し、新しい **レコード** オブジェクトを開いて子ノードを表すことができます。  
  
 リソース (ファイルやディレクトリなど) は絶対 URL で一意に識別できます。 絶対 URL を使用して**レコード**を開くと、[接続](./connection-object-ado.md)オブジェクトが暗黙的に作成され、**レコード**オブジェクトに設定されます。 **Connection**オブジェクトは、 [ActiveConnection](./activeconnection-property-ado.md)プロパティを使用して**Record**オブジェクトに明示的に設定できます。 **接続**オブジェクトを使用してアクセスできるファイルとディレクトリは、**レコード**操作が発生する*コンテキスト*を定義します。  
  
 **レコード**オブジェクトのデータ変更およびナビゲーションメソッドは、相対 url も受け入れます。これは、絶対 url または**接続**オブジェクトコンテキストを使用してリソースを開始点として検索します。  
  
> [!NOTE]
>  Http スキームを使用する Url は、 [インターネット公開のために Microsoft OLE DB プロバイダー](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)を自動的に呼び出します。 詳細については、「 [絶対 url と相対 url](../../guide/data/absolute-and-relative-urls.md)」を参照してください。  
  
 **接続**オブジェクトは、各**レコード**オブジェクトに関連付けられています。 そのため、 **レコード** オブジェクトの操作は、 **接続** オブジェクトのトランザクションメソッドを呼び出すことによって、トランザクションの一部にすることができます。  
  
 **レコード**オブジェクトは ADO イベントをサポートしていないため、通知に応答しません。  
  
 **レコード**オブジェクトのメソッドとプロパティを使用して、次の操作を実行できます。  
  
-   [ActiveConnection](./activeconnection-property-ado.md)プロパティを使用して、関連付けられている**接続**オブジェクトを設定または返します。  
  
-   [Mode](./mode-property-ado.md)プロパティを使用してアクセス許可を指定します。  
  
-   **レコード**によって表されるリソースが存在する場合、そのディレクトリの Url を[parenturl](./parenturl-property-ado.md)プロパティと共に返します。  
  
-   [ソース](./source-property-ado-record.md)プロパティを使用して**レコード**を派生させる絶対 url、相対 Url、または**レコードセット**を指定します。  
  
-   [State](./state-property-ado.md)プロパティを使用して、**レコード**の現在の状態を示します。  
  
-   **Record**  -  [RecordType](./recordtype-property-ado.md)プロパティを使用して、*単純*、*コレクション*、または*構造化ドキュメント*のレコードの種類を示します。  
  
-   [Cancel](./cancel-method-ado.md)メソッドを使用して非同期操作の実行を停止します。  
  
-   [Close](./close-method-ado.md)メソッドを使用して、データソースの**レコード**の関連付けを解除します。  
  
-   **レコード**で表されるファイルまたはディレクトリを、 [copyrecord](./copyrecord-method-ado.md)メソッドを使用して別の場所にコピーします。  
  
-   [DeleteRecord](./deleterecord-method-ado.md)メソッドを使用して、**レコード**で表されるファイル、またはディレクトリとサブディレクトリを削除します。  
  
-   **レコード**によって表されるエンティティのサブディレクトリとファイルを表す行を含む**レコードセット**を、 [getchildren](./getchildren-method-ado.md)メソッドを使用して開きます。  
  
-   [MoveRecord](./moverecord-method-ado.md)メソッドを使用して、**レコード**で表されるファイルまたはディレクトリとサブディレクトリを別の場所に移動 (名前変更) します。  
  
-   **レコード**を既存のデータソースに関連付けるか、 [Open](./open-method-ado-record.md)メソッドを使用して新しいファイルまたはディレクトリを作成します。  
  
 **レコード**オブジェクトは、スクリプトに対して安全です。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Record オブジェクトのプロパティ、メソッド、およびイベント](./record-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Fields コレクション (ADO)](./fields-collection-ado.md)   
 [Properties コレクション (ADO)](./properties-collection-ado.md)   
 [レコードとストリーム](../../guide/data/records-and-streams.md)   
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)