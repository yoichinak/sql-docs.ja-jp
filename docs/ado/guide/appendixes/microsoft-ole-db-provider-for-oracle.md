---
description: Microsoft OLE DB Provider for Oracle の概要
title: Microsoft OLE DB Provider for Oracle |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for Oracle
- OLE DB provider for Oracle [ADO]
- Oracle provider [ADO]
ms.assetid: 44fae9dd-5585-4cd6-8bbd-3248a78931b4
author: rothja
ms.author: jroth
ms.openlocfilehash: d8da5e3d5de1ac0ee3f3dfa1b0f989679af3cd1d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991013"
---
# <a name="microsoft-ole-db-provider-for-oracle-overview"></a>Microsoft OLE DB Provider for Oracle の概要
> [!IMPORTANT]
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle の OLE DB プロバイダーを使用します。

 Microsoft OLE DB Provider for Oracle により、ADO は Oracle データベースにアクセスできます。

## <a name="connection-string-parameters"></a>接続文字列パラメーター
 このプロバイダーに接続するには、 [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md)プロパティの*provider*引数を次のように設定します。

```vb
MSDAORA
```

 [プロバイダー](../../reference/ado-api/provider-property-ado.md)プロパティを読み取ると、この文字列も返されます。

 キーセットカーソルまたは動的カーソルを使用した結合クエリが Oracle データベースで実行されると、エラーが発生します。 Oracle では、静的な読み取り専用カーソルのみがサポートされます。

## <a name="typical-connection-string"></a>一般的な接続文字列
 このプロバイダーの一般的な接続文字列は次のとおりです。

```vb
"Provider=MSDAORA;Data Source=serverName;User ID=MyUserID; Password=MyPassword;"
```

 文字列は、次のキーワードで構成されています。

|キーワード|説明|
|-------------|-----------------|
|**プロバイダー**|Oracle の OLE DB プロバイダーを指定します。|
|**データ ソース**|サーバーの名前を指定します。|
|**[ユーザー ID]**|ユーザー名を指定します。|
|**パスワード**|ユーザーのパスワードを指定します。|

> [!NOTE]
>  Windows 認証をサポートするデータソースプロバイダーに接続する場合は、接続文字列にユーザー ID とパスワードの情報ではなく、 **Trusted_Connection = yes** または **INTEGRATED Security = SSPI** を指定する必要があります。

## <a name="provider-specific-connection-parameters"></a>プロバイダー固有の接続パラメーター
 プロバイダーは、ADO によって定義されているものに加えて、いくつかのプロバイダー固有の接続パラメーターをサポートしています。 ADO の接続プロパティと同様に、これらのプロバイダー固有のプロパティは、[接続](../../reference/ado-api/connection-object-ado.md)の[properties](../../reference/ado-api/properties-collection-ado.md)コレクションまたは**ConnectionString**の一部として設定できます。

 これらのパラメーターの詳細については [OLE DB プログラマーリファレンス](/previous-versions/windows/desktop/ms713643(v=vs.85))」を参照してください。 [ADO 動的プロパティインデックス](../../reference/ado-api/ado-dynamic-property-index.md)は、これらのパラメーター名と、対応する OLE DB プロパティとの間の相互参照を提供します。

|パラメーター|説明|
|---------------|-----------------|
|**ウィンドウ ハンドル**|追加情報の入力を求めるために使用するウィンドウハンドルを示します。|
|**[Locale Identifier]**|ユーザーの言語に関連する設定を指定する32ビットの一意の数値 (1033 など) を示します。 これらの設定は、日付と時刻を書式設定する方法、アルファベット順に並べ替えられる項目、文字列を比較する方法などを指定します。|
|**OLE DB サービス**|有効または無効にする OLE DB サービスを指定するビットマスクを示します。|
|**プロンプト**|接続の確立中にユーザーにプロンプトを表示するかどうかを示します。|
|**Extended Properties**|プロバイダー固有の拡張接続情報を含む文字列。 このプロパティは、プロパティメカニズムでは記述できないプロバイダー固有の接続情報に対してのみ使用します。|

## <a name="see-also"></a>参照
 [ConnectionString プロパティ (ado)](../../reference/ado-api/connectionstring-property-ado.md) [プロバイダープロパティ (ado](../../reference/ado-api/provider-property-ado.md) ) [レコードセットオブジェクト (ado)](../../reference/ado-api/recordset-object-ado.md)