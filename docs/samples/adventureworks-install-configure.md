---
title: AdventureWorks サンプルデータベース
description: Transact-sql (T-sql)、SQL Server Management Studio (SSMS)、または Azure Data Studio を使用して SQL Server に AdventureWorks サンプルデータベースをダウンロードしてインストールするには、次の手順に従います。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/16/2020
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 1482104a0c8ffea7f7f2502b83b9b268b7bb08d2
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523957"
---
# <a name="adventureworks-sample-databases"></a>AdventureWorks サンプルデータベース
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

この記事では、AdventureWorks サンプルデータベースをダウンロードするための直接リンクと、それらを SQL Server および Azure SQL Database に復元する手順について説明します。 

サンプルの詳細については、 [GitHub リポジトリのサンプル](https://github.com/microsoft/sql-server-samples/tree/master/samples/databases)を参照してください。 

## <a name="prerequisites"></a>前提条件

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2019) または [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md) または [Azure Data Studio](../azure-data-studio/download-azure-data-studio.md)


## <a name="download-backup-files"></a>バックアップファイルのダウンロード 

次のリンクを使用して、シナリオに適したサンプルデータベースをダウンロードします。 

- **OLTP** データは、最も一般的なオンライントランザクション処理ワークロード用です。 
- データ**ウェアハウス (DW)** データは、データウェアハウスのワークロードを対象としています。 
- **ライトウェイト (LT)** データは、 **OLTP** サンプルの軽量で減らすダウンバージョンです。 

必要なものがわからない場合は、SQL Server バージョンと一致する OLTP バージョンから開始してください。 

