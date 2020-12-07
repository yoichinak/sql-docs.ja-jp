---
description: SSMA コンソールのコマンドラインオプション (DB2ToSQL)
title: SSMA コンソールのコマンドラインオプション (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 237354e9-25c4-4386-9d1f-ca0618d4a9a0
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3dfef8a72c8c578b468ebcf34372e603579d13ed
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987438"
---
# <a name="command-line-options-in-ssma-console-db2tosql"></a>SSMA コンソールのコマンドラインオプション (DB2ToSQL)
Microsoft では、SSMA アクティビティを実行および制御するための強固な set コマンドラインオプションを提供しています。 以降のセクションでも同じことが説明されています。  
  
## <a name="command-line-options-in-ssma-console"></a>SSMA コンソールのコマンド ライン オプション  
ここでは、コンソールコマンドのオプションについて説明します。  
  
このセクションでは、"option" という用語は "switch" とも呼ばれます。  
  
オプションでは大文字と小文字が区別されず、' **-** ' または ' ' 文字で始めることができ **/** ます。  
  
オプションが指定されている場合は、対応するオプションパラメーターを指定することが必須になります。  
  
オプションパラメーターは、オプション文字から空白で区切る必要があります。  
  
**構文の例:**  
  
`C:\> SSMAforDB2Console.EXE -s scriptfile`  
  
`C:\> SSMAforDB2Console.EXE -s "C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \AssessmentReportGenerationSample.xml" -v "C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \VariableValueFileSample.xml" -c "C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ServersConnectionFileSample.xml"`  
  
スペースを含むフォルダーまたはファイル名は、二重引用符で囲んで指定する必要があります。  
  
コマンドラインエントリとエラーメッセージの出力は、STDOUT または指定したファイルに格納されます。  
  
### <a name="script-file-option--sscript"></a>スクリプトファイルのオプション:-s/スクリプト  
必須のスイッチであるスクリプトファイルのパス/名前は、SSMA によって実行されるコマンドシーケンスのスクリプトを指定します。  
  
**構文の例:**  
  
`C:\>SSMAforDB2Console.EXE -s "C Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml"`  
  
### <a name="variable-value-file-option--vvariable"></a>変数の値ファイルのオプション:-v/variable  
このファイルは、スクリプトファイルで使用される変数で構成されます。 これはオプションのスイッチです。 変数が変数ファイルで宣言されておらず、スクリプトファイルで使用されている場合は、アプリケーションによってエラーが生成され、コンソールの実行が終了します。  
  
**構文の例:**  
  
-   複数の変数値のファイルで定義された変数。たとえば、既定値を持つ変数と、該当する場合はインスタンス固有の値を持つ変数です。 変数が重複している場合、コマンドライン引数で指定された最後の変数ファイルは、次のように優先されます。  
  
    `C:\>SSMAforDB2Console.EXE -s`  
  
    `"C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml" -v c:\migration`  
  
    `projects\global_variablevaluefile.xml -v "c:\migrationprojects\instance_variablevaluefile.xml"`  
  
### <a name="server-connection-file-option--cserverconnection"></a>サーバー接続ファイルのオプション:-c/serverconnection  
このファイルには、各サーバーのサーバー接続情報が含まれています。 各サーバー定義は、一意のサーバー ID によって識別されます。 サーバー Id は、接続関連のコマンドのスクリプトファイルで参照されます。  
  
サーバー定義は、サーバー接続ファイルまたはスクリプトファイルの一部にすることができます。 サーバー id が重複している場合、スクリプトファイルのサーバー id はサーバー接続ファイルよりも優先されます。  
  
**構文の例:**  
  
-   サーバー Id はスクリプトファイルで使用され、別のサーバー接続ファイルで定義されます。サーバー接続ファイルでは、変数値ファイルで定義されている変数を使用します。  
  
    `C:\>SSMAforDB2Console.EXE -s "C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml"  -v`  
  
    `c:\SsmaProjects\myvaluefile1.xml -c`  
  
    `c:\SsmaProjects\myserverconnectionsfile1.xml`  
  
-   サーバー定義は、スクリプトファイルに埋め込まれています。  
  
    `C:\>SSMAforDB2Console.EXE -s "C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml"`  
  
### <a name="xml-output-option--xxmloutput-xmloutputfile"></a>XML 出力オプション:-x/xmloutput [xmloutputfile]  
このコマンドは、コマンド出力メッセージを xml 形式でコンソールまたは xml ファイルに出力するために使用されます。  
  
Xmloutput には、可視化の2つのオプションを使用できます。  
  
-   Xmloutput スイッチの後に filepath を指定した場合、出力はファイルにリダイレクトされます。  
  
    **構文の例:**  
  
    `C:\>SSMAforDB2Console.EXE -s`  
  
    `"C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml"  -x d:\xmloutput\project1output.xml`  
  
-   Xmloutput スイッチの後に filepath が指定されていない場合、xmloutput はコンソール自体に表示されます。  
  
    **構文の例:**  
  
    `C:\>SSMAforDB2Console.EXE -s "C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml"  -xmloutput`  
  
### <a name="log-file-option--llog"></a>ログファイルのオプション:-l/ログ  
コンソールアプリケーションのすべての SSMA 操作は、ログファイルに記録されます。 これはオプションのスイッチです。 ログファイルとそのパスがコマンドラインで指定されている場合、ログは指定した場所に生成されます。 それ以外の場合は、既定の場所に生成されます。  
  
**構文の例:**  
  
`C:\>SSMAforDB2Console.EXE`  
  
`"C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml"  -l c:\SsmaProjects\migration1.log`  
  
### <a name="project-environment-folder-option--eprojectenvironment"></a>プロジェクト環境フォルダーオプション:-e/projectenvironment  
これは、現在の SSMA プロジェクトのプロジェクト環境設定フォルダーを表します。 このスイッチは省略可能です。  
  
**構文の例:**  
  
`C:\>SSMAforDB2Console.EXE -s`  
  
`"C:\ Program Files\Microsoft SQL Server Migration Assistant for DB2\Sample Console Scripts \ConversionAndDataMigrationSample.xml"  -e c:\SsmaProjects\CommonEnvironment`  
  
### <a name="secure-password-option--psecurepassword"></a>セキュリティで保護されたパスワードオプション:-p/securepassword  
このオプションは、サーバー接続の暗号化されたパスワードを示します。 このオプションは、他のすべてのオプションとは異なります。このオプションでは、どのスクリプトも実行されず、移行に関連するアクティビティでも役に立ちませんが、移行プロジェクトで使用されるサーバー接続のパスワード暗号化の管理に役立ちます。  
  
コマンドラインパラメーターとして他のオプションやパスワードを入力することはできません。 それ以外の場合、エラーが発生します。 詳細については、「 [パスワードの管理](./managing-passwords-db2tosql.md) 」セクションを参照してください。  
  
では、次のサブオプションがサポートされてい `-p/securepassword` ます。  
  
-   指定したサーバー ID またはサーバー接続ファイルで定義されているすべてのサーバー Id の保護された記憶域にパスワードを追加する。 次の-overwrite オプションは、既に存在する場合、パスワードを更新します。  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}` `-c|-serverconnection <server-connection-file> [-v|variable <variable-value-file>]``[-o|overwrite]`  
  
    `-p|-securepassword -a|add    {"<server_id>[, .n]"|all}``-s|-script <server-connection-file> [-v|variable <variable-value-file>] [-o|overwrite]`  
  
-   暗号化されたパスワードを、指定したサーバー ID またはすべてのサーバー Id の保護された記憶域から削除するには、次のようにします。  
  
    `-p/securepassword -r/remove {<server_id> [, ...n] | all}`  
  
-   パスワードが暗号化されているサーバー Id の一覧を表示するには、次のようにします。  
  
    `-p/securepassword -l/list`  
  
-   保護された記憶域に格納されているパスワードを暗号化されたファイルにエクスポートします。 このファイルは、ユーザーが指定したパスフレーズで暗号化されます。  
  
    `-p/securepassword -e/export {<server-id> [, ...n] | all} <encrypted-password -file>`  
  
-   以前にエクスポートされた暗号化ファイルは、ユーザーが指定したパスフレーズを使用して、ローカルの保護されたストレージにインポートされます。 ファイルの暗号化が解除されると、新しいファイルに保存され、ローカルコンピューターで暗号化されます。  
  
    `-p/securepassword -i/import {<server-id> [, ...n] | all} <encrypted-password -file>`  
  
    複数のサーバー Id は、コンマ区切り記号を使用して指定できます。  
  
### <a name="help-option--help"></a>ヘルプオプション:-?/Help  
SSMA コンソールオプションの構文の概要が表示されます。  
  
`C:\>SSMAforDB2Console.EXE -?`  
  
SSMA コンソールのコマンドラインオプションの表形式の表示については、 [「付録-1 &#40;DB2ToSQL&#41;](../../ssma/db2/appendix-1-db2tosql.md)」を参照してください。  
  
### <a name="securepassword-help-option--securepassword--help"></a>SecurePassword ヘルプオプション:-securepassword-?/Help  
SSMA コンソールオプションの構文の概要が表示されます。  
  
`C:\>SSMAforDB2Console.EXE -securepassword -?`  
  
SSMA コンソールのコマンドラインオプションの表形式の表示については、 [「付録-1 &#40;DB2ToSQL](../../ssma/db2/appendix-1-db2tosql.md) 」を参照してください&#41;  
  
### <a name="next-step"></a>次の手順  
次の手順は、プロジェクトの要件によって異なります。  
  
1.  パスワードを指定する、またはパスワードをエクスポート/インポートする方法については、「パスワードの [管理 &#40;DB2ToSQL&#41;](../../ssma/db2/managing-passwords-db2tosql.md)」を参照してください。  
  
2.  レポートを生成する方法については、「 [レポートの生成 &#40;DB2ToSQL&#41;](../../ssma/db2/generating-reports-db2tosql.md)」を参照してください。  
  
3.  コンソールでの問題のトラブルシューティングについては、「 [&#40;DB2ToSQL&#41;のトラブルシューティング ](../../ssma/db2/troubleshooting-db2tosql.md)」を参照してください。  
