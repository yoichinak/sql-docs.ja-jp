---
description: Open メソッド (ADO MD)
title: Open メソッド (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Open
- Cellset::Open
helpviewer_keywords:
- Open method [ADO MD]
ms.assetid: a87d8080-a238-45e5-bc80-9a8625b3810f
author: rothja
ms.author: jroth
ms.openlocfilehash: 5c7b403ed89ae9933b4169af4e53921205318ccd
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986233"
---
# <a name="open-method-ado-md"></a>Open メソッド (ADO MD)
多次元クエリの結果を取得し、結果を [セルセット](./cellset-object-ado-md.md)に返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Cellset.Open Source, ActiveConnection  
```  
  
#### <a name="parameters"></a>パラメーター  
 *ソース*  
 省略可能。 多次元式 (MDX) クエリなど、有効な多次元クエリに評価される **バリアント** です。 *Source*引数は、 [source](./source-property-ado-md.md)プロパティに対応しています。 MDX の詳細については、Microsoft Data Access Components SDK の [オンライン分析処理 (OLAP) の OLE DB](/previous-versions/windows/desktop/ms717005(v=vs.85)) に関するドキュメントを参照してください。  
  
 *ActiveConnection*  
 省略可能。 有効な ADO[接続](../ado-api/connection-object-ado.md)オブジェクト変数名または接続の定義のいずれかを指定する文字列に評価される**バリアント**。 *ActiveConnection*引数は、[セルセット](./cellset-object-ado-md.md)オブジェクトを開くための接続を指定します。 この引数に対して接続定義を渡すと、指定されたパラメーターを使用して新しい接続が開かれます。 *ActiveConnection*引数は、 [ActiveConnection](./activeconnection-property-ado-md.md)プロパティに対応しています。  
  
## <a name="remarks"></a>解説  
 **Open**メソッドは、パラメーターのいずれかが省略されていて、それに対応するプロパティ値が**セル**セットを開こうとする前に設定されていない場合に、エラーを生成します。  
  
## <a name="applies-to"></a>適用対象  
 [CellSet オブジェクト (ADO MD)](./cellset-object-ado-md.md)  
  
## <a name="see-also"></a>参照  
 [セルセットの例 (VB)](./cellset-example-vb.md)   
 [ActiveConnection プロパティ (ADO MD)](./activeconnection-property-ado-md.md)   
 [Close メソッド (ADO MD)](./close-method-ado-md.md)   
 [Connection オブジェクト (ADO)](../ado-api/connection-object-ado.md)   
 [Source プロパティ (ADO MD)](./source-property-ado-md.md)   
 [State プロパティ (ADO MD)](./state-property-ado-md.md)