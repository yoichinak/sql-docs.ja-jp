---
description: スクリプト ファイルの作成 (MySQLToSQL)
title: スクリプトファイルの作成 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Creating script files, configuring console settings
- Creating script files, Script commands
- Creating script files, script file validation
- Creating script files, server connection parameters
ms.assetid: b4608fe7-c777-4ba5-b853-4402f02109e3
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: bc77109e51cff1169105f39c1898dfd1fc32588c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472459"
---
# <a name="creating-script-files-mysqltosql"></a>スクリプト ファイルの作成 (MySQLToSQL)
SSMA コンソールアプリケーションを起動する前の最初の手順は、スクリプトファイルを作成し、必要に応じて変数値ファイルとサーバー接続ファイルを作成することです。  
  
スクリプトファイルは、次の3つのセクション可視化に分けることができます。  
  
1.  **構成:** コンソールアプリケーションの構成パラメーターをユーザーが設定できるようにします。  
  
2.  **サーバー:** ユーザーがソース/ターゲットサーバーの定義を設定できるようにします。 別のサーバー接続ファイルにすることもできます。  
  
3.  **スクリプト-コマンド:** ユーザーが SSMA ワークフローコマンドを実行できるようにします。  
  
各セクションについては、以下で詳しく説明します。  
  
## <a name="configuring-mysql-console-settings"></a>MySQL コンソール設定の構成  
スクリプトの構成は、コンソールのスクリプトファイルに表示されます。  
  
構成ノードで要素のいずれかが指定されている場合は、グローバル設定として設定されます。つまり、すべてのスクリプトコマンドに適用されます。 これらの構成要素は、ユーザーがグローバル設定をオーバーライドする場合は、[スクリプト-コマンド] セクションの各コマンド内で設定することもできます。  
  
ユーザーが構成可能なオプションは次のとおりです。  
  
1.  **出力ウィンドウプロバイダー:** "メッセージを表示しない" 属性が "true" に設定されている場合、コマンド固有のメッセージはコンソールに表示されません。 属性の説明は次のとおりです。  
  
    -   destination: 出力をファイルまたは stdout に印刷する必要があるかどうかを指定します。 既定では、これは false です。  
  
    -   ファイル名: ファイルのパス (省略可能)。  
  
    -   -メッセージの非表示: コンソールでメッセージを表示しません。 既定では ' false ' です。  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <output-window  
  
        suppress-messages="<true/false>"   (optional)  
  
        destination="<file/stdout>"        (optional)  
  
        file-name="<file-name>"            (optional)  
  
       />  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <...All commands...>  
  
      <output-window  
  
         suppress-messages="<true/false>"   (optional)  
  
         destination="<file/stdout>"        (optional)  
  
         file-name="<file-name>"            (optional)  
  
       />  
  
    </...All commands...>  
    ```  
  
2.  **データ移行接続プロバイダー:** これにより、データ移行の対象となるソース/ターゲットサーバーが指定されます。  ソース-使用-last-最後に使用されたソースサーバーがデータ移行に使用されることを示します。 同様に、target-last-used-最後に使用された対象サーバーがデータ移行に使用されることを示します。 ユーザーは、ソースサーバーまたはターゲットサーバーの属性を使用して、サーバー (ソースまたはターゲット) を指定することもできます。  
  
    次のように、1つまたは他の指定した属性のみを使用できます。  
  
    - ソース-使用-last-used = "true" (既定値) またはソースサーバー = "source_servername"  
  
    - target-last-used = "true" (既定値) または target-server = "target_servername"  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <data-migration-connection  source-use-last-used="true"  
  
                                  target-server="<target-server-unique-name>"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <migrate-data>  
  
      <data-migration-connection   source-server="<source-server-unique-name>"  
  
                                   target-use-last-used="true"/>  
  
    </migrate-data>  
    ```  
  
