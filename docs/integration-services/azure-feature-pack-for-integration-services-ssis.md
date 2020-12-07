---
description: Integration Services (SSIS) 用の Azure Feature Pack
title: Integration Services (SSIS) 用の Azure Feature Pack | Microsoft Docs
ms.custom: ''
ms.date: 12/24/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.SSIS.AZURE.F1
- SQL14.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 63e40e66003737798c444f220058feceab69411a
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678918"
---
# <a name="azure-feature-pack-for-integration-services-ssis"></a>Integration Services (SSIS) 用の Azure Feature Pack

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


SQL Server Integration Services (SSIS) Feature Pack for Azure は、このページにリストされている SSIS のコンポーネントを提供して、Azure サービスへの接続、Azure とオンプレミスのデータ ソース間でのデータ転送、および Azure に格納されたデータの処理を行うための拡張機能です。

[![SSIS Feature Pack for Azure のダウンロード](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png)](https://www.microsoft.com/download/details.aspx?id=100430) **ダウンロード**

- SQL Server 2019 の場合 - [Microsoft SQL Server 2019 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=100430)
- SQL Server 2017 の場合 - [Microsoft SQL Server 2017 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=54798)
- SQL Server 2016 の場合 - [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=49492)
- SQL Server 2014 の場合 - [Microsoft SQL Server 2014 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=47366)
- SQL Server 2012 の場合 - [Microsoft SQL Server 2012 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=47367)

ダウンロード ページには、前提条件に関する情報も含まれます。 必ず SQL Server をインストールしてから Azure Feature Pack をサーバーにインストールします。そうしないと、サーバー上の SSIS カタログ データベース (SSISDB) にパッケージを展開するときに Feature Pack 内のコンポーネントを利用できない場合があります。

## <a name="components-in-the-feature-pack"></a>Feature Pack のコンポーネント
-   接続マネージャー

    -   [Azure Data Lake Analytics 接続マネージャー](connection-manager/azure-data-lake-analytics-connection-manager.md)

    -   [Azure Data Lake Store 接続マネージャー](../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)
    
    -   [Azure HDInsight 接続マネージャー](../integration-services/connection-manager/azure-hdinsight-connection-manager.md)

    -   [Azure Resource Manager の接続マネージャー](../integration-services/connection-manager/azure-resource-manager-connection-manager.md)
    
    -   [Azure Storage 接続マネージャー](../integration-services/connection-manager/azure-storage-connection-manager.md)

    -   [Azure サブスクリプション接続マネージャー](../integration-services/connection-manager/azure-subscription-connection-manager.md)
    
-   タスク

    -   [Azure BLOB のダウンロード タスク](../integration-services/control-flow/azure-blob-download-task.md)

    -   [Azure BLOB のアップロード タスク](../integration-services/control-flow/azure-blob-upload-task.md)

    -   [Azure Data Lake Analytics タスク](control-flow/azure-data-lake-analytics-task.md)

    -   [Azure Data Lake Store ファイル システム タスク](../integration-services/control-flow/azure-data-lake-store-file-system-task.md)

    -   [Azure HDInsight クラスターの作成タスク](../integration-services/control-flow/azure-hdinsight-create-cluster-task.md)

    -   [Azure HDInsight クラスターの削除タスク](../integration-services/control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Azure HDInsight Hive タスク](../integration-services/control-flow/azure-hdinsight-hive-task.md)

    -   [Azure HDInsight Pig タスク](../integration-services/control-flow/azure-hdinsight-pig-task.md)

    -   [Azure SQL DW のアップロード タスク](../integration-services/control-flow/azure-sql-dw-upload-task.md)

    -   [柔軟なファイル タスク](../integration-services/control-flow/flexible-file-task.md)

-   データ フロー コンポーネント

    -   [Azure BLOB Source](../integration-services/data-flow/azure-blob-source.md)

    -   [Azure Blob Destination](../integration-services/data-flow/azure-blob-destination.md)
    
    -   [Azure Data Lake Store Source](../integration-services/data-flow/azure-data-lake-store-source.md)
    
    -   [Azure Data Lake Store Destination](../integration-services/data-flow/azure-data-lake-store-destination.md)

    -   [柔軟なファイル ソース](../integration-services/data-flow/flexible-file-source.md)

    -   [柔軟なファイルの変換先](../integration-services/data-flow/flexible-file-destination.md)

-   Azure BLOB、Azure Data Lake Store、および Data Lake Storage Gen2 のファイル列挙子。 「[Foreach ループ コンテナー](../integration-services/control-flow/foreach-loop-container.md)」を参照してください。

## <a name="use-tls-12"></a>TLS 1.2 を使用する

Azure Feature Pack で使用される TLS のバージョンは、システム .NET Framework 設定に準拠しています。
TLS 1.2 を使用するには、次の 2 つのレジストリキーの下に `SchUseStrongCrypto` という名前の `REG_DWORD` 値をデータ `1` と共に追加します。

1. `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319`
2. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319`

## <a name="dependency-on-java"></a>Java への依存関係

Azure Data Lake Store/柔軟なファイル コネクタで ORC/Parquet ファイル形式を使用するには、Java が必要です。  
Java ビルドのアーキテクチャ (32/64 ビット) は、SSIS ランタイムのそれと一致しなければ使用できません。
次の Java ビルドがテストされています。

- [Zulu の OpenJDK 8u192](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Oracle の Java SE Runtime Environment 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

### <a name="set-up-zulus-openjdk"></a>Zulu の OpenJDK を設定する

1. インストール zip パッケージをダウンロードし、抽出します。
2. コマンド プロンプトから `sysdm.cpl` を実行します。
3. **[詳細設定]** タブの **[環境変数]** を選択します。
4. **[システム変数]** セクションで **[新規]** を選択します。
5. **[変数名]** に「`JAVA_HOME`」と入力します。
6. **[ディレクトリの参照]** を選択し、解凍したフォルダーに移動し、`jre` サブフォルダーを選択します。
   **[OK]** を選択すると、 **変数の値** が自動的に入力されます。
7. **[OK]** を選択し、 **[新しいシステム変数]** ダイアログ ボックスを閉じます。
8. **[OK]** を選択し、 **[環境変数]** ダイアログ ボックスを閉じます。
9. **[OK]** を選択して **[システム プロパティ]** ダイアログ ボックスを閉じます。

> [!TIP]
> Parquet 形式を使用し、"Java の呼び出し中にエラーが発生しました。メッセージ: **java.lang.OutOfMemoryError:Java heap space** " というエラーが発生した場合、環境変数 *`_JAVA_OPTIONS`* を追加し、JVM の最小/最大ヒープ サイズを調整できます。
>
>![jvm ヒープ](media/azure-feature-pack-jvm-heap-size.png)
>
> 例: 変数 *`_JAVA_OPTIONS`* を設定し、値 *`-Xms256m -Xmx16g`* を指定します。 フラグ Xms では、Java 仮想マシン (JVM) の初期メモリ割り当てプールを指定します。Xmx では、最大メモリ割り当てプールを指定します。 これは、JVM 起動時のメモリ量が *`Xms`* 、使用可能なメモリ量が最大で *`Xmx`* であることを意味します。 既定値は最小 64MB および最大 1G です。

### <a name="set-up-zulus-openjdk-on-azure-ssis-integration-runtime"></a>Azure-SSIS Integration Runtime で Zulu の OpenJDK を設定する

これは、Azure-SSIS Integration Runtime の[カスタム セットアップ インターフェイス](/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup)経由で行う必要があります。
`zulu8.33.0.1-jdk8.0.192-win_x64.zip` が使用されているとします。
BLOB コンテナーは次のように構成できます。

~~~
main.cmd
install_openjdk.ps1
zulu8.33.0.1-jdk8.0.192-win_x64.zip
~~~

エントリ ポイントとして、`main.cmd` により PowerShell スクリプト `install_openjdk.ps1` の実行がトリガーされます。それによって次に `zulu8.33.0.1-jdk8.0.192-win_x64.zip` が抽出され、それに応じて `JAVA_HOME` が設定されます。

**main.cmd**

~~~
powershell.exe -file install_openjdk.ps1
~~~

> [!TIP]
> Parquet 形式を使用し、"Java の呼び出し中にエラーが発生しました。メッセージ: **java.lang.OutOfMemoryError:Java heap space** " というエラーが発生した場合、 *`main.cmd`* でコマンドを追加し、JVM の最小/最大ヒープ サイズを調整できます。 例:
> ~~~
> setx /M _JAVA_OPTIONS "-Xms256m -Xmx16g"
> ~~~
> フラグ Xms では、Java 仮想マシン (JVM) の初期メモリ割り当てプールを指定します。Xmx では、最大メモリ割り当てプールを指定します。 これは、JVM 起動時のメモリ量が *`Xms`* 、使用可能なメモリ量が最大で *`Xmx`* であることを意味します。 既定値は最小 64MB および最大 1G です。

**install_openjdk.ps1**

~~~
Expand-Archive zulu8.33.0.1-jdk8.0.192-win_x64.zip -DestinationPath C:\
[Environment]::SetEnvironmentVariable("JAVA_HOME", "C:\zulu8.33.0.1-jdk8.0.192-win_x64\jre", "Machine")
~~~

### <a name="set-up-oracles-java-se-runtime-environment"></a>Oracle の Java SE Runtime Environment を設定する

1. exe インストーラーをダウンロードし、実行します。
2. インストーラーの指示に従い、設定を完了します。

## <a name="scenario-processing-big-data"></a>シナリオ:ビッグ データの処理
 Azure コネクタを使用して、次のビッグ データの処理を完了します。

1.  Azure Blob Upload Task を使用して、入力データを Azure Blob ストレージにアップロードします。

2.  Azure HDInsight Create Cluster Task を使用して、Azure HDInsight のクラスターを作成します。 独自のクラスターを使用する場合は、この手順は省略できます。

3.  Azure HDInsight Hive Task か Azure HDInsight Pig Task を使用して、Azure HDInsight クラスターで Pig または Hive ジョブを呼び出します。

4.  手順 2 でオンデマンドの HDInsight クラスターを作成した場合は、使用後の HDInsight クラスターを Azure HDInsight Delete Cluster Task で削除します。

5.  Azure HDInsight Blob Download Task を使用して、Azure Blob ストレージから Pig/Hive の出力データをダウンロードします。

![SSIS Azure コネクタのビッグ データのシナリオを示すスクリーンショット。](../integration-services/media/ssis-azureconnector-bigdatascenario.png)
 
## <a name="scenario-managing-data-in-the-cloud"></a>シナリオ:クラウド内のデータ管理
 SSIS パッケージ内の Azure Blob Destination を使用して、出力データを Azure Blob ストレージに書き込みむか、または Azure Blob Source を使用して、Azure Blob ストレージからデータを読み取ります。

![OLE DB ソースから Azure Blob Destination へのデータ フローを示すスクリーンショット。](../integration-services/media/ssis-azureconnector-cloudarchive-1.png)
 
 ![Azure BLOB Source から OLE DB 変換先へのデータ フローを示すスクリーンショット。](../integration-services/media/ssis-azureconnector-cloudarchive-2.png)

 Azure Blob 列挙子とともに Foreach ループ コンテナーを使用して、複数の BLOB ファイルのデータを処理します。

![制御フローで Foreach ループ コンテナーを示すスクリーンショット。](../integration-services/media/ssis-azureconnector-cloudarchive-3.png)

## <a name="release-notes"></a>リリース ノート

### <a name="version-1190"></a>バージョン 1.19.0

#### <a name="improvements"></a>機能強化

1. Azure Storage 接続マネージャーに Shared Access Signature 認証のサポートを追加。

### <a name="version-1180"></a>バージョン 1.18.0

#### <a name="improvements"></a>機能強化

1. Flexible File タスクの場合、次の 3 点で改善されます:(1) コピー操作と削除操作でワイルドカードが使用できるようになる、(2) ユーザーは削除操作で再帰的検索の有効と無効を切り替えることができる、(3) コピー操作のコピー先となるファイル名を空にし、コピー元のファイル名を維持できる。

### <a name="version-1170"></a>バージョン 1.17.0

これは、SQL Server 2019 に対してのみリリースされる修正プログラムのバージョンです。

#### <a name="bugfixes"></a>バグ修正

1. Visual Studio 2019 で実行し、SQL Server 2019 をターゲットにすると、柔軟なファイル タスクのソースまたは送信先が `Attempted to access an element as a type incompatible with the array.` というエラー メッセージで失敗する場合があります。
1. Visual Studio 2019 で実行し、SQL Server 2019 をターゲットにすると、ORC または Parquet 形式を使用した柔軟なファイルのソースまたは送信先が、`Microsoft.DataTransfer.Common.Shared.HybridDeliveryException: An unknown error occurred. JNI.JavaExceptionCheckException.` というエラー メッセージで失敗する場合があります。

### <a name="version-1160"></a>バージョン 1.16.0

#### <a name="bugfixes"></a>バグ修正

1. 場合によっては、パッケージの実行から "エラー:ファイルまたはアセンブリ 'Newtonsoft.Json, Version=11.0.0.0, Culture=neutral, PublicKeyToken=30ad4fe6b2a6aeed'、またはその依存関係の 1 つが読み込むことができませんでした。" が報告されます。

### <a name="version-1150"></a>バージョン 1.15.0

#### <a name="improvements"></a>機能強化

1. 柔軟なファイル タスクに、フォルダー/ファイルの削除操作が追加されます
1. 柔軟なファイル ソースに、外部/出力データ型の変換機能が追加されます

#### <a name="bugfixes"></a>バグ修正

1. 特定のケースで、"配列と互換性のない型の要素にアクセスしようとしました" というエラー メッセージと共に発生する Data Lake Storage Gen2 の接続障害がテストされます
1. Azure Storage エミュレーターのサポートが再開されます