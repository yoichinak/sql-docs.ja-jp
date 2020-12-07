---
title: CLR 統合を使用したはじめに |Microsoft Docs
description: この記事では、.NET Framework CLR との Microsoft SQL Server 統合を使用してデータベースオブジェクトをコンパイルするために必要な名前空間とライブラリについて説明します。
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: quickstart
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- database objects [CLR integration]
- namespaces [CLR integration]
- database objects [CLR integration], about CLR integration
- stored procedures [CLR integration]
- common language runtime [SQL Server], about CLR integration
- building database objects [CLR integration], about CLR integration
- common language runtime [SQL Server], stored procedures
- common language runtime [SQL Server], namespaces
- Hello World example [CLR integration]
- library [CLR integration]
ms.assetid: c73e628a-f54a-411a-bfe3-6dae519316cc
author: rothja
ms.author: jroth
ms.openlocfilehash: c307172d7bf8b258cbd56b4ef4abfe6704750358
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192362"
---
# <a name="getting-started-with-clr-integration"></a>CLR 統合の概要

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

このトピックでは、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .NET Framework 共通言語ランタイム (CLR) との統合を使用してデータベースオブジェクトをコンパイルするために必要な名前空間とライブラリの概要について説明します。 また、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# を使用した簡単な CLR ストアド プロシージャを記述、コンパイル、および実行する方法についても説明します。  
  
## <a name="required-namespaces"></a>必要な名前空間  

