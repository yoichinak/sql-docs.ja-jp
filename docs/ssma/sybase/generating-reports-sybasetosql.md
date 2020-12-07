---
description: レポートの生成 (SybaseToSQL)
title: レポートの生成 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,generating reports
- Sybase Console,refresh-from-database report
- Sybase Console,synchronize-target report
ms.assetid: 19278f6a-6d58-4867-9d71-c6228040466e
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 99516dc132f9c086c96bb3b886424927d68bab1b
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92034961"
---
# <a name="generating-reports-sybasetosql"></a>レポートの生成 (SybaseToSQL)
コマンドを使用して実行される特定のアクティビティのレポートは、SSMA コンソールのオブジェクトツリーレベルで生成されます。  
  
レポートを生成するには、次の手順に従います。  
  
1.  [ **書き込みの概要-レポート先** ] パラメーターを指定します。 関連するレポートは、ファイル名 (指定されている場合) または指定したフォルダーに格納されます。 次の表で説明するように、ファイル名はシステムで定義されています。 ** &lt; n &gt; **は、同じコマンドを実行するたびに数字で増加する一意のファイル番号です。  
  
    Reports vis vis コマンドは次のとおりです。  
  
    |法. いいえ。|command|レポート タイトル|  
    |-|-|-|  
    |1|生成-評価-レポート|AssessmentReport &lt; n &gt;XML|  
    |2|変換-スキーマ|SchemaConversionReport &lt; n &gt;XML|  
    |3|データの移行|DataMigrationReport &lt; n &gt;XML|  
    |4|convert-sql ステートメント|ConvertSQLReport &lt; n &gt; 。XML|  
    |5|同期-ターゲット|Target同期レポート &lt; n &gt; 。XML|  
    |6|データベースからの更新|SourceDBRefreshReport &lt; n &gt;XML|  
  
    > [!IMPORTANT]  
    > 出力レポートは、評価レポートとは異なります。 前者は、実行中のコマンドのパフォーマンスに関するレポートです。後者は、プログラムで使用するための XML レポートです。  
  
    出力レポートのコマンドオプション (Sl から)。 いいえ。 2-4) 「 [SSMA コンソールの実行 &#40;SybaseToSQL&#41;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md) 」セクションを参照してください。  
  
2.  レポートの詳細設定を使用して、出力レポートに必要な詳細の範囲を指定します。  
  
    |法. いいえ。|コマンドとパラメーター|出力の説明|  
    |-|-|-|  
    |1|verbose = "false"|アクティビティの概要レポートを生成します。|  
    |2|verbose = "true"|各活動の概要と詳細な状態レポートを生成します。|  
  
    > [!NOTE]  
    > 上記で指定したレポート詳細設定は、レポートの生成、スキーマの変換、スキーマの変換、データの移行、および sql ステートメントの変換に適用されます。  
  
3.  エラー報告の設定を使用して、エラーレポートに必要な詳細の範囲を指定します。  
  
    |法. いいえ。|コマンドとパラメーター|出力の説明|  
    |-|-|-|  
    |1|レポート-エラー = "false"|エラー/警告/情報メッセージについての詳細はありません。|  
    |2|レポート-エラー = "true"|詳細なエラー/警告/情報メッセージ。|  
  
    > [!NOTE]  
    > 上記で指定したエラー報告の設定は、[レポートの生成]、[スキーマの変換]、[スキーマの変換]、[データの移行]、[sql ステートメントの変換] の各コマンドに適用されます。  
  
```xml  
<generate-assessment-report  
  
    object-name="<object-name>"  
  
    object-type="<object-type>"  
  
    verbose="<true/false>"  
  
    report-erors="<true/false>"  
  
    write-summary-report-to="<file-name/folder-name>"  
  
    assessment-report-folder="<folder-name>"  
  
    assessment-report-overwrite="<true/false>"  
  
/>  
```  
  
### <a name="synchronize-target"></a>同期-ターゲット:  
コマンド **synchronize-target** には、同期操作のエラーレポートの場所を指定する " **レポートエラー-エラー-** パラメーター" があります。 次に、名前を指定してファイルを**Target同期し &lt; &gt; ます。XML**は、指定した場所に作成されます。ここで、 ** &lt; n &gt; **は、同じコマンドを実行するたびに数字で増加する一意のファイル番号です。  
  
**注:** フォルダーパスが指定されている場合、' report-errors-to ' パラメーターは、コマンド ' synchronize-target ' の省略可能な属性になります。  
  
```xml  
<!-- Example: Synchronize target entire Database with all attributes-->  
  
<synchronize-target  
  
    object-name="<object-name>"  
  
    on-error="<object-type>"  
  
    report-errors-to="<file-name/folder-name>"  
  
/>  
```  
**オブジェクト名:** 同期の対象となるオブジェクトを指定します (個々オブジェクト名またはグループオブジェクト名を使用することもできます)。  
  
**エラー発生時:** 同期エラーを警告またはエラーとして指定するかどうかを指定します。 エラー発生時に使用可能なオプション:  
  
-   レポート-合計-警告  
  
-   レポート-警告ごと  
  
-   失敗-スクリプト  
  
### <a name="refresh-from-database"></a>データベースからの更新:  
[ **データベースからの更新** ] コマンドには、[ **レポート-エラー-** ] パラメーターがあります。これにより、更新操作のエラーレポートの場所が指定されます。 次に、Sourcedbrefreshreport n という名前のファイルを作成し** &lt; &gt; ます。XML**は、指定した場所に作成されます。ここで、 ** &lt; n &gt; **は、同じコマンドを実行するたびに数字で増加する一意のファイル番号です。  
  
**注:** フォルダーパスが指定されている場合、' report-errors-to ' パラメーターは、コマンド ' synchronize-target ' の省略可能な属性になります。  
  
```xml  
<!-- Example: Refresh entire Schema (with all attributes)-->  
  
<refresh-from-database  
  
    object-name="<object-name>"  
  
    object-type ="<object-type>"  
  
    on-error="report-total-as-warning/report-each-as-warning/fail-script"  
  
    report-errors-to="<file-name/folder-name> "  
  
/>  
```  
**オブジェクト名:** 更新の対象となるオブジェクトを指定します (個々オブジェクト名またはグループオブジェクト名を使用することもできます)。  
  
**エラー発生時:** 更新エラーを警告またはエラーとして指定するかどうかを指定します。 エラー発生時に使用可能なオプション:  
  
-   レポート-合計-警告  
  
-   レポート-警告ごと  
  
-   失敗-スクリプト  
  
## <a name="see-also"></a>参照  
[SSMA コンソール (Sybase) の実行](./executing-the-ssma-console-sybasetosql.md)  
