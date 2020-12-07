---
description: SQL Server での SSMA コンポーネントのインストール (SybaseToSQL)
title: SQL Server での SSMA コンポーネントのインストール (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 07/14/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5ad9e12c-2cdb-4dd2-8703-05a23242d19d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 33b5663e7693de8c031f2b39c0436a771920be56
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88372368"
---
# <a name="installing-ssma-components-on-sql-server-sybasetosql"></a>SQL Server での SSMA コンポーネントのインストール (SybaseToSQL)

SSMA のインストールに加えて、サーバー側のデータ移行を使用するために、を実行しているコンピューターにコンポーネントをインストールする必要もあり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これらのコンポーネントには、データの移行をサポートする SSMA 拡張パックと、サーバーとサーバー間の接続を有効にする Sybase プロバイダーが含まれます。

## <a name="ssma-for-sybase-extension-pack"></a>SSMA for Sybase extension pack

SSMA 拡張パックは、指定されたインスタンスにデータベース、 **sysdb** 、および **ssmatesterdb_syb**を追加し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 **Sysdb**データベースには、データの移行に必要なテーブルとストアドプロシージャが含まれています。 **Ssmatester_syb**データベースには、ssma tester コンポーネントによって使用されるオブジェクト (テーブル、トリガー、ビュー) が作成されるスキーマ**ssma_sybase_utilities**が含まれています。

また、データをに移行するときに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、サーバー側のデータ移行エンジンを使用してデータを移行するときに、ssma によっ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] てエージェントジョブが作成されます。

### <a name="prerequisites"></a>[前提条件]

