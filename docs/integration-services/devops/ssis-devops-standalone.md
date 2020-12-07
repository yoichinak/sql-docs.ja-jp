---
title: スタンドアロン SQL Server Integration Services (SSIS) DevOps ツール | Microsoft Docs
description: スタンドアロン SSIS DevOps ツールで SSIS CICD をビルドする方法について説明します。
ms.date: 10/16/2020
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 52578422cc9f68c728c901cf39bf05425576133b
ms.sourcegitcommit: 36fe62a3ccf34979bfde3e192cfa778505add465
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "94521096"
---
# <a name="standalone-sql-server-integration-service-ssis-devops-tools-preview"></a>スタンドアロン SQL Server Integration Service (SSIS) DevOps ツール (プレビュー)

スタンドアロン **SSIS DevOps ツール** は、SSIS CICD タスクを実行するための一連の実行可能ファイルを提供します。 これらの実行可能ファイルは、Visual Studio や SSIS ランタイムのインストールに依存することなく、任意の CICD プラットフォームと簡単に統合できます。 提供される実行可能ファイルは次のとおりです。

- SSISBuild.exe: プロジェクト配置モデルまたはパッケージ配置モデル内で SSIS プロジェクトをビルドします。
- SSISDeploy.exe: ISPAC ファイルを SSIS カタログに配置するか、.DTSX ファイルとその依存関係をファイル システムに配置します。

## <a name="installation"></a>インストール

.NET Framework 4.6.2 以降が必要です。

