---
title: コマンドプロンプトで Database Experimentation Assistant を実行する
description: コマンドプロンプトから、Database Experimentation Assistant (DEA) でトレースをキャプチャし、結果を分析する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 02/25/2020
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: pochiraju
ms.author: rajpo
ms.reviewer: mathoma
ms.openlocfilehash: 0e52cf31a94f2fd63f92305b80f7f7ae049c2809
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100066447"
---
# <a name="run-database-experimentation-assistant-at-a-command-prompt"></a>コマンドプロンプトで Database Experimentation Assistant を実行する

この記事では、Database Experimentation Assistant (DEA) でトレースをキャプチャし、その結果をすべてコマンドプロンプトから分析する方法について説明します。

   > [!NOTE]
   > 各 DEA 操作の詳細については、次のコマンドを実行してみてください。
   >
   > `Deacmd.exe -o <operation> --help`
   >
   > 操作名が必要です。有効な操作は、 **分析**、 **Startcapture**、および **stopcapture** です。

## <a name="start-a-new-workload-capture-by-using-the-dea-command"></a>DEA コマンドを使用して、新しいワークロードキャプチャを開始します。

新しいワークロードのキャプチャを開始するには、コマンドプロンプトで次のコマンドを実行します。

`Deacmd.exe -o StartCapture -n <Trace FileName> -x <Trace Format> -h <SQLServerInstance> -f <database name> -e <Encrypt Connection> -m <Authetication Mode> -u <user name> -p <password> -l <Location of Output Folder> -d <duration>`

**例**

`Deacmd.exe -o StartCapture -n sql2008capture -x 0 -h localhost -f adventureworks -e --trust -m 0 -l c:\test  -d 60`

**その他のオプション**

コマンドを使用して新しいワークロードキャプチャを開始するときに `Deacmd.exe` 、次の追加オプションを使用できます。

| オプション| 説明 |  
| --- | --- |
| -n, --name | 必要トレースファイル名 |
| -x、--format | 必要トレースの形式 (Trace = 0、Xevent = 1) |
| -d、--duration | 必要キャプチャの最大期間 (分) |
| -l, --location | 必要ホストコンピューターにトレース/xevent ファイルを格納するための出力フォルダーの場所 |
| -t、--type | (既定値: 0) Sql Server の種類/エディション (SqlServer = 0、AzureSQLDB = 1、Azure SQL Managed Instance = 2) |
| -h、--host | 必要SQL Server ホスト名またはインスタンス名を指定してキャプチャを開始します |
| -e、--暗号化 | (既定値: True)SQL Server インスタンスへの接続を暗号化します。 既定値は true です。 |
| --trust | (既定値: False)SQL Server インスタンスに接続しているときにサーバー証明書を信頼します。 既定値は false です。 |
| -f、--databasename | (既定値:)トレースをフィルター処理するデータベースの名前。指定しない場合は、すべてのデータベースでキャプチャが開始されます |
| -m、--authmode | (既定: 0) 認証モード (Windows = 0、Sql 認証 = 1) |
| -u、--username | SQL Server に接続するためのユーザー名 |
| -p、--password | SQL Server に接続するためのパスワード |

## <a name="replay-a-workload-capture"></a>ワークロードのキャプチャを再生する

**分散再生の使用**

分散再生を使用している場合は、次の手順を実行します。

1. 分散再生コントローラーコンピューターにログインします。
2. DEA コマンドを使用してキャプチャしたワークロードトレースを IRF ファイルに変換するには、コマンドプロンプトで次のコマンドを実行します。

    `DReplay preprocess -m "dreplaycontroller" -i "Path to first trace file" -d "<Folder path on controller>\IrfFolder"`

3. StartReplayCaptureTrace を使用して SQL Server を実行しているターゲットコンピューターでトレースキャプチャを開始します。

    a.  SQL Server Management Studio (SSMS) で、<Dea_InstallPath \Scripts\StartReplayCaptureTrace.sql. を開きます。 \>

    b.  を実行して、指定した `Set @durationInMins=0` 時間が経過するとトレースキャプチャが自動的に停止しないようにします。

    c.  トレースファイルあたりの最大ファイルサイズを設定するには、を実行 `Set @maxfilesize` します。 推奨サイズは 200 (MB) です。

    d.  を編集し `@Tracefile` て、トレースファイルの一意の名前を設定します。

    e.  `@dbname`ワークロードを特定のデータベースでのみキャプチャする必要がある場合は、データベース名を指定して編集します。 既定では、サーバー全体のワークロードがキャプチャされます。

