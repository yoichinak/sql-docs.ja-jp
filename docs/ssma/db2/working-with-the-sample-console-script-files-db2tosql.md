---
description: サンプルのコンソールスクリプトファイルの操作 (DB2ToSQL)
title: サンプルのコンソールスクリプトファイルの操作 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5c3080c3-d074-4f99-a5f5-219ebeddc474
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: d609900151e7ced05be4cc92e65c06270b6ef8a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426924"
---
# <a name="working-with-the-sample-console-script-files-db2tosql"></a>サンプルのコンソールスクリプトファイルの操作 (DB2ToSQL)
ユーザー参照および使用のために、いくつかのサンプルファイルが製品と共に提供されています。 このセクションでは、エンドユーザーのニーズに合わせて、これらのスクリプトを簡単にカスタマイズする方法について説明します。  
  
## <a name="sample-console-script-files"></a>サンプルコンソールスクリプトファイル  
さまざまなシナリオをカバーする次のサンプルコンソールスクリプトファイルは、ユーザー参照用に用意されています。  
  
-   ServersConnectionFileSample.xml  
  
-   VariableValueFileSample.xml  
  
-   AssessmentReportGenerationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
1.  **ServersConnectionFileSample.xml:**  
  
    -   このサンプルでは、ソースとターゲットのデータベースで使用できるさまざまなモードの接続を提供し、ユーザーは要件に従って任意のモードを選択できます。 このサンプルには、サーバー定義が含まれています。  
  
    -   ユーザーは、必要なソースとターゲットのサーバー定義に値を変更するだけで、必要なデータベースに接続できます。 この例では、すべての値は、 **VariableValueFileSample.xml**で使用できる変数値として提供されています。  その他のすべての接続パラメーターは、ユーザーの作業サーバー接続ファイルから削除できます。  
  
    -   ソースサーバーとターゲットサーバーへの接続の詳細については、「 [DB2ToSQL&#41;&#40;のサーバー接続ファイルの作成 ](../../ssma/db2/creating-the-server-connection-files-db2tosql.md) 」を参照してください。  
  
2.  **VariableValueFileSample.xml:** サンプルコンソールスクリプトファイルで使用されており、 `ServersConnectionFileSample.xml` このファイルで照合されているすべての変数。 サンプルのコンソールスクリプトを実行するには、ユーザーがサンプル変数の値をユーザー定義の変数に置き換えるだけで、このファイルを追加のコマンドライン引数としてスクリプトファイルと共に渡す必要があります。  
  
    変数値ファイルの詳細については、「 [DB2ToSQL&#41;&#40;の変数値ファイルの作成 ](../../ssma/db2/creating-variable-value-files-db2tosql.md)」を参照してください。  
  
3.  **AssessmentReportGenerationSample.xml:** このサンプルを使用すると、データの変換と移行を開始する前にユーザーが分析に使用できる xml 評価レポートを生成できます。  
  
    このコマンドでは、 `generate-assessment-report` 属性の変数値 (参照 **VariableValueFileSample.xml**) を、 `object-name` ユーザーが使用しているデータベース名に変更する必要があります。 指定されたオブジェクトの種類によっては、 `object-type` 値も変更する必要があります。  
  
    ユーザーが複数のオブジェクトまたはデータベースを評価する必要がある場合は、 `metabase-object` サンプルの `generate-assessment-report` コンソールスクリプトファイルの例4に示すように、複数のノードを指定できます。  
  
    レポートの生成の詳細については、「 [レポートの生成 &#40;DB2ToSQL&#41;](../../ssma/db2/generating-reports-db2tosql.md)」を参照してください。  
  
    **注:**  
  
    変数値 file コマンドライン引数がコンソールアプリケーションに渡され、ユーザーが指定した値を使用して VariableValueFileSample.xml が更新されていることを確認します。  
  
    サーバー接続ファイルのコマンドライン引数がコンソールアプリケーションに渡され、ServersConnectionFileSample.xml が正しいサーバーパラメーター値で更新されていることを確認します。  
  
4.  **SqlStatementConversionSample.xml:** このサンプルを使用する `t-sql` `sql` と、入力として指定されたソースデータベースコマンドの対応するスクリプトをユーザーが生成できます。  
  
    このコマンドでは、 `convert-sql-statement` 属性の変数値 (参照 **VariableValueFileSample.xml**) `context` をユーザーが使用しているデータベース名に変更する必要があります。 ユーザーは、 `sql` 変換する必要があるソースデータベースコマンドに属性値を変更する必要もあり `sql` ます。  
  
    ユーザーは、変換する sql ファイルを指定することもできます。 これについては、 `convert-sql-statement` サンプルのコンソールスクリプトファイルのコマンド例4で説明しました。  
  
    > [!NOTE]  
    > 変数値 file コマンドライン引数がコンソールアプリケーションに渡され、ユーザーが指定した値を使用して VariableValueFileSample.xml が更新されていることを確認します。  
  
5.  **ConversionAndDataMigrationSample.xml:** このサンプルを使用すると、ユーザーはデータ移行への変換からエンドツーエンドの移行を実行できます。 変更する必要がある必須の属性値の一覧を次に示します。  
  
    |コマンド名|説明|属性|  
    |----------------|---------------|-------------|  
    |`map-schema`|転送元データベースから送信先スキーマへのスキーママッピング。|`source-schema:` を変換する必要があるソースデータベースを指定します。<br /><br />`sql-server-schema`: 移行先のターゲットデータベースを指定します。|  
    |`convert-schema`|送信元スキーマから送信先スキーマへのスキーマ変換を実行します。<br /><br />ユーザーが複数のオブジェクトまたはデータベースを評価する必要がある場合は、 `metabase-object` サンプルの `convert-schema` コンソールスクリプトファイルの例4に示すように、複数のノードを指定できます。|`object-name`: 変換する必要があるソースデータベースまたはオブジェクトの名前を指定します。 に指定されている `object-type` オブジェクトの型に基づいて、対応するが変更されていることを確認します。 `object-name`|  
    |`synchronize-target`|ターゲットデータベースとターゲットオブジェクトを同期します。<br /><br />ユーザーが複数のオブジェクトまたはデータベースを評価する必要がある場合は、 `metabase-object` `synchronize-target` サンプルコンソールスクリプトファイルのコマンド例3に示すように、複数のノードを指定できます。|`object-name:` を作成する必要がある sql server データベースまたはオブジェクトの名前を指定します。 に指定されている `object-type` オブジェクトの型に基づいて、対応するが変更されていることを確認します。 `object-name`|  
    |`migrate-data`|ソースデータをターゲットに移行します。<br /><br />ユーザーが複数のオブジェクトまたはデータベースを評価する必要がある場合は、 `metabase-object` サンプルの `migrate-data` コンソールスクリプトファイルの例2に示すように、複数のノードを指定できます。|`object-name:` 移行する必要があるソースデータベースまたはテーブルの名前を指定します。 に指定されている `object-type` オブジェクトの型に基づいて、対応するが変更されていることを確認します。 `object-name`|  
  
## <a name="see-also"></a>参照  
[DB2ToSQL&#41;&#40;の変数値ファイルの作成 ](../../ssma/db2/creating-variable-value-files-db2tosql.md)  
[DB2ToSQL&#41;&#40;のサーバー接続ファイルの作成 ](../../ssma/db2/creating-the-server-connection-files-db2tosql.md)  
[DB2ToSQL&#41;&#40;レポートの生成 ](../../ssma/db2/generating-reports-db2tosql.md)  
  
