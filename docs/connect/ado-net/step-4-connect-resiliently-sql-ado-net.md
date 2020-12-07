---
title: 手順 4:ADO.NET で SQL に弾性的に接続する
description: 再試行ロジックを使用し ADO.NET を使用して SQL データベースへの接続の回復性を向上させる方法について説明します。
ms.custom: ''
ms.date: 08/15/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9b608b0b-6b38-42da-bb83-79df8c170cd7
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: d2a300ce4565d9eb6104dd73c89a7b30b7aa1e8e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725535"
---
# <a name="step-4-connect-resiliently-to-sql-with-adonet"></a>手順 4:ADO.NET で SQL に弾性的に接続する

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

- 前の記事:&nbsp;&nbsp;&nbsp;[手順 3: ADO.NET を使用した SQL への接続を概念実証する](step-3-connect-sql-ado-net.md)  

  
このトピックでは、カスタムの再試行ロジックを示す C# コード サンプルを提供します。 再試行ロジックによって信頼性が高まります。 この再試行ロジックは、プログラムが数秒間待機して再試行すると解消する傾向がある一時的なエラーや*一時的な障害*を適切に処理することを目的としています。  
  
一時的な障害の原因には、次のものがあります。  
  
- インターネットをサポートするネットワークの短時間の障害。  
- クエリが送信された時点で、クラウド システムがリソースの負荷分散を行っている可能性があります。  
  
  
ローカル Microsoft SQL Server に接続するための ADO.NET クラスでは、Azure SQL Database に接続することもできます。 ただし、ADO.NET クラス自体で、運用環境での使用に必要な堅牢性と信頼性がすべて提供されるわけではありません。 クライアント プログラムで一時的な障害が発生しても、そこから通知なしに正常に回復し、処理を続行できる場合があります。  
  
## <a name="step-1-identify-transient-errors"></a>手順 1:一時的なエラーを識別する  
  
プログラムでは、一時的なエラーと永続的なエラーを区別する必要があります。 一時的なエラーとは、一時的なネットワークの問題など、短期間で解消する可能性のあるエラー状態です。  永続的なエラーの例として、プログラムにターゲット データベース名のスペルミスが含まれており (この場合は、"そのようなデータベースは見つかりません" というエラーがいつまでも表示されます)、短期間で解消される見込みがない場合が考えられます。  
  
一時的な障害として分類されるエラー番号の一覧は、[SQL Database クライアント アプリケーションのエラー メッセージ](/azure/sql-database/sql-database-develop-error-messages/)に関するページに記載されています。  
  
## <a name="step-2-create-and-run-sample-application"></a>手順 2:サンプル アプリケーションを作成して実行する  
  
このサンプルは、.NET Framework 4.5.1 以降がインストールされていることを前提としています。  C# のコード サンプルは、Program.cs という名前の 1 つのファイルで構成されます。 次のセクションでコードについて説明します。  
  
### <a name="step-2a-capture-and-compile-the-code-sample"></a>手順 2.a: サンプル コードをキャプチャしてコンパイルする  
  
次の手順で、サンプルをコンパイルができます。  
  