3.  **ユーザー入力ポップアップ:** これにより、オブジェクトがデータベースから読み込まれたときに、エラーを処理できます。 ユーザーは入力モードを提供し、エラーが発生した場合は、ユーザーが指定したとおりにコンソールが続行されます。  
  
    モードは次のとおりです。  
  
    -   **ask-ユーザー-** ユーザーに対して続行 (' yes ') またはエラー出力 (' no ') を求めるメッセージを表示します。  
  
    -   **エラー-** コンソールにエラーが表示され、実行が停止します。  
  
    -   **続行-** コンソールが実行を続行します。  
  
    既定のモードは **error**です。  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <!-- Connect to target database -->  
  
    <connect-target-database server="<target-server-unique-name>">  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </connect-target-database>  
    ```  
  
4.  **再接続プロバイダー:** これにより、接続エラーが発生した場合に、ユーザーは再接続設定を設定できます。 これは、ソースサーバーと対象サーバーの両方に設定できます。  
  
    再接続モードは次のとおりです。  
  
    -   [再接続-最後に使用されたサーバー]: 接続がアクティブでない場合、最大で5回使用された最後のサーバーへの再接続を試みます。  
  
    -   生成-エラー: 接続がアクティブでない場合は、エラーが生成されます。  
  
    既定のモードでは、 **エラー**が発生します。  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
    <reconnect-manager  on-source-reconnect="<reconnect-to-last-used-server/generate-an-error>"  
  
                        on-target-reconnect="<reconnect-to-last-used-server/generate-an-error>"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <!--synchronization-->  
  
    <synchronize-target>  
  
      <reconnect-manager on-target-reconnect="reconnect-to-last-used-server"/>  
  
    </synchronize-target>  
    ```  
    *or*  
  
    ```xml  
    <!--data migration-->  
  
    <migrate-data server="target-server-unique-name">  
  
      <reconnect-manager  
  
        on-source-reconnect="reconnect-to-last-used-server"  
  
        on-target-reconnect="generate-an-error"/>  
  
    </migrate-data>  
    ```  
  
5.  **コンバーターの上書きプロバイダー:** これにより、ターゲットメタベースに既に存在するオブジェクトをユーザーが処理できるようになります。 次のようなアクションが考えられます。  
  
    -   エラー: コンソールにエラーが表示され、実行が停止します。  
  
    -   overwrite: 既存のオブジェクトの値を上書きします。 この操作は、既定で実行されます。  
  
    -   スキップ: コンソールは、データベースに既に存在するオブジェクトをスキップします。  
  
    -   ask-ユーザー: 入力を求めるメッセージを表示します (' yes '/' no ')  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <convert-schema object-name="<object-name>">  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </convert-schema>  
    ```  
  
6.  **失敗した前提条件プロバイダー:** これにより、コマンドの処理に必要なすべての前提条件をユーザーが処理できるようになります。 既定では、strict モードは ' false ' です。 "True" に設定されている場合は、前提条件を満たすためにエラーが発生した場合に例外が生成されます。  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true/false>"/>  
  
    </output-providers>  
    ```  
  
7.  **操作の停止:** 途中操作中に、ユーザーが操作を停止したい場合は、 **Ctrl + C** キーを押すことができます。 SSMA for MySQL コンソールは、操作が完了するまで待機し、コンソールの実行を終了します。  
  
    ユーザーがすぐに実行を停止したい場合は、SSMA コンソールアプリケーションが突然終了するように、 **Ctrl + C** キーを再度押すことができます。  
  
8.  **進行状況プロバイダー:** 各コンソールコマンドの進行状況を通知します。 この機能は、既定では無効になっています。 進行状況レポートの属性は次のとおりです。  
  
    -   オフ  
  
    -   -1% ごと  
  
    -   -2% ごと  
  
    -   -5% ごと  
  
    -   -10% ごと  
  
    -   -20% ごと  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <progress-reporting enable="<true/false>"          (optional)  
  
                         report-messages="<true/false>"  (optional)  
  
                         report-progress="<every-1%/every-2%/every-5%/every-10%/every-20%/off>" (optional)/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <...All commands...>  
  
      <progress-reporting  
  
        enable="<true/false>"              (optional)  
  
        report-messages="<true/false>"     (optional)  
  
        report-progress="<every-1%/every-2%/every-5%/every-10%/every-20%/off>"     (optional)/>  
  
    </...All commands...>  
    ```  
  
9. **ロガーの詳細度:** ログの詳細レベルを設定します。 これは、UI の [すべてのカテゴリ] オプションに対応しています。 既定では、ログの詳細レベルは "エラー" です。  
  
    ロガーレベルのオプションは次のとおりです。  
  
    -   致命的-エラー: 致命的なエラーメッセージのみがログに記録されます。  
  
    -   エラー: エラーメッセージと致命的エラーメッセージのみが記録されます。  
  
    -   警告: デバッグメッセージと情報メッセージを除くすべてのレベルがログに記録されます。  
  
    -   info: デバッグメッセージを除くすべてのレベルがログに記録されます。  
  
    -   デバッグ: ログに記録されたすべてのレベルのメッセージ。  
  
    > [!NOTE]  
    > 必須のメッセージは、任意のレベルでログに記録されます。  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <log-verbosity level="<fatal-error/error/warning/info/debug>"/>  
  
    </output-providers>  
    ```  
    *or*  
  
    ```xml  
    <...All commands...>  
  
      <log-verbosity level="<fatal-error/error/warning/info/debug>"/>  
  
    </...All commands...>  
    ```  
  
