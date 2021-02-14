---
title: SQL Server のデータベース単体テストに関する問題のトラブルシューティング
description: タイムアウト エラーやデータベースが予期しないターゲットに配置されるなど、SQL Server 単体テストで発生する可能性のある問題のトラブルシューティングのヒントを確認します。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: cf4c9cd1-7e73-4c3b-922a-68b9247e7b33
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 0bd87bb75255ca50ceaed8e46c356555cdedf799
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100066867"
---
# <a name="troubleshooting-sql-server-database-unit-testing-issues"></a>SQL Server のデータベース単体テストに関する問題のトラブルシューティング

ここで示されている問題は、データベースで SQL Server 単体テストを操作した場合に発生する可能性があります。  
  
-   [単体テストの実行時に単体テストと App.Config への変更が無視される](#UnitTestingAndAppConfigChanges)  
  
-   [単体テストの実行時にデータベースが予期しないターゲットに配置される](#DatabaseDeploymentInUnitTests)  
  
-   [データベース単体テストの実行時にタイムアウトする](#TimeoutsDuringUnitTests)  
  
## <a name="unit-testing-and-appconfig-changes-ignored-when-you-run-unit-tests"></a><a name="UnitTestingAndAppConfigChanges"></a>単体テストの実行時に単体テストと App.Config への変更が無視される  
テスト プロジェクトの App.Config ファイルを変更する場合、テスト プロジェクトをビルドし直さないと、その変更が反映されません。 これらの変更には、 **[SQL Server テスト構成]** ダイアログ ボックスを使用して App.Config に対して行う変更も含まれます。 テスト プロジェクトをビルドし直さない場合、単体テストを実行しても変更は適用されません。  
  
## <a name="database-deployment-to-unexpected-target-when-you-run-unit-tests"></a><a name="DatabaseDeploymentInUnitTests"></a>単体テストの実行時にデータベースが予期しないターゲットに配置される  
単体テストの実行時にデータベース プロジェクトからデータベースを配置する場合は、単体テスト構成で指定された接続文字列情報を使用してデータベースが配置されます。 データベース プロジェクトのデバッグ プロパティで指定された接続情報はこのタスクでは使用されないため、同じデータベースの異なるインスタンスに対して SQL Server 単体テストを実行できます。  
  
## <a name="timeouts-when-you-run-database-unit-tests"></a><a name="TimeoutsDuringUnitTests"></a>データベース単体テストの実行時にタイムアウトする  
タイムアウトが原因でデータベース単体テストが失敗する場合は、テスト プロジェクトの app.config ファイルを更新してタイムアウト期間を長くすることができます。 接続文字列で定義した接続のタイムアウトは、単体テストがサーバーに接続する際の待機時間を指定します。 app.config ファイルで直接定義する必要があるコマンド タイムアウトは、単体テストが Transact\-SQL スクリプトを実行する際の待機時間を指定します。 実行時間の長い単体テストで問題が発生した場合は、適切なコンテキスト要素でコマンド タイムアウト値を大きくしてください。 たとえば、**PrivilegedContext** 要素に 120 秒のコマンド タイムアウトを指定するには、app.config を次のように更新します。  
  
```  
<SqlUnitTesting_VS2010>  
    <DatabaseDeployment DatabaseProjectFileName="..\..\..\..\..\..\Visual Studio 2010\Projects\Database10\Database10\AdventureWorks.sqlproj"  
        Configuration="Debug" />  
    <DataGeneration ClearDatabase="true" />  
    <ExecutionContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(LocalDB)\Projects;Initial Catalog=AdventureWorks_Test;Integrated Security=True;Pooling=False"  
        CommandTimeout="30" />  
    <PrivilegedContext Provider="System.Data.SqlClient" ConnectionString="Data Source=(LocalDB)\Projects;Initial Catalog=AdventureWorks_Test;Integrated Security=True;Pooling=False"  
        CommandTimeout="120" />  
</SqlUnitTesting_VS2010>  
```  
  
## <a name="see-also"></a>参照  
[方法: 関数、トリガー、ストアド プロシージャに対する SQL Server の単体テストを作成する方法](../ssdt/how-to-create-unit-tests-for-functions-triggers-stored-procedures.md)  
[方法: SQL Server の単体テストの実行を構成する方法](../ssdt/how-to-configure-sql-server-unit-test-execution.md)  
  
