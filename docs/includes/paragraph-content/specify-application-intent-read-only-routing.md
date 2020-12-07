---
title: インクルード ファイル
description: インクルード ファイル
services: sql-database
author: MightyPen
ms.service: sql-database
ms.topic: include
ms.date: 04/05/2018
ms.author: genemi
ms.custom: include file
ms.openlocfilehash: a443b615a6a04b588ed6dc84c6a8a4f6ed12e2f0
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726760"
---
## <a name="specifying-application-intent"></a>アプリケーション インテントの指定

接続文字列には、キーワード **ApplicationIntent** を指定することができます。 割り当て可能な値は、**ReadWrite** または **ReadOnly** です。 既定値は **ReadWrite** です。

**ApplicationIntent=ReadOnly** が指定されている場合、クライアントによって接続時に読み取りワークロードが要求されます。 サーバーでは、接続時と **USE** データベース ステートメントの実行時にこのインテントが適用されます。

**ApplicationIntent** キーワードは、従来の読み取り専用データベースに対しては無効です。  


#### <a name="targets-of-readonly"></a>ReadOnly のターゲット

接続で **ReadOnly** が選択された場合、その接続は、データベースに存在する可能性のある次の特別な構成のいずれかに割り当てられます。

- [Always On](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
    - 対象の AlwaysOn データベースのワークロードの読み取りを許可または禁止できます。 この選択は、**PRIMARY_ROLE** および **SECONDARY_ROLE** Transact-SQL ステートメントの **ALLOW_CONNECTIONS** 句を使用することで制御できます。

- [geo レプリケーション](/azure/sql-database/sql-database-geo-replication-overview)

- [読み取りスケールアウト](/azure/sql-database/sql-database-read-scale-out)

これらの特別なターゲットがいずれも使用できない場合は、通常のデータベースから読み取られます。

&nbsp;

**ApplicationIntent** キーワードを使用すると、"*読み取り専用ルーティング*" を有効にできます。


## <a name="read-only-routing"></a>読み取り専用ルーティング

読み取り専用ルーティングは、データベースの読み取り専用レプリカの可用性を実現する機能です。 読み取り専用ルーティングを有効にするには、次のすべてを適用します。

- AlwaysOn 可用性グループ リスナーに接続する必要があります。

- **ApplicationIntent** 接続文字列キーワードを **ReadOnly**に設定する必要があります。

- データベース管理者が可用性グループを構成し、読み取り専用のルーティングを有効にする必要があります。

複数の接続でそれぞれに読み取り専用ルーティングが使用されている場合、すべてが同じ読み取り専用レプリカに接続されるとは限りません。 データベース同期の変更やサーバーのルーティング構成の変更によって、クライアントが別の読み取り専用レプリカに接続される場合があります。 すべての読み取り専用要求が、同じ読み取り専用レプリカに接続されるようにすることができます。 この同一性を保証するには、**Server** 接続文字列キーワードに可用性グループ リスナーを "*渡さない*" ようにします。 代わりに、読み取り専用インスタンスの名前を指定します。

読み取り専用ルーティングには、プライマリへの接続よりも時間がかかることがあります。 待機時間が長くなるのは、読み取り専用ルーティングがまずプライマリに接続し、次に使用できる読み取り可能なセカンダリを検索するためです。 このような複数のステップがあるため、ログイン タイムアウトを少なくとも 30 秒に増やす必要があります。