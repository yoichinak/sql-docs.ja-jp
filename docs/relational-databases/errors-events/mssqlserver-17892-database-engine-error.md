---
description: MSSQLSERVER_17892
title: MSSQLSERVER_17892
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17892 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 59cf1ed10d71bf9813f2ce814d88e7f7d64b6b2e
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418789"
---
# <a name="mssqlserver_17892"></a>MSSQLSERVER_17892
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|17892|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|SRV_LOGON_FAILED_BY_TRIGGER|
|メッセージ テキスト|トリガーの実行により、ログイン \<Login Name> のログオンに失敗しました。|
||

## <a name="explanation"></a>説明

エラー 17892 は、ログオン トリガー コードを正常に実行できない場合に発生します。 [ログオン トリガー](/sql/relational-databases/triggers/logon-triggers)は、LOGON イベントに応答してストアド プロシージャを起動します。 このイベントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスでユーザー セッションが確立されるときに発生します。 次のようなエラー メッセージがユーザーに報告されます。

> メッセージ 17892、レベル 14、状態 1、サーバー \<Server Name>、行 1  
トリガーの実行により、ログイン \<Login Name> のログオンに失敗しました。

## <a name="possible-causes"></a>考えられる原因

この問題は、その特定のユーザー アカウントのトリガー コードの実行時にエラーが発生した場合に発生するおそれがあります。 次のようなシナリオが考えられます。

- トリガーが存在しないテーブルにデータを挿入しようとする場合。
- ログオン トリガーによって参照されるオブジェクトに対するアクセス許可がログインにない場合。

## <a name="user-action"></a>ユーザー アクション

該当するシナリオに応じて、次のいずれかの解決策を使用してください。

- **シナリオ 1** : 現在、管理者アカウントで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] へのオープン セッションにアクセスできる。

  この場合は、トリガー コードを修正するために必要な修正措置を講じることができます。

  - 例 1:トリガー コードによって参照されるオブジェクトが存在しない場合は、そのオブジェクトを作成して、ログイン トリガーが正常に実行されるようにします。

  - 例 2:トリガー コードによって参照されるオブジェクトが存在するが、ユーザーにアクセス許可がない場合は、そのオブジェクトにアクセスするために必要な特権を付与します。  
  
  または、ログイン トリガーを削除または無効にして、ユーザーが引き続き [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にログインできるようにすることもできます。  

- **シナリオ 2** : 管理者特権で開いている現在のセッションはないが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で専用管理者接続 (DAC) が有効になっている。

    この場合、DAC 接続はログイン トリガーの影響を受けないため、DAC 接続を使用して、例 1 で説明したのと同じ手順を行うことができます。 DAC 接続の詳細については、「[データベース管理者用の診断接続](/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators)」を参照してください。

    ご使用の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で DAC が有効になっているかどうかを確認するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログで次のようなメッセージがあるかを確認します。

    > 2020-02-09 16:17:44.150 ポート 1434 でローカルにリッスンするため、専用管理者接続のサポートが確立されました。  

- **シナリオ 3** :サーバーで DAC が有効になっておらず、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] への既存の管理セッションもない。

    このシナリオで問題を修復する唯一の方法は、次の手順を行うことです。
  
    1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] と関連するサービスを停止します。
    2. スタートアップ パラメーター `-c`、`-m`、`-f` を使用して、[コマンド プロンプト](/previous-versions/sql/sql-server-2008-r2/ms180965(v=sql.105))から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を起動します。 これにより、ログイン トリガーが無効になり、上記の **例 1** で説明されているのと同じ修復手段を実行できます。
  
        > [!NOTE]
        > 上記の手順では、 *SA* または同等の管理者アカウントが必要です。
  
         これらおよび他のスタートアップ オプションについて詳しくは、「[データベース エンジン サービスのスタートアップ オプション](/sql/database-engine/configure-windows/database-engine-service-startup-options)」を参照してください。

## <a name="more-information"></a>詳細情報

ログオン トリガーが失敗するもう 1 つの状況は、`EVENTDATA` 関数を使用している場合です。 この関数により、XML が返され、大文字と小文字が区別されます。  そのため、IP アドレスに基づいてアクセスをブロックすることを目的として、次のログオン トリガーを作成すると、この問題が発生するおそれがあります。

``` sql
 CREATE TRIGGER tr_logon_CheckIP  
 ON ALL SERVER  
 FOR LOGON  
 AS
 BEGIN
  IF IS_SRVROLEMEMBER ( 'sysadmin' ) = 1  
     BEGIN
         DECLARE @IP NVARCHAR ( 15 );  
         SET @IP = ( SELECT EVENTDATA ().value ( '(/EVENT_INSTANCE/ClientHost)[1]' , 'NVARCHAR(15)' ));  
         IF NOT EXISTS( SELECT IP FROM DBAWork.dbo.ValidIP WHERE IP = @IP )  
         ROLLBACK ;  
     END ;  
 END ;  
 GO
```

ユーザーが、トリガーのこの部分にインターネットからこのスクリプトをコピーする場合に、大文字と小文字を区別しませんでした。

```sql
 SELECT EVENTDATA ().value ( '(/event_instance/clienthost)[1]' , 'NVARCHAR(15)' ));  
```

その結果、`EVENTDATA` により常に **NULL** が返され、SA と同等のすべてのログインのアクセスが拒否されました。 この場合、DAC 接続が有効になっていなかったため、上記のスタートアップ パラメーターを使用してサーバーを再起動し、トリガーを削除する以外に選択肢はありませんでした。