1. [無料の Visual Studio Community edition](https://www.visualstudio.com/products/visual-studio-community-vs)、C# コンソール アプリケーション テンプレートから新しいプロジェクトを作成します。  
    - [ファイル]、[新規作成]、[プロジェクト]、[インストール済み]、[テンプレート]、[Visual C#]、[Windows]、[従来のデスクトップ]、[コンソール アプリケーション] の順にクリックします。  
    - プロジェクトに、「 **RetryAdo2**」という名前を付けます。  
2. [ソリューション エクスプローラー] ペインを開きます。  
    - プロジェクトの名前を確認します。  
    - Program.cs ファイルの名前を確認します。  
3. Program.cs ファイルを開きます。  
4. Program.cs ファイルの内容全体を次のコード ブロックのコードに置き換えます。  
5. メニューで [ビルド]、[ソリューションのビルド] の順にクリックします。  
  
### <a name="step-2b-copy-and-paste-sample-code"></a>手順 2.b: サンプル コードをコピーして貼り付ける  
  
このコードを、 **Program.cs** ファイルに貼り付けます。  
  
次にサーバー名、パスワードなどの文字列を編集する必要があります。 これらの文字列は、 **GetSqlConnectionStringBuilder**という名前のメソッドにあります。  
  
注:このサーバー名の接続文字列には **tcp:** の 4 文字のプレフィックスが含まれているため、Azure SQL Database 向けになっています。 ただし、このサーバー文字列は、Microsoft SQL Server に接続するように調整することができます。  
  
  
```csharp
using System;  // C#  
using CG = System.Collections.Generic;  
using QC = Microsoft.Data.SqlClient;  
using TD = System.Threading;  
    
namespace RetryAdo2  
{  
  public class Program  
  {  
    static public int Main(string[] args)  
    {  
      bool succeeded = false;  
      int totalNumberOfTimesToTry = 4;  
      int retryIntervalSeconds = 10;  
    
      for (int tries = 1;  
        tries <= totalNumberOfTimesToTry;  
        tries++)  
      {  
        try  
        {  
          if (tries > 1)  
          {  
            Console.WriteLine  
              ("Transient error encountered. Will begin attempt number {0} of {1} max...",  
              tries, totalNumberOfTimesToTry  
              );  
            TD.Thread.Sleep(1000 * retryIntervalSeconds);  
            retryIntervalSeconds = Convert.ToInt32  
              (retryIntervalSeconds * 1.5);  
          }  
          AccessDatabase();  
          succeeded = true;  
          break;  
        }  
    
        catch (QC.SqlException sqlExc)  
        {  
          if (TransientErrorNumbers.Contains  
            (sqlExc.Number) == true)  
          {  
            Console.WriteLine("{0}: transient occurred.", sqlExc.Number);  
            continue;  
          }  
          else  
          {  
            Console.WriteLine(sqlExc);  
            succeeded = false;  
            break;  
          }  
        }  
    
        catch (TestSqlException sqlExc)  
        {  
          if (TransientErrorNumbers.Contains  
            (sqlExc.Number) == true)  
          {  
            Console.WriteLine("{0}: transient occurred. (TESTING.)", sqlExc.Number);  
            continue;  
          }  
          else  
          {  
            Console.WriteLine(sqlExc);  
            succeeded = false;  
            break;  
          }  
        }  
    
        catch (Exception Exc)  
        {  
          Console.WriteLine(Exc);  
          succeeded = false;  
          break;  
        }  
      }  
    
      if (succeeded == true)  
      {  
        return 0;  
      }  
      else  
      {  
        Console.WriteLine("ERROR: Unable to access the database!");  
        return 1;  
      }  
    }  
    
    /// <summary>  
    /// Connects to the database, reads,  
    /// prints results to the console.  
    /// </summary>  
    static public void AccessDatabase()  
    {  
      //throw new TestSqlException(4060); //(7654321);  // Uncomment for testing.  
    
      using (var sqlConnection = new QC.SqlConnection  
          (GetSqlConnectionString()))  
      {  
        using (var dbCommand = sqlConnection.CreateCommand())  
        {  
          dbCommand.CommandText = @"  
SELECT TOP 3  
    ob.name,  
    CAST(ob.object_id as nvarchar(32)) as [object_id]  
  FROM sys.objects as ob  
  WHERE ob.type='IT'  
  ORDER BY ob.name;";  
    
          sqlConnection.Open();  
          var dataReader = dbCommand.ExecuteReader();  
    
          while (dataReader.Read())  
          {  
            Console.WriteLine("{0}\t{1}",  
              dataReader.GetString(0),  
              dataReader.GetString(1));  
          }  
        }  
      }  
    }  
    
    /// <summary>  
    /// You must edit the four 'my' string values.  
    /// </summary>  
    /// <returns>An ADO.NET connection string.</returns>  
    static private string GetSqlConnectionString()  
    {  
      // Prepare the connection string to Azure SQL Database.  
      var sqlConnectionSB = new QC.SqlConnectionStringBuilder();  
    
      // Change these values to your values.  
      sqlConnectionSB.DataSource = "tcp:myazuresqldbserver.database.windows.net,1433"; //["Server"]  
      sqlConnectionSB.InitialCatalog = "MyDatabase"; //["Database"]  
    
      sqlConnectionSB.UserID = "MyLogin";  // "@yourservername"  as suffix sometimes.  
      sqlConnectionSB.Password = "MyPassword";  
      sqlConnectionSB.IntegratedSecurity = false;  
    
      // Adjust these values if you like. (ADO.NET 4.5.1 or later.)  
      sqlConnectionSB.ConnectRetryCount = 3;  
      sqlConnectionSB.ConnectRetryInterval = 10;  // Seconds.  
    
      // Leave these values as they are.  
      sqlConnectionSB.IntegratedSecurity = false;  
      sqlConnectionSB.Encrypt = true;  
      sqlConnectionSB.ConnectTimeout = 30;  
    
      return sqlConnectionSB.ToString();  
    }  
    
    static public CG.List<int> TransientErrorNumbers =  
      new CG.List<int> { 4060, 40197, 40501, 40613,  
      49918, 49919, 49920, 11001 };  
  }  
    
  /// <summary>  
  /// For testing retry logic, you can have method  
  /// AccessDatabase start by throwing a new  
  /// TestSqlException with a Number that does  
  /// or does not match a transient error number  
  /// present in TransientErrorNumbers.  
  /// </summary>  
  internal class TestSqlException : ApplicationException  
  {  
    internal TestSqlException(int testErrorNumber)  
    { this.Number = testErrorNumber; }  
    
    internal int Number  
    { get; set; }  
  }  
}  
```  
  
###  <a name="step-2c-run-the-program"></a>手順 2.c: プログラムの実行  
  
  
**RetryAdo2.exe** 実行可能ファイルにはパラメーターを入力しません。 .exe ファイルを実行するには、次のようにします。  
  
1. RetryAdo2.exe バイナリをコンパイルした場所にコンソール ウィンドウを開きます。  
2. 入力パラメーターなしで RetryAdo2.exe を実行します。  
  
  
  
```  
database_firewall_rules_table   245575913  
filestream_tombstone_2073058421 2073058421  
filetable_updates_2105058535    2105058535  
```  
  
  
  
## <a name="step-3-ways-to-test-your-retry-logic"></a>手順 3:再試行ロジックをテストする方法  
  
一時的なエラーをシミュレートして再試行ロジックをテストするには、いくつかの方法があります。  
  
  
###  <a name="step-3a-throw-a-test-exception"></a>手順 3.a: テスト例外をスローする  
  
コード サンプルには、以下のものが含まれています。  
  
- **Number** という名前のプロパティを含む、**TestSqlException** という名前の小さな 2 番目のクラス。  
- `//throw new TestSqlException(4060);` のコメントを解除できます。  
  
throw ステートメントのコメントを解除して再コンパイルすると、**RetryAdo2.exe** の次回の実行によって次のような行が出力されます。  
  
```  
[C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
>> RetryAdo2.exe  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 2 of 4 max...  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 3 of 4 max...  
4060: transient occurred. (TESTING.)  
Transient error encountered. Will begin attempt number 4 of 4 max...  
4060: transient occurred. (TESTING.)  
ERROR: Unable to access the database!  
  
[C:\VS15\RetryAdo2\RetryAdo2\bin\Debug\]  
>>  
```  
  
###  <a name="step-3b-retest-with-a-persistent-error"></a>手順 3.b: 永続的なエラーで再テストする  
  
コードが永続的なエラーを適切に処理できることを確かめるには、前のテストを再実行します。ただし、4060 などの実際の一時的なエラーの番号は使用しないでください。 代わりに、意味のない番号 7654321 を使用します。 プログラムはこれを永続的なエラーとして扱い、再試行をすべてバイパスするはずです。  
  
###  <a name="step-3c-disconnect-from-the-network"></a>手順 3.c: ネットワークから切断する  
  
1. クライアント コンピューターをネットワークから切断します。  
    - デスクトップの場合、ネットワーク ケーブルを外します。  
    - ラップトップの場合、ファンクション キーの組み合わせを押してネットワーク アダプターをオフにします。  
2. RetryAdo2.exe を起動し、最初の一時的なエラーがコンソールに表示されるのを待ちます (おそらく 11001)。  
3. RetryAdo2.exe が実行している間に、ネットワークに再接続します。  
4. 続いて行われる再試行が成功したことをコンソールで確認します。  
  
  
###  <a name="step-2d-temporarily-misspell-the-server-name"></a>手順 2.d: 一時的にスペルミスのあるサーバー名を使用する  
  
1. 一時的に 40615 を別のエラー番号として **TransientErrorNumbers**に追加し、再コンパイルします。  
2. `new QC.SqlConnectionStringBuilder()`の行にブレークポイントを設定します。  
3. *[エディット コンティニュ]* 機能を使用して、数行下で意図的にサーバー名のスペルを間違えます。  
    - プログラムを実行し、ブレークポイントに戻ります。  
    - 40615 エラーが発生します。  
4. スペルミスを修正します。  
5. プログラムを実行すると正常に終了します。  
6. 40615 を削除し、再コンパイルします。  
  
## <a name="next-steps"></a>次のステップ  
  
他のベスト プラクティスおよびデザイン ガイドラインを調べるには、[SQL Database への接続: リンク、ベスト プラクティスおよびデザイン ガイドライン](/azure/azure-sql/database/develop-overview)に関するページを参照してください。