[ダウンロード センター](https://aka.ms/AA9xp65)から最新のインストーラーをダウンロードし、ウィザードまたはコマンド ラインを使用してインストールします。

- ウィザードを使用してインストールする

インストールする .exe ファイルをダブルクリックし、実行可能ファイルと依存関係ファイルを抽出するフォルダーを指定します。

![インストール場所](media/installation-location.png)

- コマンド ラインを使用してインストールする

```
SSISDevOpsTools.exe /Q /C /T:<full path>
```

![インストールのコマンド ライン](media/installation-command-line.png)


## <a name="ssisbuildexe"></a>SSISBuild.exe

**構文**

```
SSISBuild.exe -project|-p:<dtproj file path> [-configuration|-c:<configuration name>] [-projectPassword|-pp:<project password>] [-stripSensitive|-ss] [-output|-o:<output path>] [-log|-l:<log level>[;<log path>]] [-quiet|-q] [-help|-h|-?]
```

**パラメーター**

|パラメーター|説明|
|---------|---------|
|-project \|-p:\<dtproj file path>|ビルドされる dtproj ファイルのファイル パス。|
|-configuration\|-c:\<configuration name>|ビルドに使用されるプロジェクト構成の名前。 指定されていない場合、dtproj ファイルに最初に定義されているプロジェクト構成が選択されます。|
|-projectPassword\|-pp:\<project password>|SSIS プロジェクトとそのパッケージのパスワード。 この引数は、SSIS プロジェクトとパッケージの保護レベルが EncryptSensitiveWithPassword または EncryptAllWithPassword の場合にのみ有効です。 パッケージ配置モデルでは、この引数で指定されたのと同じパスワードが、すべてのパッケージで共有される必要があります。|
|-stripSensitive\|-ss|SSIS プロジェクトの保護レベルを DontSaveSensitve に変換します。 保護レベルが EncryptSensitiveWithPassword または EncryptAllWithPassword の場合は、引数 -projectPassword を正しく設定する必要があります。 このオプションは、プロジェクト配置モデルに対してのみ有効です。|
|-output\|-o:\<output path>|ビルド成果物の出力パス。 プロジェクト構成の既定の出力パスは、この引数の値によって上書きされます。|
|-log\|-l:\<log level>[;\<log path>]|関連する設定をログに記録します。 <li>log level:ログ記録レベルがこれに等しいか、それ以上のログのみがログ ファイルに書き込まれます。 ログ記録レベルには、次の 4 つがあります (低レベルから高レベルへの昇順)。DIAG、INFO、WRN、ERR。 指定しなかった場合の既定のログ記録レベルは、INFO です。 <li> log path:ログを保持するファイルのパス。 パスを指定しなかった場合、ログ ファイルは生成されません。|
|-quiet\|-q|標準出力にログを表示しません。|
|-help\|-h\|-?|このコマンドライン ユーティリティの詳しい使用方法を表示します。|

**使用例**

- 最初に定義されたプロジェクト構成を使用し、パスワードによる暗号化を指定せずに dtproj をビルドします。    
    ```
    SSISBuild.exe -p:"C:\projects\demo\demo.dtproj"
    ```

- "DevConfiguration" 構成を使用し、パスワードによる暗号化を指定して dtproj をビルドし、指定のフォルダーにビルド成果物を出力します。
    ```
    SSISBuild.exe -p:C:\projects\demo\demo.dtproj -c:DevConfiguration -pp:encryptionpassword -o:D:\folder
    ```

- "DevConfiguration" 構成を使用し、パスワードによる暗号化、機密データのストライピング、およびログ レベル DIAG を指定して、dtproj をビルドします。
    ```
    SSISBuild.exe -p:C:\projects\demo\demo.dtproj -c:DevConfiguration -pp:encryptionpassword -ss -l:diag
    ```

## <a name="ssisdeployexe"></a>SSISDeploy.exe

**構文**

```
SSISDeploy.exe -source|-s:<source path> -destination|-d:<type>;<path>[;server] [-authType|-at:<auth type name>] [-connectionStringSuffix|-css:<connection string suffix>] [-projectPassword|-pp:<project password>] [-username|-u:<username>] [-password|-p:<password>] [-log|-l:<log level>[;<log path>]] [-quiet|-q] [-help|-h|-?]
```

**パラメーター**

|パラメーター|説明|
|---------|---------|
|-source\|-s:\<source path>|配置する成果物のローカル ファイル パス。 ISPAC、DTSX、DTSX のフォルダーのパス、SSISDeploymentManfiest が指定できます。|
|-destination\|-d:\<type>;\<path>[;server]|配置先の種類、ターゲット フォルダーのパス、およびソース ファイルの配置先となる SSIS カタログのサーバー名。 現在、配置先の種類として次の 2 つがサポートされています。 <li> *CATALOG*: 指定された SSIS カタログに、1 つまたは複数の ISPAC ファイルを配置します。 CATALOG の配置先のパスは、次の形式で指定する必要があります。 <br> /SSISDB/\<folder name>[/\<project name>] <br> オプションの <project name> は、ソースで単一の ISPAC ファイル パスが指定されている場合にのみ有効となります。 CATALOG の配置先の場合は、サーバー名を指定する必要があります。 <li> *FILE*: 1 つまたは複数の SSISDeploymentManifest ファイル内で指定された SSIS パッケージまたはファイルを、ファイル システムの指定されたパスに配置します。 FILE の配置先のパスは、次の形式のローカル フォルダー パスまたはネットワーク フォルダー パスにできます。 <br>\\\\\<machine name>\\\<folder name>[\\\<sub folder name>\...]|
|-authType\|-at:\<auth type name>|SQL Server にアクセスするための認証の種類。 CATALOG の配置先の場合は必須です。 次の種類がサポートされています。 <li> WIN:Windows 認証 <li> SQL: SQL Server 認証 <li> ADPWD:Active Directory - パスワード <li> ADINT:Active Directory - 統合|
|-connectionStringSuffix\|-css:\<connection string suffix> |SSIS カタログへの接続に使用される、接続文字列のサフィックス。|
|-projectPassword\|-pp:\<project password> |ISPAC または DTSX ファイルを復号化するためのパスワード。|
|-username\|-u:\<username>  |指定された SSIS カタログまたはファイル システムにアクセスするためのユーザー名。 ファイル システムへのアクセスには、プレフィックスとドメイン名を使用できます。|
|-password\|-p:\<password>  |指定された SSIS カタログまたはファイル システムにアクセスするためのパスワード。|
|-log\|-l:\<log level>[;\<log path>] |このユーティリティの実行に関連する設定をログに記録します。 <li> log level:ログ記録レベルがこれに等しいか、それ以上のログのみがログ ファイルに書き込まれます。 ログ記録レベルには、次の 4 つがあります (低レベルから高レベルへの昇順)。DIAG、INFO、WRN、ERR。 指定しなかった場合の既定のログ記録レベルは、INFO です。 <li> log path:ログを保持するファイルのパス。 パスを指定しなかった場合、ログ ファイルは生成されません。|
|-quiet\|-q |ログを標準出力に表示しません。|
|-help\|-h\|-?  |このコマンドライン ユーティリティの詳しい使用方法を表示します。|

**使用例**

- Windows 認証を使用して、パスワードで暗号化されていない単一の ISPAC を SSIS カタログに配置します。
    ```
    SSISDeploy.exe -s:D:\myfolder\demo.ispac -d:catalog;/SSISDB/destfolder;myssisserver -at:win
    ```

- SQL 認証を使用して、パスワードで暗号化された単一の ISPAC を SSIS カタログに配置し、プロジェクト名を変更します。
    ```
    SSISDeploy.exe -s:D:\myfolder\test.ispac -d:catalog;/SSISDB/folder/testproj;myssisserver -at:sql -u:sqlusername -p:sqlpassword -pp:encryptionpassword
    ```

- 単一の SSISDeploymentManifest とそれに関連付けられたファイルを、Azure ファイル共有に配置します。
    ```
    SSISDeploy.exe -s:D:\myfolder\mypackage.SSISDeploymentManifest -d:file;\\myssisshare.file.core.windows.net\destfolder -u:Azure\myssisshare -p:storagekey
    ```

- DTSX ファイルのフォルダーを、オンプレミスのファイル システムに配置します。
    ```
    SSISDeploy.exe -s:D:\myfolder -d:file;\\myssisshare\destfolder
    ```

## <a name="release-notes"></a>リリース ノート

### <a name="version-011-preview"></a>バージョン 0.1.1 プレビュー

リリース日:2020 年 11 月 11 日

- ispac を SSIS カタログに配置するときに、SSISDeploy.exe によるアセンブリの読み込みが失敗する問題を修正しました。

### <a name="version-010-preview"></a>バージョン 0.1.0 プレビュー

リリース日:2020 年 10 月 16 日

スタンドアロン SSIS DevOps ツールの初期プレビュー リリース。

## <a name="next-steps"></a>次のステップ

- [スタンドアロン SSIS DevOps ツール](https://aka.ms/AA9xp65)を入手する
- ご質問がある場合は、[Q&A](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools&ssr=false#qna) を参照してください
