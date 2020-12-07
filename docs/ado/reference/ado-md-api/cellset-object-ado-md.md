---
description: CellSet オブジェクト (ADO MD)
title: Cellset オブジェクト (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset
helpviewer_keywords:
- Cellset object [ADO MD]
ms.assetid: 5e2452c0-cac0-49b2-8099-836c35794d50
author: rothja
ms.author: jroth
ms.openlocfilehash: 411ed21d5fecf5c9791a5d96aac60724e7446958
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987153"
---
# <a name="cellset-object-ado-md"></a>CellSet オブジェクト (ADO MD)
多次元クエリの結果を表します。 これは、キューブまたは他のセルセットから選択されたセルのコレクションです。  
  
## <a name="remarks"></a>解説  
 **セルセット**内のデータは、配列に似た直接アクセスを使用して取得されます。 特定のメンバーにドリルダウンして、そのメンバーに関するデータを取得することができます。 たとえば、次のコードは、という名前のセルセットの最初の軸の最初の位置にある最初のメンバーのキャプションを返し `cst` ます。  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
 セルセット内には、現在のセルの概念はありません。 代わりに、 [Item](./item-property-ado-md-cellset.md) プロパティは、セルセットから特定の [セル](./cell-object-ado-md.md) オブジェクトを取得します。 **項目**プロパティの引数によって、取得するセルが決まります。 セルの一意の序数値を指定できます。 セルは、セルセットの各軸に沿った位置番号を使用して取得することもできます。 セルの取得の詳細については、 [Item](./item-property-ado-md-cellset.md) プロパティを参照してください。  
  
 **Cellset**オブジェクトのコレクション、メソッド、およびプロパティを使用して、次の操作を実行できます。  
  
-   [ActiveConnection](./activeconnection-property-ado-md.md)プロパティを設定して、開いている接続を**セルセット**オブジェクトに関連付けます。  
  
-   [Open](./open-method-ado-md.md)メソッドを使用して多次元クエリの結果を実行および取得します。  
  
-   [アイテム](./item-property-ado-md-cellset.md)プロパティを使用して、セル**セット**から**セル**を取得します。  
  
-   [Axes](./axes-collection-ado-md.md)コレクションを使用して**セルセット**を定義する[軸](./axis-object-ado-md.md)オブジェクトを返します。  
  
-   [Filteraxis](./filteraxis-property-ado-md.md)プロパティを使用して、**セルセット**のデータをフィルター処理するために使用されるディメンションに関する情報を取得します。  
  
-   [Source](./source-property-ado-md.md)プロパティを使用して**セルセット**を定義するために使用するクエリを返します。値の設定もできます。  
  
-   [State](./state-property-ado-md.md)プロパティを使用して、**セルセット**(開く、closed、実行中、または接続) の現在の状態を返します。  
  
-   [Close](./close-method-ado-md.md)メソッドを使用して、開いている**セルセット**を閉じます。  
  
-   標準の ADO[プロパティ](../ado-api/properties-collection-ado.md)コレクションを使用して、**セルセット**に関するプロバイダー固有の情報を取得します。  
  
 ここでは、次のトピックについて説明します。  
  
-   [プロパティ、メソッド、およびイベント](./cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [セルセットの例 (VB)](./cellset-example-vb.md)   
 [Axes コレクション (ADO MD)](./axes-collection-ado-md.md)   
 [Cell オブジェクト (ADO MD)](./cell-object-ado-md.md)   
 [Connection オブジェクト (ADO)](../ado-api/connection-object-ado.md)   
 [Properties コレクション (ADO)](../ado-api/properties-collection-ado.md)