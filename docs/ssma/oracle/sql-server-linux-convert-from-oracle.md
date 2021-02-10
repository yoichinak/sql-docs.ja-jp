---
title: Oracle HR スキーマを SQL Server on Linux | に移行します。Microsoft Docs
description: サンプル Oracle スキーマを SQL Server on Linux に変換する
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: ''
ms.technology: ssma
ms.openlocfilehash: fb21fdc7da82d6dae2390ddcf0884ea1e8ac8a58
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100044392"
---
# <a name="migrate-an-oracle-schema-to-sql-server-2017-on-linux-with-the-sql-server-migration-assistant"></a>SQL Server Migration Assistant を使用して Oracle スキーマを Linux 上の SQL Server 2017 に移行する

このチュートリアルでは、Windows 上の Oracle の SQL Server Migration Assistant (SSMA) を使用して、 [Linux 上](../../linux/sql-server-linux-overview.md)の Oracle サンプル **HR** スキーマを SQL Server 2017 に変換します。

> [!div class="checklist"]
> * SSMA を Windows にダウンロードしてインストールする
> * SSMA プロジェクトを作成して移行を管理する
> * Oracle への接続
> * 移行レポートを実行する
> * サンプル HR スキーマの変換
> * データを移行する

## <a name="prerequisites"></a>前提条件

- **HR** スキーマがインストールされた Oracle 12c (12.2.0.1.0) のインスタンス
- SQL Server on Linux の作業インスタンス

> [!NOTE]
> 同じ手順を使用して Windows 上の SQL Server を対象にすることもできますが、[プロジェクト **に移行** ] 設定で windows を選択する必要があります。

## <a name="download-and-install-ssma-for-oracle"></a>SSMA for Oracle のダウンロードとインストール

ソースデータベースによっては、使用可能な SQL Server Migration Assistant のエディションがいくつかあります。  [Oracle 用の SQL Server Migration Assistant](https://aka.ms/ssmafororacle)の現在のバージョンをダウンロードし、ダウンロードページの指示に従ってインストールします。

> [!NOTE]
> 現時点では、 **Ssma For Oracle Extension Pack** は Linux ではサポートされていませんが、このチュートリアルでは必要ありません。

## <a name="create-and-set-up-project"></a>プロジェクトの作成と設定

新しい SSMA プロジェクトを作成するには、次の手順に従います。

1. SSMA for Oracle を開き、[**ファイル**] メニューの [**新しいプロジェクト**] をクリックします。

1. プロジェクトに名前を付けます。

1. [ **移行先** ] フィールドで、[SQL Server 2017 (Linux)-Preview] を選択します。

SSMA for Oracle では、既定では Oracle サンプルスキーマが使用されません。 HR スキーマを有効にするには、次の手順に従います。

1. SSMA で、[ **ツール** ] メニューを選択します。

1. [ **既定のプロジェクト設定**] を選択し、[ **システムオブジェクトの読み込み**] を選択します。

1. [ **HR** ] がオンになっていることを確認し、[ **OK]** を選択します。

## <a name="connect-to-oracle"></a>Oracle への接続

次に、SSMA を Oracle に接続します。

1. ツールバーの [ **Oracle への接続**] をクリックします。

1. サーバー名、ポート、Oracle SID、ユーザー名、およびパスワードを入力します。

   ![Oracle への接続](./media/sql-server-linux-convert-from-oracle/ConnectToOracle.png)

1. 次いで **[Connect]** をクリックします。 SSMA for Oracle は、しばらくしてデータベースに接続し、そのメタデータを読み取ります。

## <a name="create-a-report"></a>レポートを作成する

移行レポートを生成するには、次の手順に従います。

1. **Oracle メタデータエクスプローラー** で、サーバーのノードを展開します。

1. [ **スキーマ**] を展開し、[ **HR**] を右クリックして、[ **レポートの作成**] を選択します。

   ![Oracle メタデータエクスプローラーのレポートの作成](./media/sql-server-linux-convert-from-oracle/CreateReport.png)

1. 新しいブラウザーウィンドウが開き、変換に関連付けられたすべての警告とエラーが一覧表示されたレポートが表示されます。

   > [!NOTE]
   > このチュートリアルでは、この一覧について何もする必要はありません。 独自の Oracle データベースに対してこれらの手順を実行する場合は、レポートを確認して、データベースの重要な変換の問題に対処する必要があります。

   ![移行レポートのサンプル](./media/sql-server-linux-convert-from-oracle/SSMAReport.png)

## <a name="connect-to-sql-server"></a>SQL Server への接続

次に、[ **Connect to SQL Server** ] を選択し、適切な接続情報を入力します。  まだ存在しないデータベース名を使用すると、SSMA for Oracle によって作成されます。

![SQL Server への接続](./media/sql-server-linux-convert-from-oracle/ConnectToSQLServer.png)

## <a name="convert-schema"></a>スキーマの変換

**Oracle メタデータエクスプローラー** で **HR** を右クリックし、[スキーマの変換] を選択します。

![スキーマの変換](./media/sql-server-linux-convert-from-oracle/ConvertSchema.png)

## <a name="synchronize-database"></a>データベースの同期

次に、データベースを同期します。

1. 変換が完了したら、 **SQL Server メタデータエクスプローラー** を使用して、前の手順で作成したデータベースにアクセスします。

1. データベースを右クリックし、[ **データベースとの同期**] を選択して、[OK] をクリックします。

   ![データベースとの同期](./media/sql-server-linux-convert-from-oracle/SynchronizeWithDatabase.png)

## <a name="migrate-data"></a>データの移行

最後の手順は、データを移行することです。

1. **Oracle メタデータエクスプローラー** で、[ **HR**] を右クリックし、[**データの移行**] を選択します。

1. データ移行手順では、Oracle と SQL Server の資格情報を再入力する必要があります。

1. 完了したら、データ移行レポートを確認します。次のスクリーンショットのようになります。

   ![データ移行レポート](./media/sql-server-linux-convert-from-oracle/DataMigrationReport.png)

## <a name="next-steps"></a>次のステップ

より複雑な Orcale スキーマの場合、変換プロセスには、クライアントアプリケーションに対してより多くの時間、テスト、および可能性のある変更が含まれます。 このチュートリアルの目的は、移行プロセス全体の一部として SSMA for Oracle を使用する方法を説明することです。

このチュートリアルでは、以下の内容を学習しました。
> [!div class="checklist"]
> * SSMA を Windows にインストールする
> * 新しい SSMA プロジェクトを作成する
> * Oracle からの移行を評価して実行する

次に、SSMA を使用する他の方法について説明します。

> [!div class="nextstepaction"]
>[SQL Server Migration Assistant のドキュメント](../sql-server-migration-assistant.md)