4. ターゲット SQL Server インスタンスに対して IRF ファイルを再生するには、コマンドプロンプトで次のコマンドを実行します。

    `DReplay replay -m "dreplaycontroller" -d "<Folder Path on Dreplay Controller>\IrfFolder" -o -s "SQL2016Target" -w "dreplaychild1,dreplaychild2,dreplaycild3,dreplaychild4"`

    a.  ステータスを監視するには、コマンドプロンプトでを実行 `DReplay status -f 1` します。

    b.  再生を停止するには (たとえば、パス% が予想より低い場合)、コマンドプロンプトでを実行 `DReplay cancel` します。

5. ターゲット SQL Server インスタンスのトレースキャプチャを停止します。
6. SSMS でを開き `<Dea_InstallPath>\Scripts\StopCaptureTrace.sql` ます。
7. `@Tracefile`SQL Server を実行しているターゲットコンピューター上のトレースファイルのパスと一致するように、を編集します。
8. SQL Server を実行しているターゲットコンピューターに対してスクリプトを実行します。

**組み込み再生の使用**

組み込み再生を使用している場合は、分散再生を設定する必要はありません。 コマンドラインを使用して組み込みの再生を使用することはできますが、中間には、組み込みの再生を使用して、GUI を使用して再生を実行できます。

## <a name="analyze-traces-using-the-dea-command"></a>DEA コマンドを使用してトレースを分析する

新しいトレース分析を開始するには、コマンドプロンプトで次のコマンドを実行します。

`Deacmd.exe -o analysis -a <Target1 trace filepath> -b <Target2 trace filepath> -r reportname -h <SQLserverInstance> -e <encryptconnection> -u <username>`

**例**

`Deacmd.exe -o analysis -a C:\Trace\SQL2008Source\Trace.trc -b C:\ Trace\SQL2014Trace\Trace.trc -r upgrade20082014 -h localhost -e`

これらのトレースファイルの分析レポートを表示するには、GUI を使用してグラフや構成されたメトリックを表示する必要があります。  ただし、指定された SQL Server インスタンスに分析データベースが書き込まれるため、生成された分析テーブルに対して直接クエリを実行することもできます。

**その他のオプション**

DEA コマンドを使用してトレースを分析する場合は、次の追加オプションを使用できます。

| オプション| 説明 |  
| --- | --- |
| -a、--traceA | 必要インスタンスのイベントファイルへのファイルパス。 C:\traces\Sql2008trace.trc. の例  ファイルのバッチがある場合は、最初のファイルを選択し、DEA がロールオーバーファイルを自動的にチェックします。 ファイルが blob 内にある場合は、イベントファイルをローカルに保存するフォルダーのパスを指定します。  C:\traces\ の例 |
| -b、--traceB | 必要B インスタンスのイベントファイルへのファイルパス。 C:\traces\Sql2014trace.trc. の例 ファイルのバッチがある場合は、最初のファイルを選択し、DEA がロールオーバーファイルを自動的にチェックします。 ファイルが blob 内にある場合は、イベントファイルをローカルに保存するフォルダーのパスを指定します。  C:\traces\ の例 |
| -r、--ReportName | 必要現在の分析の名前。 生成された分析レポートは、この名前で識別されます。 |
| -t、--type | (既定値: 0) Sql Server の種類/エディション (SqlServer = 0、AzureSQLDB = 1、Azure SQL Managed Instance = 2) |
| -h、--host | 必要ホスト名またはインスタンス名の SQL Server |
| -e、--暗号化 | (既定値: True)SQL Server インスタンスへの接続を暗号化します。 既定値は true です。 |
| --trust | (既定値: False)SQL Server インスタンスに接続しているときにサーバー証明書を信頼します。 既定値は false です。 |
| -m、--authmode | (既定: 0) 認証モード (Windows = 0、Sql 認証 = 1) |
| -u、--username | SQL Server に接続するためのユーザー名 |
| --p | SQL Server に接続するためのパスワード |
| --ab | (既定値: False)トレース A の格納場所は blob です。 使用する場合は、--アブダビ (Blob Url のトレース) も指定する必要があります。 |
| --bb | (既定値: False)トレース B のストレージの場所は blob にあります。 使用する場合は、--bbu (Trace B Blob Url) も指定する必要があります。 |
| --アブダビ | SAS キーを持つインスタンスの Blob URL |
| --bbu | SAS キーを使用した B インスタンスの Blob URL |

## <a name="see-also"></a>関連項目

- DEA の使用方法の詳細については、「 [Database Experimentation Assistant の概要](database-experimentation-assistant-overview.md)」を参照してください。
