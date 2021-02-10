---
description: OLE DB 用の Microsoft データ整形サービス (ADO サービスプロバイダー)
title: OLE DB 用の Microsoft データ整形サービス (ADO サービスプロバイダー) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], data shaping service for OLE DB
- data shaping service for OLE DB [ADO]
ms.assetid: 523009ce-e01b-4e2d-a7df-816d7688aff0
author: rothja
ms.author: jroth
ms.openlocfilehash: a83d37c301d34c273514e4d6eb0551bc86429bd4
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100029376"
---
# <a name="microsoft-data-shaping-service-for-ole-db-overview"></a>OLE DB 用の Microsoft データ整形サービスの概要
> [!IMPORTANT]
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、アプリケーションは XML を使用する必要があります。

 OLE DB サービスプロバイダー用の Microsoft データ整形サービスは、データプロバイダーからの階層構造の (整形された) [レコードセット](../../reference/ado-api/recordset-object-ado.md) オブジェクトの構築をサポートしています。

## <a name="provider-keyword"></a>Provider キーワード
 OLE DB のデータ整形サービスを呼び出すには、接続文字列に次のキーワードと値を指定します。

```vb
"Provider=MSDataShape"
```

## <a name="dynamic-properties"></a>動的プロパティ
 このサービスプロバイダーが呼び出されると、次の動的プロパティが[Connection](../../reference/ado-api/connection-object-ado.md)オブジェクトの[properties](../../reference/ado-api/properties-collection-ado.md)コレクションに追加されます。

|動的プロパティ名|説明|
|---------------------------|-----------------|
|**一意のリシェイプ名**|**リシェイプ名** プロパティの値が重複している **レコードセット** オブジェクトを使用できるかどうかを示します。 この動的プロパティが **True** で、既存の **レコードセット** と同じユーザー指定のリシェイプ名で新しい **レコードセット** が作成された場合、**新しいレコードセットオブジェクトの** リシェイプ名が変更され、一意になります。 このプロパティが **False** で、既存の **レコードセット** と同じユーザー指定のリシェイプ名で新しい **レコードセット** が作成された場合、両方の **レコードセット** オブジェクトのリシェイプ名は同じになります。 したがって、両方のレコードセットが存在する限り、どちらの **レコードセット** もリシェイプできません。<br /><br /> プロパティの既定値は **False** です。|
|**Data Provider**|整形する行を提供するプロバイダーの名前を示します。 プロバイダーが行の提供に使用されない場合、この値は NONE になります。|

 接続文字列のキーワードとして名前を指定することで、書き込み可能な動的プロパティを設定することもできます。 たとえば、Microsoft Visual Basic で、次のように指定して **Data Provider** 動的プロパティを "MSDASQL" に設定します。

```vb
Dim cn as New ADODB.Connection
cn.Open "Provider=MSDataShape;Data Provider=MSDASQL"
```

 また、プロパティの名前を [Properties](../../reference/ado-api/properties-collection-ado.md) プロパティのインデックスとして指定することによって、動的プロパティを設定または取得することもできます。 たとえば、次のコード例では、 **Data Provider** 動的プロパティの現在の値を取得して出力し、cn の場合に新しい値を設定します。DataProvider が "MSDataShape" に設定されました (直接または間接的に接続文字列を介して)。接続が開かれていません。

```vb
Debug.Print cn.Properties("Data Provider")
cn.Properties("Data Provider") = "MSDASQL"
```

> [!NOTE]
>  動的プロパティの **Data Provider** は、開かれていない **接続** オブジェクトに対してのみ設定できます。 接続が開かれると、 **Data Provider** プロパティが読み取り専用になります。

 データシェイプの詳細については、「 [データシェイプ](../data/data-shaping-overview.md)」を参照してください。

## <a name="see-also"></a>参照
 [付録 A: プロバイダー](./appendix-a-providers.md)