---
title: CLR スカラー値関数 |Microsoft Docs
description: スカラー値関数は、1つの値を返します。 SQL Server CLR 統合では、スカラー値のユーザー定義関数をマネージコードで記述できます。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- SVF
- scalar-valued functions
ms.assetid: 20dcf802-c27d-4722-9cd3-206b1e77bee0
author: rothja
ms.author: jroth
ms.openlocfilehash: 7416b00b55ea680e25d80151957b3da0ccfc6351
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810388"
---
# <a name="clr-scalar-valued-functions"></a>CLR スカラー値関数
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  SVF (スカラー値関数) は、文字列値、整数値、ビット値などの単一値を返します。 スカラー値のユーザー定義関数は、任意の .NET Framework プログラミング言語を使用してマネージコードで作成できます。 これらの関数からは、[!INCLUDE[tsql](../../includes/tsql-md.md)] コードや他のマネージド コードにアクセスできます。 CLR 統合の利点とマネージコードとの使い分けの詳細については [!INCLUDE[tsql](../../includes/tsql-md.md)] 、「 [clr 統合の概要](../../relational-databases/clr-integration/clr-integration-overview.md)」を参照してください。  
  
## <a name="requirements-for-clr-scalar-valued-functions"></a>CLR スカラー値関数の要件  
 .NET Framework SVF は、.NET Framework アセンブリのクラスのメソッドとして実装されます。 入力パラメーターと SVF から返される型は、でサポートされている任意のスカラーデータ型にすることができます [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。ただし、 **varchar**、 **char**、 **rowversion**、 **text**、 **ntext**、 **image**、 **timestamp**、 **table**、 **cursor**は除きます。 SVF では、実装メソッドの戻り値のデータ型が上記のいずれかの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ型になるようにする必要があります。 型変換の詳細については、「 [CLR パラメーターデータのマッピング](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)」を参照してください。  
  
 .NET Framework の言語で .NET Framework を実装する場合、 **sqlfunction** カスタム属性を指定して、関数に関する追加情報を含めることができます。 **Sqlfunction**属性は、関数がデータにアクセスしたり、変更したりするかどうか、決定的であるかどうか、および関数が浮動小数点演算を必要とするかどうかを示します。  
  
 ユーザー定義スカラー値関数は、決定的関数になる場合と非決定的関数になる場合があります。 特定の入力パラメーターのセットを渡して決定的関数を呼び出すと、常に同じ結果が返されます。 一方、特定の入力パラメーターのセットを渡して非決定的関数を呼び出すと、異なる結果が返されることがあります。  
  
> [!NOTE]  
>  入力値とデータベースの状態が同じでも、関数が必ずしも常に同じ出力値を生成しない場合は、その関数を決定的関数としてマークしないでください。 完全に決定的ではない関数を決定的関数としてマークした場合、インデックス付きビューと計算列が破損する可能性があります。 **Isdeterministic**プロパティを true に設定して、関数を決定的としてマークします。  
  
### <a name="table-valued-parameters"></a>テーブル値パラメーター  
 テーブル値パラメーター (TVP) とは、プロシージャや関数に渡されるユーザー定義のテーブル型です。TVP を使用すると、複数行のデータを効率的にサーバーに渡すことができます。 TVP の機能はパラメーター配列に似ていますが、より柔軟性が高く、[!INCLUDE[tsql](../../includes/tsql-md.md)] との統合も緊密です。 テーブル値パラメーターを使用するとパフォーマンスが向上する可能性もあります。 また、サーバーへのラウンド トリップを減らすのにも役立ちます。 スカラー パラメーターのリストを使用するなどしてサーバーに複数の要求を送信する代わりに、データを TVP としてサーバーに送信できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のプロセスで実行されているマネージド ストアド プロシージャやマネージド関数にユーザー定義のテーブル型をテーブル値パラメーターとして渡したり、戻り値として受け取ったりすることはできません。 Tvp の詳細については、「 [データベースエンジン&#41;&#40;テーブル値パラメーターの使用 ](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)」を参照してください。  
  
## <a name="example-of-a-clr-scalar-valued-function"></a>CLR スカラー値関数の例  
 データにアクセスして整数値を返す簡単な SVF を次に示します。  
  
```csharp  
using Microsoft.SqlServer.Server;  
using System.Data.SqlClient;  
  
public class T  
{  
    [SqlFunction(DataAccess = DataAccessKind.Read)]  
    public static int ReturnOrderCount()  
    {  
        using (SqlConnection conn   
            = new SqlConnection("context connection=true"))  
        {  
            conn.Open();  
            SqlCommand cmd = new SqlCommand(  
                "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
            return (int)cmd.ExecuteScalar();  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Public Class T  
    <SqlFunction(DataAccess:=DataAccessKind.Read)> _  
    Public Shared Function ReturnOrderCount() As Integer  
        Using conn As New SqlConnection("context connection=true")  
            conn.Open()  
            Dim cmd As New SqlCommand("SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
            Return CType(cmd.ExecuteScalar(), Integer)  
        End Using  
    End Function  
End Class  
```  
  
 コードの1行目では、ADO.NET 名前空間にアクセスするために、**属性と system.string**にアクセスするために**Microsoft. SqlServer. サーバー**を参照しています。 (この名前空間には、 **SqlClient**、の .NET Framework Data Provider が含まれてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます)。  
  
 次に、関数は **sqlfunction** カスタム属性を受け取ります。これは、 **Microsoft の SqlServer** 名前空間にあります。 このカスタム属性は、UDF (ユーザー定義関数) がサーバーのデータを読み取るときにインプロセス プロバイダーを使用するかどうかを示します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、UDF によるデータの更新、挿入、または削除を許可していません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、インプロセス プロバイダーを使用しない UDF の実行を最適化できます。 これは、 **dataaccesskind** を **dataaccesskind**に設定することによって示されます。 その次の行で、対象のメソッドは public static (Visual Basic .NET では shared) になっています。  
  
 **SqlServer**名前空間にある**sqlcontext**クラスは、 **SqlCommand** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 既に設定されているインスタンスへの接続を使用して SqlCommand オブジェクトにアクセスできます。 ここでは使用しませんが、現在のトランザクションコンテキストは **、system.string アプリケーションプログラミング** インターフェイス (API) を介して使用することもできます。  
  
 関数本体のコードのほとんどの行は、 **system.string 名前空間** にある型を使用するクライアントアプリケーションを記述した開発者を対象としています。  
  
 [C#]  
  
```csharp
using(SqlConnection conn = new SqlConnection("context connection=true"))   
{  
   conn.Open();  
   SqlCommand cmd = new SqlCommand(  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn);  
   return (int) cmd.ExecuteScalar();  
}    
```  
  
 [Visual Basic]  
  
```vb
Using conn As New SqlConnection("context connection=true")  
   conn.Open()  
   Dim cmd As New SqlCommand( _  
        "SELECT COUNT(*) AS 'Order Count' FROM SalesOrderHeader", conn)  
   Return CType(cmd.ExecuteScalar(), Integer)  
End Using  
```  
  
 適切なコマンドテキストは、 **SqlCommand** オブジェクトを初期化することによって指定されます。 前の例では、テーブル **SalesOrderHeader**の行の数をカウントします。 次に、 **cmd**オブジェクトの**ExecuteScalar**メソッドが呼び出されます。 これにより、クエリに基づいて **int** 型の値が返されます。 最後に、注文数が呼び出し側に返されます。  
  
 このコードを FirstUdf.cs というファイルに保存すると、次のようにアセンブリとしてコンパイルできます。  
  
 [C#]  
  
```  
csc.exe /t:library /out:FirstUdf.dll FirstUdf.cs   
```  
  
 [Visual Basic]  
  
```  
vbc.exe /t:library /out:FirstUdf.dll FirstUdf.vb  
```  
  
> [!NOTE]  
>  `/t:library`は、実行可能ファイルではなくライブラリを生成することを示しています。 実行可能ファイルは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には登録できません。  
  
> [!NOTE]  
>  **/Clr: pure**でコンパイルされた Visual C++ データベースオブジェクトは、での実行がサポートされていません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 このようなデータベース オブジェクトには、スカラー値関数などがあります。  
  
 アセンブリと UDF を登録する [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリと呼び出しの例を次に示します。  
  
```sql
CREATE ASSEMBLY FirstUdf FROM 'FirstUdf.dll';  
GO  
  
CREATE FUNCTION CountSalesOrderHeader() RETURNS INT   
AS EXTERNAL NAME FirstUdf.T.ReturnOrderCount;   
GO  
  
SELECT dbo.CountSalesOrderHeader();  
GO  
  
```  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] で公開する関数名は、対象の public static メソッドの名前と一致している必要はありません。  
  
## <a name="see-also"></a>参照  
 [CLR パラメーターデータのマッピング](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)   
 [CLR 統合のカスタム属性の概要](../clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md)   
 [ユーザー定義関数](../../relational-databases/user-defined-functions/user-defined-functions.md)   
 [CLR データベース オブジェクトからのデータ アクセス](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
