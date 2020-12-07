---
description: SSMS ユーティリティ
title: SSMS ユーティリティ
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], opening
- command prompt utilities [SQL Server], sqlwb
- sqlwb utility
- Management Studio command line
- opening SQL Server Management Studio
ms.assetid: aafda520-9e2a-4e1e-b936-1b165f1684e8
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 07/24/2020
ms.openlocfilehash: 4cc43babe2ae064731f293a0dc96219aaeced5a5
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036006"
---
# <a name="ssms-utility"></a>SSMS ユーティリティ

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

**SSMS** ユーティリティが [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開きます。 指定すると、 **Ssms** はサーバーへの接続を確立し、クエリ、スクリプト、ファイル、プロジェクト、ソリューションを開きます。

クエリ、プロジェクト、またはソリューションを含んだファイルを指定できます。 接続情報が指定され、ファイルの種類とサーバーの種類が対応している場合、クエリを含んだファイルは自動的にサーバーに接続されます。 たとえば、.sql ファイルならば、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の SQL クエリ エディター ウィンドウが開き、.mdx ファイルならば [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の MDX クエリ エディター ウィンドウが開きます。 **SQL Server のソリューションと SQL Server のプロジェクト**は、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] で開きます。

> [!NOTE]
> **Ssms** ユーティリティはクエリを実行しません。 コマンド ラインからクエリを実行するには、 **sqlcmd** ユーティリティを使用します。 

## <a name="syntax"></a>構文

```syntaxsql
Ssms
[scriptfile] [projectfile] [solutionfile] 
[-S servername] [-d databasename] [-G] [-U username] [-E] [-nosplash] [-log [filename]?] [-?] 
```

## <a name="arguments"></a>引数

*scriptfile* 開くスクリプト ファイルを 1 つ以上指定します。 パラメーターには、ファイルへの完全パスを含める必要があります。 

*projectfile* 開くスクリプト プロジェクトを指定します。 パラメーターには、スクリプト プロジェクト ファイルへの完全パスを含める必要があります。 

*solutionfile* 開くソリューションを指定します。 パラメーターには、ソリューション ファイルへの完全パスを含める必要があります。 

[ **-S** _servername_] サーバー名

[ **-d** _databasename_] データベース名

**[-G]** Azure Active Directory 認証を使用して接続します。 接続の種類は、 **-U** が含まれるかどうかで決まります。

> [!Note]
> **[Active Directory - MFA サポートで汎用]** は現在サポートされていません。

[ **-U** _username_] "SQL 認証" を使用して接続するときのユーザー名

> [!Note]
> **-P** は、SSMS バージョン 18.0 で削除されました。
>
> 対処法:UI を使用してサーバーに接続して、パスワードの保存を試みます。

**[-E]** Windows 認証を使用した接続

**[-nosplash]** [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開くとき、スプラッシュ スクリーンのグラフィックを表示しません。 限られた帯域幅を使用した接続では、ターミナル サービスを使用して [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を起動しているコンピューターへ接続する場合に、このオプションを使用してください。 この引数では、大文字と小文字は区別されず、他の引数の前後どちらにも指定できます。

[ **-log** _[filename]?_ ] トラブルシューティング用に指定したファイルに [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] のアクティビティを記録します。

**[-?]** コマンド ライン ヘルプを表示します。

## <a name="remarks"></a>解説

すべてのスイッチは省略可能で、コンマで区切られるファイル以外は、空白で区切られます。 スイッチを指定していない場合、 **Ssms** は、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] [ツール] **メニューの** [オプション] **設定で指定されているとおりに** を開きます。 たとえば、 **[環境/全般]** の **[スタートアップ時]** オプションで、 **[新しいクエリ ウィンドウを開く]** を指定すると、**Ssms** は空白のクエリ エディターで開きます。

**-log** スイッチは、他のすべてのスイッチの後の、コマンド ラインの末尾に指定する必要があります。 ファイル名引数は省略可能です。 ファイル名が指定され、そのファイルが存在しない場合は、ファイルが作成されます。 ファイルを作成できない場合 (書き込みアクセスが不十分な場合など)、ログはローカライズされていない APPDATA の場所 (下記を参照) に書き込まれます。 ファイル名引数を指定しない場合、2 つのファイルは、現在のユーザーのローカライズされていないアプリケーション データ フォルダーに書き込まれます。 SQL Server のローカライズされていないアプリケーション データ フォルダーは APPDATA 環境変数から確認できます。 たとえば、SQL Server 2012 の場合、フォルダーは \<system drive>:\Users\\<ユーザー名\>\AppData\Roaming\Microsoft\AppEnv\10.0\\ です。 2 つのファイルは、既定では ActivityLog.xml および ActivityLog.xsl という名前になります。 ActivityLog.xml にはアクティビティ ログ データが含まれ、ActivityLog.xsl は XML スタイル シートで、XML ファイルを簡単に表示できます。 Internet Explorer などの既定の XML ビューアーでログ ファイルを表示するには、次の手順に従います。[スタート] ボタンをクリックし、[ファイル名を指定して実行] をクリックし、表示されたフィールドに「\<system drive>:\Users\\<ユーザー名\>\AppData\Roaming\Microsoft\AppEnv\10.0\ActivityLog.xml」と入力して、Enter キーを押します。

接続情報が指定され、ファイルの種類とサーバーの種類が対応している場合、クエリを含んだファイルはサーバーへの接続を要求します。 たとえば、.sql ファイルならば、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の SQL クエリ エディター ウィンドウが開き、.mdx ファイルならば [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の MDX クエリ エディター ウィンドウが開きます。 **SQL Server のソリューションと SQL Server のプロジェクト**は、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] で開きます。

次の表では、ファイルの拡張子に対応するサーバーの種類を示します。

| サーバーの種類 | 拡張機能 |
|-------------|-----------|
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|.sql|
|SQL Server Analysis Services (SQL Server Analysis Services)|.mdx<br /><br /> .xmla|

## <a name="examples"></a>例

次のスクリプトは、既定の設定でコマンド プロンプトから [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開きます。

```console
  Ssms
```

次のスクリプトでは、"*Active Directory - 統合*" を使用してコマンド プロンプトから [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開きます。

```console
Ssms.exe -S servername.database.windows.net -G
```

次のスクリプトは、コマンド プロンプトから [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開きます。接続には Windows 認証を使用し、サーバー `ACCTG and the database AdventureWorks2012,` に対して設定されているコード エディターを使用します。また、スプラッシュ スクリーンは表示されません。

```console
Ssms -E -S ACCTG -d AdventureWorks2012 -nosplash
```

次のスクリプトは、コマンド プロンプトから [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開き、MonthEndQuery スクリプトを開きます。

```console
Ssms "C:\Documents and Settings\username\My Documents\SQL Server Management Studio Projects\FinanceScripts\FinanceScripts\MonthEndQuery.sql"
```

次のスクリプトは、コマンド プロンプトから [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開き、 `developer`という名前のコンピューター上にある NewReportsProject プロジェクトを開きます。

```console
Ssms "\\developer\fin\ReportProj\ReportProj\NewReportProj.ssmssqlproj"
```

次のスクリプトは、コマンド プロンプトから [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を開き、MonthlyReports ソリューションを開きます。 

```console
Ssms "C:\solutionsfolder\ReportProj\MonthlyReports.ssmssln"
```

## <a name="see-also"></a>参照

[SQL Server Management Studio の使用 [SQL Server]](./sql-server-management-studio-ssms.md)