|**OLTP** |**データ ウェアハウス (data warehouse)** |**軽量**|
|---------|---------|---------|
|[AdventureWorks2019](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2019.bak)|[AdventureWorksDW2019](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2019.bak)|[AdventureWorksLT2019](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2019.bak)|
|[AdventureWorks2017](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)|[AdventureWorksDW2017](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)|[AdventureWorksLT2017](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2017.bak)|
|[AdventureWorks2016](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)|[AdventureWorksDW2016](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)|[AdventureWorksLT2016](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2016.bak)|
|[AdventureWorks2016_EXT .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016_EXT.bak)|[AdventureWorksDW2016_EXT .bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016_EXT.bak)| 該当なし |
|[AdventureWorks2014](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)|[AdventureWorksDW2014](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)|[AdventureWorksLT2014](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2014.bak)|
|[AdventureWorks2012](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)|[AdventureWorksDW2012](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)|[AdventureWorksLT2012](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksLT2012.bak)|
|[AdventureWorks2008R2](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)| [AdventureWorksDW2008R2](https://github.com/microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-dw.bak) | 該当なし |

その他のファイルは、GitHub で直接見つけることができます。 

- [SQL Server 2014-2019](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [SQL Server 2012](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [SQL Server 2008 と2008R2](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)


## <a name="restore-to-sql-server"></a>SQL Server に復元 

このファイルを使用して、 `.bak` サンプルデータベースを SQL Server インスタンスに復元できます。 これを行うには、 [RESTORE (transact-sql)](../t-sql/statements/restore-statements-transact-sql.md) コマンドを使用するか、 [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md) または [AZURE DATA STUDIO](../azure-data-studio/download-azure-data-studio.md)のグラフィカルインターフェイス (GUI) を使用します。

# <a name="sql-server-management-studio-ssms"></a>[SQL Server Management Studio (SSMS)](#tab/ssms)

SQL Server Management Studio (SSMS) を使い慣れていない場合は、 [接続 & クエリ](../ssms/quickstarts/connect-query-sql-server.md) を使用して開始することができます。 

SQL Server Management Studio でデータベースを復元するには、次の手順を実行します。

1. `.bak`「[バックアップファイルのダウンロード](#download-backup-files)」セクションに記載されているいずれかのリンクから適切なファイルをダウンロードします。
2. ファイルを `.bak` SQL Server のバックアップ場所に移動します。 これは、インストール場所、インスタンス名、および SQL Server のバージョンによって異なります。 たとえば、SQL Server 2019 の既定のインスタンスの既定の場所は次のとおりです。

   `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup`. 

3. SQL Server Management Studio (SSMS) を開き、で SQL Server に接続します。 
4. データベースの復元ウィザードを起動するには**オブジェクトエクスプローラー**[データベースの復元 **] で [データベース]** を右クリックします。  >  **Restore Database...** **Restore Database** 

   :::image type="content" source="media/adventureworks-install-configure/restore-db-ssms.png" alt-text="オブジェクトエクスプローラーでデータベースを右クリックし、[データベースの復元] を選択して、データベースを復元する方法を示すスクリーンショット。":::


1. [ **デバイス** ] を選択し、省略記号 **(...)** を選択してデバイスを選択します。 
1. [ **追加** ] を選択し、 `.bak` 最近この場所に移動したファイルを選択します。 この場所にファイルを移動したが、ウィザードで表示できない場合は、通常、アクセス許可の問題が SQL Server か、このフォルダー内のこのファイルに対するアクセス許可が SQL Server にサインインしているユーザーがいないことを示しています。 
1. [ **OK]** を選択して、データベースのバックアップの選択を確認し、 **[バックアップデバイスの選択** ] ウィンドウを閉じます。 
1. [ **ファイル** ] タブを確認し **て、復元** の場所とファイル名が **データベースの復元** ウィザードの目的の場所とファイル名と一致していることを確認します。 
1. **[OK]** を選択してデータベースを復元します。 

   :::image type="content" source="media/adventureworks-install-configure/restore-db-wizard-ssms.png" alt-text="オブジェクトエクスプローラーでデータベースを右クリックし、[データベースの復元] を選択して、データベースを復元する方法を示すスクリーンショット。":::

SQL Server データベースの復元の詳細については、「 [SSMS を使用したデータベースバックアップの復元](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)」を参照してください。

# <a name="transact-sql-t-sql"></a>[Transact-SQL (T-SQL)](#tab/tsql)

Transact-sql (T-sql) を使用して、サンプルデータベースを復元できます。 AdventureWorks2019 を復元する例を以下に示しますが、データベース名とインストールファイルのパスは環境によって異なる場合があります。 

AdventureWorks2019 を復元するには、必要に応じて環境に合わせて値を変更し、次の Transact-sql (T-sql) コマンドを実行します。

```sql
USE [master]
RESTORE DATABASE [AdventureWorks2019] 
FROM  DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup\AdventureWorks2019.bak' 
WITH  FILE = 1,  NOUNLOAD,  STATS = 5
GO

```

# <a name="azure-data-studio"></a>[Azure Data Studio](#tab/data-studio)

[Azure Data Studio Studio](../azure-data-studio/download-azure-data-studio.md)を使い慣れていない場合は、[接続 & クエリ](../azure-data-studio/quickstart-sql-server.md)を使用して開始することができます。

Azure Data Studio でデータベースを復元するには、次の手順を実行します。

1. `.bak`「[バックアップファイルのダウンロード](#download-backup-files)」セクションに記載されているいずれかのリンクから適切なファイルをダウンロードします。
1. ファイルを `.bak` SQL Server のバックアップ場所に移動します。 これは、インストール場所、インスタンス名、および SQL Server のバージョンによって異なります。 たとえば、SQL Server 2019 の既定のインスタンスの既定の場所は次のとおりです。

    `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup`.

1. Azure Data Studio Studio を開き、SQL Server インスタンスに接続します。
1. サーバーを右クリックし、[ **管理**] を選択します。

   :::image type="content" source="media/adventureworks-install-configure/ads-manage.png" alt-text="オブジェクトエクスプローラーでデータベースを右クリックし、[データベースの復元] を選択して、データベースを復元する方法を示すスクリーンショット。":::

1. **復元**の選択

   :::image type="content" source="media/adventureworks-install-configure/ads-restore-database.png" alt-text="オブジェクトエクスプローラーでデータベースを右クリックし、[データベースの復元] を選択して、データベースを復元する方法を示すスクリーンショット。":::

1. [ **全般** ] タブで、[ **ソース**] の一覧に表示される値を入力します。
    1. [ **復元元**] で、[ *バックアップファイル*] を選択します。
    1. [ **バックアップファイルのパス**] で、.bak ファイルを保存した場所を選択します。 
    
   :::image type="content" source="media/adventureworks-install-configure/ads-source.png" alt-text="オブジェクトエクスプローラーでデータベースを右クリックし、[データベースの復元] を選択して、データベースを復元する方法を示すスクリーンショット。":::
    
    これにより、 **データベース**、 **ターゲットデータベース** 、復元などの残りのフィールドが自動的 **に**設定されます。 

   :::image type="content" source="media/adventureworks-install-configure/ads-destination-restore-plan.png" alt-text="オブジェクトエクスプローラーでデータベースを右クリックし、[データベースの復元] を選択して、データベースを復元する方法を示すスクリーンショット。":::

1. [ **復元** ] を選択して、データベースを復元します。 

   :::image type="content" source="media/adventureworks-install-configure/ads-restore.png" alt-text="オブジェクトエクスプローラーでデータベースを右クリックし、[データベースの復元] を選択して、データベースを復元する方法を示すスクリーンショット。":::

---

## <a name="deploy-to-azure-sql-database"></a>Azure SQL Database に配置する

サンプル Azure SQL Database データを表示するには、2つのオプションがあります。 新しいデータベースを作成するときにサンプルを使用することも、SQL Server Management Studio (SSMS) を使用して SQL Server から直接 Azure にデータベースをデプロイすることもできます。

代わりに Azure SQL Managed Instance のサンプルデータを取得するには、「 [sql Managed Instance に対して World Wide インポーターを復元](/azure/azure-sql/managed-instance/restore-sample-database-quickstart)する」を参照してください。 

### <a name="deploy-new-sample-database"></a>新しいサンプルデータベースのデプロイ

Azure SQL Database で新しいデータベースを作成する場合は、空のデータベースまたはサンプルデータベースを作成することができます。 

サンプルデータベースを使用して新しいデータベースを作成するには、次の手順に従います。 

1. Azure portal に接続します。
1. ナビゲーションウィンドウの左上にある [ **リソースの作成** ] を選択します。 
1. [ **データベース** ] を選択し、[ **SQL Database**] を選択します。 
1. 要求された情報を入力して、データベースを作成します。 
1. [**追加設定**] タブで、[**データソース**] の下の既存のデータとして [**サンプル**] を選択します。 

   :::image type="content" source="media/adventureworks-install-configure/deploy-sample-to-azure.png" alt-text="オブジェクトエクスプローラーでデータベースを右クリックし、[データベースの復元] を選択して、データベースを復元する方法を示すスクリーンショット。":::

1. [ **作成** ] を選択して、AdventureWorksLT データベースの復元されたコピーである新しい SQL Database を作成します。 


### <a name="deploy-database-from-sql-server"></a>SQL Server からデータベースを配置する

SQL Server Management Studio には、Azure SQL Database にデータベースを直接配置する機能が用意されています。 このメソッドは、現在、データの検証を提供していないので、開発とテストを目的としています。運用環境では使用しないでください。 

SQL Server から Azure SQL Database にサンプルデータベースを配置するには、次の手順を実行します。

1. SQL Server Management Studio で SQL Server に接続します。 
1. まだ実行していない場合は、 [サンプルデータベースを SQL Server に復元](#restore-to-sql-server)します。 
1. 復元したデータベースを右クリックし、**オブジェクトエクスプローラー**  >  **タスク**] [  >  **データベースを Microsoft Azure SQL Database に配置**...] の順にクリックします。 

   :::image type="content" source="media/adventureworks-install-configure/deploy-db-to-azure.png" alt-text="オブジェクトエクスプローラーでデータベースを右クリックし、[データベースの復元] を選択して、データベースを復元する方法を示すスクリーンショット。":::

1. ウィザードに従って Azure SQL Database に接続し、データベースをデプロイします。 


## <a name="creation-scripts"></a>作成スクリプト

データベースを復元する代わりに、スクリプトを使用して、バージョンに関係なく AdventureWorks データベースを作成することもできます。 

次のスクリプトを使用すると、AdventureWorks データベース全体を作成できます。 

- [AdventureWorks OLTP スクリプト Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [AdventureWorks DW スクリプト Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

スクリプトの使用に関する追加情報については、 [GitHub](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)を参照してください。 

## <a name="next-steps"></a>次のステップ

サンプルデータベースを復元したら、次のチュートリアルを使用して SQL Server を開始します。 


[SQL Server データベースエンジンのチュートリアル](../relational-databases/database-engine-tutorials.md)   
[SQL Server Management Studio を使用した接続とクエリ (SSMS)](../ssms/quickstarts/connect-query-sql-server.md)   
[Azure Data Studio を使用した接続とクエリ](../ssms/quickstarts/connect-query-sql-server.md)