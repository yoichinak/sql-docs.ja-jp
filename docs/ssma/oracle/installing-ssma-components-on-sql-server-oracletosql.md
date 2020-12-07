---
title: SQL Server での SSMA コンポーネントのインストール (OracleToSQL) |Microsoft Docs
description: Oracle データベースの変換をサポートするために SQL Server を実行しているコンピューターに SSMA 拡張パックと Oracle プロバイダーをインストールする方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 11/16/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing the extension pack
- SQL Server Database Objects
ms.assetid: 33070e5f-4e39-4b70-ae81-b8af6e4983c5
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 64850d1a701491f0dc5817576a568fdc3ebc2483
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870105"
---
# <a name="installing-ssma-components-on-sql-server-oracletosql"></a>SQL Server での SSMA コンポーネントのインストール (OracleToSQL)

SSMA のインストールに加えて、を実行しているコンピューターにコンポーネントをインストールする必要もあり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これらのコンポーネントには、データ移行をサポートする SSMA extension pack と、サーバー間接続を有効にする Oracle プロバイダーが含まれます。

## <a name="ssma-for-oracle-extension-pack"></a>SSMA for Oracle extension pack

SSMA 拡張パックは、拡張ストアドプロシージャを配置し、指定されたインスタンスに **sysdb** および **ssmatesterdb** データベースを追加し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 拡張ストアドプロシージャは、Oracle の機能と behaiov をエミュレートするために必要な機能を提供します。一方、 **sysdb** データベースには、データの移行に必要なテーブルとストアドプロシージャが含まれています。 **Ssmatesterdb** データベースには、Tester コンポーネント (インストールされている場合) に必要なテーブルとプロシージャが含まれています。

また、データをに移行するときに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、サーバー側のデータ移行エンジンを使用してデータを移行するときに、ssma によって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントジョブが作成されます。

### <a name="prerequisites"></a>前提条件