10. **暗号化されたパスワードの上書き:** ' True ' の場合、サーバー接続ファイルまたはスクリプトファイルのサーバー定義セクションで指定されたクリアテキストのパスワードが存在する場合は、保護されたストレージに格納されている暗号化されたパスワードを上書きします。 パスワードがクリアテキストで指定されていない場合、ユーザーはパスワードの入力を求められます。  
  
    次の2つのケースが発生します。  
  
    1.  Override オプションが **false**の場合、検索の順序は "保護されたストレージ- &gt; スクリプトファイル- &gt; サーバー接続ファイル-プロンプトユーザー" になり &gt; ます。  
  
    2.  Override オプションが **true**の場合、検索の順序は、スクリプトファイル &gt; サーバー接続ファイルの &gt; プロンプトユーザーになります。  
  
    **例:**  
  
    ```xml  
    <output-providers>  
  
      <encrypted-password override="<true/false>"/>  
  
    </output-providers>  
    ```  
  
構成できないオプションは次のとおりです。  
  
-   **再接続の最大試行回数:** ネットワーク障害のために確立された接続がタイムアウトまたは中断した場合、サーバーに再接続する必要があります。 再接続の試行は最大 **5** 回まで許可され、その後、コンソールが再接続を自動的に実行します。 自動再接続の機能により、スクリプトを再実行する手間が軽減されます。  
  
## <a name="server-connection-parameters"></a>サーバー接続パラメーター  
サーバー接続パラメーターは、スクリプトファイルまたはサーバー接続ファイルで定義できます。 詳細については、 [&#40;MySQLToSQL&#41;のサーバー接続ファイルの作成 ](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md) に関するセクションを参照してください。  
  
## <a name="script-commands"></a>スクリプト コマンド  
このスクリプトファイルには、一連の移行ワークフローコマンドが XML 形式で含まれています。 SSMA コンソールアプリケーションは、スクリプトファイルに表示されるコマンドの順序で移行を処理します。  
  
たとえば、MySQL データベース内の特定のテーブルの典型的なデータ移行は、データベーステーブルの階層構造に従い &gt; ます。  
  
スクリプトファイル内のすべてのコマンドが正常に実行されると、SSMA コンソールアプリケーションが終了し、コントロールがユーザーに返されます。 スクリプトファイルの内容は、変数の [値のファイル](creating-variable-value-files-mysqltosql.md) に含まれる変数情報、または変数の値をスクリプトファイル内の別のセクションに格納することにより、静的なものになります。  
  
**例:**  
  
```xml  
<!--Sample of script file commands -->  
  
<ssma-script-file>  
  
  <script-commands>  
  
    <create-new-project project-folder="<project-folder>"  
  
                        project-name="<project-name>"  
  
                        overwrite-if-exists="<true/false>"/>  
  
    <connect-source-database server="<source-server-unique-name>"/>  
  
    <save-project/>  
  
    <close-project/>  
  
  </script-commands>  
  
</ssma-script-file>  
```  
3つのスクリプトファイル (さまざまなシナリオを実行するため)、変数値ファイル、およびサーバー接続ファイルで構成されるテンプレートは、product ディレクトリの Sample Console Scripts フォルダーにあります。  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   VariableValueFileSample.xml  
  
-   ServersConnectionFileSample.xml  
  
テンプレート (ファイル) は、関連性を確認するために表示されるパラメーターを変更した後に実行できます。  
  
スクリプトの完全な一覧については、「 [SSMA コンソール &#40;MySQLToSQL の実行](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)」を参照してください&#41;  
  
## <a name="script-file-validation"></a>スクリプトファイルの検証  
ユーザーは、' スキーマ ' フォルダーで使用可能なスキーマ定義ファイル **m 2ssconsolescriptschema** に対して、スクリプトファイルを簡単に検証できます。  
  
## <a name="next-step"></a>次の手順  
コンソールを操作する次の手順では、 [MySQLToSQL&#41;&#40;変数値ファイルを作成 ](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)します。  
  
## <a name="see-also"></a>参照  
[MySQLToSQL&#41;&#40;の変数値ファイルの作成 ](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
  
