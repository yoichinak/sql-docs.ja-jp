---
title: SqlPipe オブジェクト |Microsoft Docs
description: SQL Server で実行されている CLR データベースオブジェクトの場合、SqlPipe オブジェクトの Send メソッドを使用して、接続されているパイプに結果を送信できます。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- custom result sets [CLR integration]
- SqlPipe object
- tabular results
ms.assetid: 3e090faf-085f-4c01-a565-79e3f1c36e3b
author: rothja
ms.author: jroth
ms.openlocfilehash: 66b5478f23d771d9aa65f98f4bc7f29bcf885b25
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810866"
---
# <a name="sqlpipe-object"></a>SqlPipe オブジェクト
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、結果や出力パラメーターを呼び出し側のクライアントに送信するストアド プロシージャ (または拡張ストアド プロシージャ) を作成することがごく一般的でした。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)]ストアドプロシージャでは、0個以上の行を返す**SELECT**ステートメントは、接続された呼び出し元の "パイプ" に結果を送信します。  
  
 で実行される共通言語ランタイム (CLR) データベースオブジェクトの場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 **SqlPipe**オブジェクトの**send**メソッドを使用して、接続されているパイプに結果を送信できます。 **Sqlcontext**オブジェクトの**Pipe**プロパティにアクセスして、 **SqlPipe**オブジェクトを取得します。 **SqlPipe**クラスは、概念的には ASP.NET にある**Response**クラスに似ています。 詳細については、.NET Framework Software Development Kit の SqlPipe クラスのリファレンス ドキュメントを参照してください。  
  
## <a name="returning-tabular-results-and-messages"></a>表形式の結果とメッセージを返す  
 **SqlPipe**には、3つのオーバーロードを持つ**Send**メソッドがあります。 これらは次のとおりです。  
  
-   `void Send(string message)`  
  
-   `void Send(SqlDataReader reader)`  
  
-   `void Send(SqlDataRecord record)`  
  
 **Send**メソッドは、データをクライアントまたは呼び出し元に直接送信します。 通常は、 **SqlPipe**からの出力を使用するクライアントですが、入れ子になった CLR ストアドプロシージャの場合は、出力コンシューマーもストアドプロシージャにすることができます。 たとえば、Procedure1 がコマンド テキスト "EXEC Procedure2" の SqlCommand.ExecuteReader() を呼び出すとします。 Procedure2 もマネージド ストアド プロシージャです。 ここで Procedure2 が SqlPipe.Send( SqlDataRecord ) を呼び出すと、行はクライアントではなく、Procedure1 のリーダーに送信されます。  
  
 **Send**メソッドは、情報メッセージとしてクライアントに表示される文字列メッセージを送信します。これは、の PRINT に相当し [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。 また、 **SqlDataRecord**または **SqlDataReader**を使用した複数行の結果セットを使用して、単一行の結果セットを送信することもできます。  
  
 **SqlPipe**オブジェクトには、 **executeandsend**メソッドもあります。 このメソッドを使用して、( **SqlCommand** オブジェクトとして渡された) コマンドを実行し、結果を直接呼び出し元に返すことができます。 送信されたコマンドにエラーがある場合、パイプに例外が送信されますが、呼び出し元のマネージド コードにもコピーが送信されます。 呼び出し元コードが例外をキャッチしない場合は、履歴を伝わり [!INCLUDE[tsql](../../includes/tsql-md.md)] コードに反映され、2 度出力に表示されます。 呼び出し元コードが例外をキャッチした場合、パイプ コンシューマーにはまだエラーが表示されますが、重複するエラーはありません。  
  
 コンテキスト接続に関連付けられている **SqlCommand** のみを取得できます。非コンテキスト接続に関連付けられているコマンドを実行することはできません。  
  
## <a name="returning-custom-result-sets"></a>カスタム結果セットを返す  
 マネージストアドプロシージャは、 **SqlDataReader**からのものではない結果セットを送信できます。 Sendの **start** メソッドを **sendresult row** および **sendresultsstart**と共に使用すると、ストアドプロシージャからクライアントにカスタム結果セットを送信できます。  
  
 **Send、start** は、入力として **SqlDataRecord** を受け取ります。 さらに、結果セットの先頭にマークを付け、レコード メタデータを使用して、結果セットを説明するメタデータを生成します。 **Sendの start**を使用してレコードの値を送信することはありません。 **Sendの行**を使用して送信される後続のすべての行は、そのメタデータ定義と一致している必要があります。  
  
> [!NOTE]  
>  Sendの**start**メソッドを呼び出した後は、 **SendResultsRow** **Sendresultsstart と sendresultsstart**のみを呼び出すことができます。 **SqlPipe**の同じインスタンスで他のメソッドを呼び出すと、 **InvalidOperationException**が発生します。 **Sendresultsend** セットは、他のメソッドを呼び出すことができる初期状態に **SqlPipe** バックします。  
  
### <a name="example"></a>例  
 **Uspgetproductline**ストアドプロシージャは、指定された製品ライン内のすべての製品の名前、製品番号、色、および表示価格を返します。 このストアドプロシージャは、 *prodLine*と完全に一致するものを受け取ります。  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
  
public partial class StoredProcedures  
{  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void uspGetProductLine(SqlString prodLine)  
{  
    // Connect through the context connection.  
    using (SqlConnection connection = new SqlConnection("context connection=true"))  
    {  
        connection.Open();  
  
        SqlCommand command = new SqlCommand(  
            "SELECT Name, ProductNumber, Color, ListPrice " +  
            "FROM Production.Product " +   
            "WHERE ProductLine = @prodLine;", connection);  
  
        command.Parameters.AddWithValue("@prodLine", prodLine);  
  
        try  
        {  
            // Execute the command and send the results to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command);  
        }  
        catch (System.Data.SqlClient.SqlException ex)  
        {  
            // An error occurred executing the SQL command.  
        }  
     }  
}  
};  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.SqlClient  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
  
Partial Public Class StoredProcedures  
<Microsoft.SqlServer.Server.SqlProcedure()> _  
Public Shared Sub uspGetProductLine(ByVal prodLine As SqlString)  
    Dim command As SqlCommand  
  
    ' Connect through the context connection.  
    Using connection As New SqlConnection("context connection=true")  
        connection.Open()  
  
        command = New SqlCommand( _  
        "SELECT Name, ProductNumber, Color, ListPrice " & _  
        "FROM Production.Product " & _  
        "WHERE ProductLine = @prodLine;", connection)  
        command.Parameters.AddWithValue("@prodLine", prodLine)  
  
        Try  
            ' Execute the command and send the results   
            ' directly to the caller.  
            SqlContext.Pipe.ExecuteAndSend(command)  
        Catch ex As System.Data.SqlClient.SqlException  
            ' An error occurred executing the SQL command.  
        End Try  
    End Using  
End Sub  
End Class  
```  
  
 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントは、ツーリング自転車製品の一覧を返す **Uspgetproduct** プロシージャを実行します。  
  
```  
EXEC uspGetProductLineVB 'T';  
```  
  
## <a name="see-also"></a>参照  
 [SqlDataRecord オブジェクト](../../relational-databases/clr-integration-data-access-in-process-ado-net/sqldatarecord-object.md)   
 [CLR ストアドプロシージャ](/dotnet/framework/data/adonet/sql/clr-stored-procedures)   
 [ADO.NET に対する SQL Server インプロセス固有の拡張機能](../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)  
  