SSMA for Oracle サーバーコンポーネントをにインストールする前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システムが次の要件を満たしていることを確認してください。

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスはインストールされています。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows インストーラー3.1 以降のバージョン。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] バージョン4.7.2 以降のバージョン。 これは [.NET Framework デベロッパーセンター](https://go.microsoft.com/fwlink/?LinkId=48882)から入手できます。
- OLE DB provider for Oracle (OLE DB を使用する場合)、および移行する Oracle データベースへの接続。 プロバイダーは、Oracle 製品メディアまたは Oracle Web サイトからインストールできます。
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インストール中に Browser サービスが実行されている必要があります。 これは、セットアップウィザードでのインスタンスの一覧を設定するために使用され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 インストール後に Browser サービスを無効にすることができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

  > [!NOTE]
  > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser サービスが実行されていても、セットアップにインスタンスの一覧が表示されない場合は、UDP ポート1434のブロックを解除する必要があります。 Windows ファイアウォールを使用して、一時的にポートのブロックを解除することも、Windows ファイアウォールを一時的に無効にすることもできます。 また、ウイルス対策ソフトウェアを一時的に無効にすることが必要になる場合もあります。 インストール後に、ファイアウォールとウイルス対策ソフトウェアが有効になっていることを確認してください。

### <a name="installing-the-extension-pack"></a>拡張機能パックのインストール

にデータを移行する前に、拡張機能パックをいつでもインストールでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

> [!IMPORTANT]
> 拡張機能パックをインストールするには、のインスタンスの **sysadmin** サーバーロールのメンバーである必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

拡張機能パックをインストールするには:

1. を実行しているコンピューターに **SSMAforOracleExtensionPack_ *n*.msi** ( *n* はビルド番号) をコピーします [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
2. **SSMAforOracleExtensionPack_ *n*.msi** をダブルクリックします。
3. **[ようこそ]** ページで **[次へ]** をクリックします。
4. [使用許諾 **契約書** ] ページで、使用許諾契約書を読みます。 同意する場合は、 **[同意する] を選択し** 、[ **次へ**] をクリックします。
5. [ **セットアップの種類の選択** ] ページで、[ **標準**] を選択します。
6. [ **インストールの準備完了** ] ページで、[ **インストール**] を選択します。
7. [ **インストールの最初の手順を完了しまし** た] ページで、[ **次へ**] を選択します。
  
   新しいダイアログボックスが表示されます。 拡張パックの種類を選択します。
  
8. 目的のインストールの種類を選択し、[ **次へ**] をクリックします。

   > [!IMPORTANT]
   > リモートオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Linux で実行されている場合は拡張パックをインストールする場合にのみ使用し、を対象とする場合にのみ使用してください [!INCLUDE[ssAzureMi](../../includes/ssazuremi_md.md)] 。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows で実行されているインストールでは、常に拡張機能パックをローカルにインストールする必要があります。 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] および Azure Synapse Analytics では、拡張機能パックはサポートされていません。

   拡張機能パックをローカルインスタンスにインストールする場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、次のページでは、Oracle スキーマを移行するのローカルインスタンスを選択でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 ドロップダウンでインスタンスを選択し、[ **次へ**] を選択します。

   既定のインスタンスには、コンピューターと同じ名前が付けられています。 名前付きインスタンスの後には、円記号とインスタンス名が続きます。

9. [接続] ページで、[認証方法] を選択し、[ **次へ**] を選択します。

   Windows 認証では、Windows 資格情報を使用してのインスタンスにサインインしようとし [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 [サーバー認証] を選択した場合は、ログイン名とパスワードを入力する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

10. 次の手順では、サーバー側のデータの移行中に拡張パックデータベースに格納されている機微なデータを暗号化するために使用されるマスターキーのパスワードを設定する必要があります。 強力なパスワードを入力し、[ **次へ**] をクリックします。

11. 次のページで、[ **Install Utilities Database *n***] を選択し、Extension Pack library をインストールします。ここで、 *n* はバージョン番号です。 テスト担当者機能を使用する予定の場合は、[ **テスト担当者データベースをインストール** する] チェックボックスをオンにし、[ **次へ**] を選択します。

    **Sysdb** データベースは、(サーバー側のデータ移行エンジンを使用して) データの移行に必要なテーブルとストアドプロシージャがこのデータベースに作成された状態で作成されます。

    [ **テスト担当者データベースをインストール** する] オプションがオンになっている場合は、 **ssmatesterdb** データベースが作成されます。

12. インストールが完了すると、の別のインスタンスにユーティリティデータベースをインストールするかどうかを確認するメッセージが表示されます。 [はい] を選択し、[次へ] を選択します。または、[いいえ] を選択し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [**終了**] を選択します。 **Yes** **Next** **No**

13. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]またはユーティリティを使用して `sqlcmd` 、次のスクリプトを実行して CLR を有効にします。

    ```sql
    sp_configure 'clr enabled', 1
    GO
    RECONFIGURE
    GO
    ```

    CLR が有効になっていない場合、SSMA がに接続すると、次のエラーが表示され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

    > SSMA は、拡張パックのアセンブリのバージョン情報を取得できませんでした。 データベースサーバーに拡張パックを再インストールしてください。

### <a name="sql-server-database-objects"></a>SQL Server データベースオブジェクト

拡張機能パックをインストールすると、 **ssma_oracle _migration_packages** テーブルが **sysdb** データベースに表示されます。

にデータを移行するたびに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、ssma によってエージェントジョブが作成さ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] れます。 これらのジョブには **ssma_oracle データ移行パッケージ {GUID}** という名前が付けられ、[ジョブ] フォルダーのの [エージェント] ノードに表示され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ます。

次に示す拡張ストアドプロシージャは、 **master** データベースにも追加されます。

- `xp_ora2ms_exec2`
- `xp_ora2ms_exec2_ex`
- `xp_ora2ms_versioninfo2`

## <a name="see-also"></a>関連項目

- [SSMA for Oracle クライアントのインストール](../../ssma/oracle/installing-ssma-for-oracle-client-oracletosql.md)
- [SQL Server への Oracle データベースの移行](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)
