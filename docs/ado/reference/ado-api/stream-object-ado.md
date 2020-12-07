---
description: Stream オブジェクト (ADO)
title: Stream オブジェクト (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Stream
helpviewer_keywords:
- Stream object [ADO]
ms.assetid: 0514531f-009d-4519-abc3-d727014a39f1
author: rothja
ms.author: jroth
ms.openlocfilehash: 619d9d307e26829ffa74a24c6904fa84889f476f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988593"
---
# <a name="stream-object-ado"></a>Stream オブジェクト (ADO)
バイナリデータまたはテキストのストリームを表します。  
  
 ファイルシステムや電子メールシステムなどのツリー構造の階層では、 [レコード](./record-object-ado.md) には、ファイルまたは電子メールの内容を含む既定のバイナリストリームが関連付けられている場合があります。 **ストリーム**オブジェクトは、これらのデータストリームを含むフィールドまたはレコードを操作するために使用できます。 **ストリーム**オブジェクトは、次の方法で取得できます。  
  
-   バイナリまたはテキストデータを含むオブジェクト (通常はファイル) を指す URL。 このオブジェクトには、単純なドキュメント、構造化されたドキュメントを表す **レコード** オブジェクト、またはフォルダーを指定できます。  
  
-   **Record**オブジェクトに関連付けられた既定の**ストリーム**オブジェクトを開く。 レコード**を開い**たときに**レコード**オブジェクトに関連付けられた既定のストリームを取得して、ストリームを開くだけでラウンドトリップが行われないようにすることができます。  
  
-   **ストリーム**オブジェクトをインスタンス化する。 これらの **ストリーム** オブジェクトは、アプリケーションの目的でデータを格納するために使用できます。 URL に関連付けられた**ストリーム**や**レコード**の既定の**ストリーム**とは異なり、インスタンス化された**ストリーム**には、既定で基になるソースとの関連付けがありません。  
  
 **Stream**オブジェクトのメソッドとプロパティを使用して、次の操作を実行できます。  
  
-   [Open](./open-method-ado-stream.md)メソッドを使用して、**レコード**または URL から**ストリーム**オブジェクトを開きます。  
  
-   [Close](./close-method-ado.md)メソッドを使用して**ストリーム**を閉じます。  
  
-   [Write](./write-method.md)および[WriteText](./writetext-method.md)メソッドを使用して**ストリーム**にバイトまたはテキストを入力します。  
  
-   [Read](./read-method.md)および[ReadText](./readtext-method.md)メソッドを使用して、**ストリーム**からバイトを読み取ります。  
  
-   ADO バッファーに残っている **ストリーム** データを、 [Flush](./flush-method-ado.md) メソッドを使用して基になるオブジェクトに書き込みます。  
  
-   [CopyTo](./copyto-method-ado.md)メソッドを使用して**ストリーム**の内容を別の**ストリーム**にコピーします。  
  
-   [SkipLine](./skipline-method.md)メソッドと[lineseparator](./lineseparator-property-ado.md)プロパティを使用して、ソースファイルから行を読み取る方法を制御します。  
  
-   [EOS](./eos-property.md)プロパティと[SetEOS](./seteos-method.md)メソッドを使用して、ストリームの位置の終わりを確認します。  
  
-   [SaveToFile](./savetofile-method.md)メソッドと[LoadFromFile](./loadfromfile-method-ado.md)メソッドを使用して、データをファイルに保存して復元します。  
  
-   [Charset](./charset-property-ado.md)プロパティを使用して、**ストリーム**の格納に使用する文字セットを指定します。  
  
-   [Cancel](./cancel-method-ado.md)メソッドを使用して、非同期**ストリーム**操作を停止します。  
  
-   [Size](./size-property-ado-stream.md)プロパティを使用して、**ストリーム**内のバイト数を決定します。  
  
-   [Position](./position-property-ado.md)プロパティを使用して、**ストリーム**内の現在位置を制御します。  
  
-   [Type](./type-property-ado-stream.md)プロパティを使用して、**ストリーム**内のデータの種類を決定します。  
  
-   [State](./state-property-ado.md)プロパティを使用して、**ストリーム**の現在の状態 (閉じている、開いている、または実行中) を確認します。  
  
-   [モード](./mode-property-ado.md)プロパティを使用して、**ストリーム**のアクセスモードを指定します。  
  
> [!NOTE]
>  Http スキームを使用する Url は、 [インターネット公開のために Microsoft OLE DB プロバイダー](../../guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)を自動的に呼び出します。 詳細については、「 [絶対 url と相対 url](../../guide/data/absolute-and-relative-urls.md)」を参照してください。  
  
 **ストリーム**オブジェクトは、スクリプトに対して安全です。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [Stream オブジェクトのプロパティ、メソッド、およびイベント](./stream-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [レコードとストリーム](../../guide/data/records-and-streams.md)