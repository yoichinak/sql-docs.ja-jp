---
description: Microsoft OLE DB Provider for Internet Publishing の概要
title: Microsoft OLE DB Provider for Internet Publishing |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
- Internet Publishing provider [ADO]
ms.assetid: 66a208d9-b580-4655-a41e-1d36e5b5bfca
author: rothja
ms.author: jroth
ms.openlocfilehash: f924e1bec97ed399f4d6d3351c8d18b1d8dad5b1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991063"
---
# <a name="microsoft-ole-db-provider-for-internet-publishing-overview"></a>Microsoft OLE DB Provider for Internet Publishing の概要
Microsoft OLE DB Provider for Internet Publishing を使用すると、ADO は Microsoft FrontPage または Microsoft インターネットインフォメーションサーバーによって提供されるリソースにアクセスできます。 リソースには、HTML ファイルや Windows 2000 web フォルダーなどの web ソースファイルが含まれます。

## <a name="connection-string-parameters"></a>接続文字列パラメーター
 このプロバイダーに接続するには、 [ConnectionString](../../reference/ado-api/connectionstring-property-ado.md)プロパティの*provider*引数を次のように設定します。

```vb
MSDAIPP.DSO
```

 この値は、 [プロバイダー](../../reference/ado-api/provider-property-ado.md) プロパティを使用して設定または読み取ることもできます。

## <a name="typical-connection-string"></a>一般的な接続文字列
 このプロバイダーの一般的な接続文字列は次のとおりです。

```vb
"Provider=MSDAIPP.DSO;Data Source=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 - または -

```vb
"URL=ResourceURL;User ID=MyUserID;Password=MyPassword;"
```

 文字列は、次のキーワードで構成されています。

|キーワード|説明|
|-------------|-----------------|
|**プロバイダー**|インターネット発行用の OLE DB プロバイダーを指定します。|
|**データソース** または- **URL**|Web フォルダーに発行されたファイルまたはディレクトリの URL を指定します。|
|**[ユーザー ID]**|ユーザー名を指定します。|
|**パスワード**|ユーザーのパスワードを指定します。|

> [!NOTE]
>  Windows 認証をサポートするデータソースプロバイダーに接続する場合は、接続文字列にユーザー ID とパスワードの情報ではなく、 **Trusted_Connection = yes** または **INTEGRATED Security = SSPI** を指定する必要があります。

 接続文字列の "URL =" の *Resourceurl* 値を無効な値に設定した場合、既定では、インターネット公開プロバイダーによって、有効な値の入力を求めるダイアログボックスが表示されます。 これは、アプリケーションの中間層のコンポーネントに対して望ましくない動作です。これは、ダイアログボックスがクリアされ、コンポーネントからの応答を受信していないためにクライアントがフリーズしている場合に、プログラムの実行が中断されるためです。

> [!NOTE]
>  MSDAIPP の場合。DSO はプロバイダーの値として明示的に指定されます *。プロバイダーの接続文字列* キーワードまたは **プロバイダー** プロパティを使用して、接続文字列で "URL =" を使用することはできません。 そうすると、エラーが発生します。 代わりに、「 [Internet Publishing の OLE DB プロバイダーで ADO を使用する](../data/the-ole-db-provider-for-internet-publishing.md)」のトピックで説明されているように、単に URL を指定します。

## <a name="see-also"></a>参照
 インターネット[公開シナリオ](../data/internet-publishing-scenario.md)[インターネット発行用の OLE DB プロバイダー](../data/the-ole-db-provider-for-internet-publishing.md)