基本的な CLR データベースオブジェクトの開発に必要なコンポーネントは、と共にインストールされ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ます。 CLR 統合機能は、.NET Framework の一部である system.data.dll というアセンブリで公開されます。 このアセンブリは、.NET Framework ディレクトリ内だけでなく、GAC (グローバル アセンブリ キャッシュ) 内にもあります。 通常、このアセンブリへの参照は、コマンド ライン ツールと [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio の両方で自動的に追加されるので、手動で追加する必要はありません。  
  
system.data.dll アセンブリには、CLR データベース オブジェクトのコンパイルに必要な次の名前空間が含まれています。  
  
- `System.Data`  
- `System.Data.Sql`  
- `Microsoft.SqlServer.Server`  
- `System.Data.SqlTypes`  

> [!TIP]
> Linux での CLR データベースオブジェクトの読み込みはサポートされていますが、.NET Framework を使用してビルドする必要があります (SQL Server CLR 統合では .NET Core はサポートされません)。 また、EXTERNAL_ACCESS または UNSAFE アクセス許可セットを持つ CLR アセンブリは、Linux ではサポートされていません。

## <a name="writing-a-simple-hello-world-stored-procedure"></a>簡単な "Hello World" ストアド プロシージャの作成  

次の Visual C# コードまたは [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic コードをコピーしてテキスト エディターに貼り付け、"helloworld.cs" または "helloworld.vb" というファイル名を付けて保存してください。  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlTypes;  
  
public class HelloWorldProc  
{  
    [Microsoft.SqlServer.Server.SqlProcedure]  
    public static void HelloWorld(out string text)  
    {  
        SqlContext.Pipe.Send("Hello world!" + Environment.NewLine);  
        text = "Hello world!";  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlTypes  
Imports System.Runtime.InteropServices  
  
Public Class HelloWorldProc  
    \<Microsoft.SqlServer.Server.SqlProcedure> _   
    Public Shared  Sub HelloWorld(\<Out()> ByRef text as String)  
        SqlContext.Pipe.Send("Hello world!" & Environment.NewLine)  
        text = "Hello world!"  
    End Sub  
End Class  
  
```  
  
この簡単なプログラムには、パブリック クラスの静的メソッドが 1 つ含まれています。 このメソッドでは、 **[Sqlcontext](/dotnet/api/microsoft.sqlserver.server.sqlcontext)** と **[SqlPipe](/dotnet/api/microsoft.sqlserver.server.sqlpipe)** という2つの新しいクラスを使用して、単純なテキストメッセージを出力するマネージデータベースオブジェクトを作成します。 また、このメソッドは文字列 "Hello world!" を out パラメーターの値として指定します。 このメソッドを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のストアド プロシージャとして宣言すれば、[!INCLUDE[tsql](../../../includes/tsql-md.md)] ストアド プロシージャと同じ方法で実行できます。  
  
このプログラムをライブラリとしてコンパイルし、に読み込んで [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 、ストアドプロシージャとして実行します。  
  
## <a name="compile-the-hello-world-stored-procedure"></a>"Hello World" ストアドプロシージャをコンパイルします。  

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、[!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework の再配布ファイルが既定でインストールされます。 インストールされるファイルには、Visual C# プログラムと Visual Basic プログラム用のコマンド ライン コンパイラである csc.exe と vbc.exe が含まれています。 サンプルをコンパイルする前に、csc.exe または vbc.exe が格納されたディレクトリを指すようにパス変数を変更する必要があります。 .NET Framework の既定のインストール パスは、次のとおりです。  
  
`C:\Windows\Microsoft.NET\Framework\(version)`  
  
version は、インストールされた再配布可能な .NET Framework のバージョン番号を表します。 次に例を示します。  
  
`C:\Windows\Microsoft.NET\Framework\v4.6.1`

.NET Framework ディレクトリをパスに追加した後、次のコマンドを実行してサンプル ストアド プロシージャをアセンブリにコンパイルできます。 **/Target**オプションを使用すると、アセンブリにコンパイルできます。  
  
Visual C# ソース ファイルの場合は、次のコマンドを実行します。  
  
`csc /target:library helloworld.cs`  
  
 Visual Basic ソース ファイルの場合は、次のコマンドを実行します。  
  
`vbc /target:library helloworld.vb`  
  
これらのコマンドでは、/target オプションを使用してライブラリ DLL をビルドすることを指定し、Visual C# コンパイラまたは Visual Basic コンパイラを起動します。  
  
## <a name="loading-and-running-the-hello-world-stored-procedure-in-sql-server"></a>"Hello World" ストアド プロシージャの SQL Server への読み込みと実行  

サンプル プロシージャを正常にコンパイルしたら、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] でそのプロシージャをテストできます。 プロシージャをテストするには、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] を起動し、適切なテスト データベース (AdventureWorks サンプル データベースなど) に接続して新しいクエリを作成します。  
  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、CLR (共通言語ランタイム) コードを実行する機能は、既定ではオフに設定されています。 CLR コードを有効にするには、 **sp_configure** システムストアドプロシージャを使用します。 詳細については、「 [CLR 統合の有効化](../../../relational-databases/clr-integration/clr-integration-enabling.md)」を参照してください。  
  
ストアド プロシージャにアクセスするには、アセンブリを作成する必要があります。 この例では、C:\ ディレクトリに helloworld.dll アセンブリが作成されているものとします。 クエリに次の [!INCLUDE[tsql](../../../includes/tsql-md.md)] ステートメントを追加します。  
  
`CREATE ASSEMBLY helloworld from 'c:\helloworld.dll' WITH PERMISSION_SET = SAFE`  
  
アセンブリを作成した後、次のように CREATE PROCEDURE ステートメントを使用すると、HelloWorld メソッドにアクセスできるようになります。 ここではストアド プロシージャ "hello" を呼び出します。  
  
```sql
CREATE PROCEDURE hello  
@i nchar(25) OUTPUT  
AS  
EXTERNAL NAME helloworld.HelloWorldProc.HelloWorld  
-- if the HelloWorldProc class is inside a namespace (called MyNS),  
-- the last line in the create procedure statement would be  
-- EXTERNAL NAME helloworld.[MyNS.HelloWorldProc].HelloWorld  
```  
  
作成したプロシージャは、[!INCLUDE[tsql](../../../includes/tsql-md.md)] で記述された通常のストアド プロシージャと同様に実行できます。 たとえば、次のコマンドを実行します。  
  
```sql
DECLARE @J nchar(25)  
EXEC hello @J out  
PRINT @J  
```  
  
これにより、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] のメッセージ ウィンドウに次の出力結果が表示されます。  
  
```
Hello world!  
Hello world!  
```  
  
## <a name="removing-the-hello-world-stored-procedure-sample"></a>"Hello World" サンプル ストアド プロシージャの削除  

サンプル ストアド プロシージャの実行を完了したら、テスト データベースからこのプロシージャとアセンブリを削除できます。  
  
最初に、次のように drop procedure コマンドを使用してプロシージャを削除します。  
  
```sql
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'hello')  
   drop procedure hello  
```  
  
プロシージャを削除したら、サンプル コードが含まれたアセンブリを次のように削除できます。  
  
```sql
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'helloworld')  
   drop assembly helloworld  
```  
  
## <a name="next-steps"></a>次のステップ

SQL Server での CLR 統合の詳細については、次の記事を参照してください。

- [CLR ストアド プロシージャ](/dotnet/framework/data/adonet/sql/clr-stored-procedures)
- [ADO.NET に対する SQL Server インプロセス固有の拡張機能](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)
- [CLR データベース オブジェクトのデバッグ](../../../relational-databases/clr-integration/debugging-clr-database-objects.md)
- [CLR 統合のセキュリティ](../../../relational-databases/clr-integration/security/clr-integration-security.md)