SSMA for Sybase サーバーコンポーネントをにインストールする前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] システムが次の要件を満たしていることを確認してください。

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスはインストールされています。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows インストーラー3.1 以降のバージョン。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] バージョン4.7.2 以降のバージョン。 これは [.NET Framework デベロッパーセンター](https://go.microsoft.com/fwlink/?LinkId=48882)から入手できます。
- Sybase OLE DB/ADO.Net/ODBC プロバイダーと、移行するデータベースが格納されている SAP ASE データベースサーバーへの接続。 プロバイダーは、SAP ASE 製品メディアからインストールできます。 接続の詳細については、「 [SYBASE ASE &#40;SybaseToSQL&#41;への接続 ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)」を参照してください。
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インストール中に Browser サービスが実行されている必要があります。 これは、セットアップウィザードでのインスタンスの一覧を設定するために使用され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 インストール後に Browser サービスを無効にすることができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

  > [!NOTE]
  > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser サービスが実行されていても、セットアップにインスタンスの一覧が表示されない場合は、UDP ポート1434のブロックを解除する必要があります。 Windows ファイアウォールを使用して、一時的にポートのブロックを解除することも、Windows ファイアウォールを一時的に無効にすることもできます。 また、ウイルス対策ソフトウェアを一時的に無効にすることが必要になる場合もあります。 インストール後に、ファイアウォールとウイルス対策ソフトウェアが有効になっていることを確認してください。

### <a name="installing-the-extension-pack"></a>拡張機能パックのインストール

にデータを移行する前に、いつでも拡張機能パックをインストールでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

> [!IMPORTANT]
> 拡張機能パックをインストールするには、のインスタンスの sysadmin サーバーロールのメンバーである必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

拡張機能パックをインストールするには:

1. を実行しているコンピューターに、 ***n*の SSMAforSybaseExtensionPack_** をコピーします。 *n*はビルド番号です [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
2. **SSMAforSybaseExtensionPack_*n*.msi**をダブルクリックします。
3. **[ようこそ]** ページで **[次へ]** をクリックします。
4. [使用許諾 **契約書** ] ページで、使用許諾契約書を読みます。 同意する場合は、[ **契約に同意** します] オプションを選択し、[ **次へ**] をクリックします。
5. [ **セットアップの種類の選択** ] ページで、[ **標準**] をクリックします。
6. [ **インストールの準備完了** ] ページで、[ **インストール**] をクリックします。
7. [ **インストールの最初の手順を完了しまし** た] ページで、[ **次へ**] をクリックします。

   新しいダイアログボックスが表示されます。このダイアログボックスで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 拡張機能パックのインストール用のインスタンスを選択します。

8. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SAP ASE データベースを移行するのインスタンスを選択し、[**次へ**] をクリックします。

   既定のインスタンスには、コンピューターと同じ名前が付けられています。 名前付きインスタンスの後には、円記号とインスタンス名が続きます。

9. [接続] ページで、認証方法を選択し、[ **次へ**] をクリックします。

   Windows 認証では、Windows 資格情報を使用してのインスタンスにログオンしようとし [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 [サーバー認証] を選択した場合は、ログイン名とパスワードを入力する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

10. 次の手順では、サーバー側のデータの移行中に拡張パックデータベースに格納されている機微なデータを暗号化するために使用されるマスターキーのパスワードを設定する必要があります。 強力なパスワードを入力し、[ **次へ**] をクリックします。

11. 次のページで、[ **Install Utilities Database *n* **] を選択し、Extension Pack library をインストールします。ここで、 *n* はバージョン番号です。 テスト担当者機能を使用する予定の場合は、[ **テスト担当者データベースをインストール** する] チェックボックスをオンにし、[ **次へ**] を選択します。

    **Sysdb**データベースは、(サーバー側のデータ移行エンジンを使用して) データの移行に必要なテーブルとストアドプロシージャがこのデータベースに作成された状態で作成されます。

    [ **テスト担当者データベースをインストール** する] オプションがオンになっている場合、 **ssmatesterdb_syb** データベースが作成されます。

12. インストールが完了すると、の別のインスタンスにユーティリティデータベースをインストールするかどうかを確認するメッセージが表示されます。 [はい] を選択し、[次へ] を選択します。または、[いいえ] を選択し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [**終了**] を選択します。 **Yes** **Next** **No**

### <a name="sql-server-database-objects"></a>SQL Server データベースオブジェクト

拡張機能パックをインストールすると、 **sysdb**データベースに**ssma_syb bcp_migration_packages**テーブルが表示されます。 次のストアドプロシージャも表示されます。

- `bcp_clean_migration_data`
- `bcp_ensure_message_table`
- `bcp_insert_new_message`
- `bcp_post_process`
- `bcp_read_new_migration_messages`
- `bcp_save_migration_package`
- `bcp_smart_truncate`
- `bcp_start_migration_process`
- `get_jobstep_info`
- `stop_agent_process`

にデータを移行するたびに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、ssma によってエージェントジョブが作成さ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] れます。 これらのジョブには **ssma_syb データ移行パッケージ {GUID}** という名前が付けられ、[ジョブ] フォルダーのの [エージェント] ノードに表示され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ます。  

## <a name="sybase-providers"></a>Sybase プロバイダー

サーバー側のデータ移行を使用して SAP ASE からにデータを移動する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データは SAP ase との間で直接移行され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 SSMA を経由することはありません。これは、データ移行の速度が低下するためです。

### <a name="installing-the-sybase-providers"></a>Sybase プロバイダーのインストール

次の手順では、Sybase プロバイダーをインストールするための基本的なインストール手順について説明します。 正確な手順は、Sybase セットアッププログラムのバージョンによって異なります。

> [!IMPORTANT]
> セットアッププログラムを実行する前に、ライセンス契約に違反していないことを確認してください。

1. Sybase ASE セットアッププログラムを実行します。
2. [カスタムセットアップ] を選択します。
3. [機能の選択] ページで、ODBC、OLE DB および ADO.NET データプロバイダーを選択します。
4. 選択した機能を確認し、[ **完了** ] をクリックしてデータプロバイダーをインストールします。

## <a name="see-also"></a>関連項目

- [SSMA for Sybase クライアントのインストール](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md)
- [Sybase ASE データベースの SQL Server Azure SQL Database への移行](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)
