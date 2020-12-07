---
description: データ シェイプに必要なプロバイダー
title: データシェイプの必須プロバイダー |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping
- data shaping [ADO], providers required
ms.assetid: d49d48d2-ac2d-4c11-895c-5a149b444620
author: rothja
ms.author: jroth
ms.openlocfilehash: bd2829c49adb318ae80eeefd2ec2913fd8620d2b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979803"
---
# <a name="required-providers-for-data-shaping"></a>データ シェイプに必要なプロバイダー
通常、データシェイプには2つのプロバイダーが必要です。 サービスプロバイダー、 [OLE DB 用のデータ整形サービス](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)はデータの整形機能を提供し、SQL Server の OLE DB プロバイダーなどのデータプロバイダーが、整形された [レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)を設定するためのデータ行を提供します。  
  
 サービスプロバイダーの名前 (MSDataShape) は、 [接続](../../../ado/reference/ado-api/connection-object-ado.md) オブジェクト [プロバイダー](../../../ado/reference/ado-api/provider-property-ado.md) プロパティの値、または接続文字列キーワード "provider = MSDataShape;" の値として指定できます。  
  
 データプロバイダーの名前は**Data Provider**動的プロパティの値として指定できます。このプロパティは、OLE DB 用のデータシェイプサービスまたは接続文字列キーワード "**Data Provider =** _Provider_" によって**接続**オブジェクト[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクションに追加されます。  
  
 **レコードセット**に値が設定されていない場合 (たとえば、新しいキーワードを使用して列が作成される作成済みの**レコードセット**の場合など)、データプロバイダーは必要ありません。 その場合は、"**Data Provider =** none;" を指定します。  
  
## <a name="example"></a>例  
  
```  
Dim cnn As New ADODB.Connection  
cnn.Provider = "MSDataShape"  
cnn.Open "Data Provider=SQLOLEDB;Integrated Security=SSPI;Database=Northwind"  
```  
  
## <a name="see-also"></a>参照  
 [データシェイプの例](../../../ado/guide/data/data-shaping-example.md)   
 [仮形の文法](../../../ado/guide/data/formal-shape-grammar.md)   
 [一般的な Shape コマンド](../../../ado/guide/data/shape-commands-in-general.md)
