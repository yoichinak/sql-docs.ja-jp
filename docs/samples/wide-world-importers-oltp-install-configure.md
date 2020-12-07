---
title: WideWorldImporters サンプルデータベースをインストールして構成する
description: 次の手順に従って、SQL Server Management Studio で WideWorldImporters サンプルデータベースをダウンロードし、インストールして、構成します。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 9868b414d627c7ea98504120432c0c3a662d463b
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956553"
---
# <a name="installation-and-configuration"></a>インストールと構成
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]
大規模な環境では、OLTP データベースのインストールと構成の手順について説明します。

## <a name="prerequisites"></a>前提条件

- [SQL Server 2016](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) (またはそれ以降) または [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)。 このサンプルの完全なバージョンについては、SQL Server Evaluation/Developer/Enterprise Edition を使用してください。
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 最良の結果を得るには、2016年6月リリース以降を使用します。

## <a name="download"></a>ダウンロード

サンプルの最新リリースは次のとおりです。

[ワイド-インポーター-リリース](https://go.microsoft.com/fwlink/?LinkID=800630)

SQL Server または Azure SQL Database のエディションに対応するサンプル WideWorldImporters database backup/bacpac をダウンロードします。

サンプルデータベースを再作成するソースコードは、次の場所から入手できます。 データ生成にはランダムな要因があるため、サンプルを再作成すると、データにわずかな違いが生じることに注意してください。

[ワイド-インポーター](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

## <a name="install"></a>インストール


### <a name="sql-server"></a>SQL Server

バックアップを SQL Server インスタンスに復元するには、Management Studio を使用できます。

1. SQL Server Management Studio を開き、ターゲットの SQL Server インスタンスに接続します。
2. [ **データベース** ] ノードを右クリックし、[ **データベースの復元**] を選択します。
3. [**デバイス**] を選択し、[.. **.** ] ボタンをクリックします。
4. ダイアログで [ **バックアップデバイスの選択**] をクリックし、[ **追加**] をクリックして、サーバーのファイルシステム内のデータベースバックアップに移動し、バックアップを選択します。 **[OK]** をクリックします。
5. 必要に応じて、[ **ファイル** ] ウィンドウでデータファイルとログファイルのターゲットの場所を変更します。 データファイルとログファイルは別のドライブに配置することをお勧めします。
6. **[OK]** をクリックします。 これにより、データベースの復元が開始されます。 完了すると、SQL Server インスタンスにデータベース WideWorldImporters がインストールされます。

### <a name="azure-sql-database"></a>Azure SQL データベース

Bacpac を新しい SQL Database にインポートするには、Management Studio を使用できます。

1. optionalまだ Azure に SQL Server がない場合は、 [Azure portal](https://portal.azure.com/) に移動し、新しい SQL Database を作成します。 データベースを作成するプロセスでは、サーバーを作成します。 サーバーをメモしておきます。
   - [このチュートリアル](/azure/azure-sql/database/single-database-create-quickstart)を参照して、データベースを数分で作成してください
2. SQL Server Management Studio を開き、Azure のサーバーに接続します。
3. [ **データベース** ] ノードを右クリックし、[ **Data-Tier アプリケーションのインポート**] を選択します。
4. [ **インポートの設定** ] で、[ **ローカルディスクからインポート** する] を選択し、ファイルシステムからサンプルデータベースの bacpac を選択します。
5. [ **データベースの設定** ] で、データベース名を *WideWorldImporters* に変更し、使用するターゲットエディションとサービス目標を選択します。
6. [ **次へ** **] をクリックして、** 展開を開始します。 P1 の完了までに数分かかります。 価格レベルを低くする必要がある場合は、新しい P1 データベースにインポートし、価格レベルを目的のレベルに変更することをお勧めします。

## <a name="configuration"></a>構成

### <a name="full-text-indexing"></a>フルテキスト インデックス作成

サンプルデータベースでは、Full-Text インデックス作成を使用できます。 ただし、この機能は既定では SQL Server と共にインストールされません。 SQL Server セットアップ中に選択する必要があります (Azure SQL Database では既定で有効になっています)。 そのため、インストール後の手順が必要です。

1. SQL Server Management Studio で、WideWorldImporters データベースに接続し、新しいクエリウィンドウを開きます。
2. 次の T-sql コマンドを実行して、データベースでの Full-Text インデックスの使用を有効にします。  `EXECUTE Application.Configuration_ApplyFullTextIndexing`


### <a name="sql-server-audit"></a>SQL Server Audit

適用対象: SQL Server

SQL Server で監査を有効にするには、サーバー構成が必要です。 WideWorldImporters サンプルの SQL Server 監査を有効にするには、データベースで次のステートメントを実行します。

```sql
EXECUTE [Application].[Configuration_ApplyAuditing]
```

Azure SQL Database では、 [Azure portal](https://portal.azure.com/)によって監査が構成されます。

### <a name="row-level-security"></a>行レベルのセキュリティ

適用対象: Azure SQL Database

WideWorldImporters の bacpac ダウンロードでは、Row-Level セキュリティは既定では有効になっていません。 データベースで Row-Level セキュリティを有効にするには、次のストアドプロシージャを実行します。

```sql
EXECUTE [Application].[Configuration_ApplyRowLevelSecurity]
```