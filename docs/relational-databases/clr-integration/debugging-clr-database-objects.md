---
title: 共通言語ランタイム (CLR) データベースオブジェクトのデバッグ
description: SQL Server は、SQL Server デバッガーと Microsoft Visual Studio デバッガーを統合するデータベース内の Transact-sql オブジェクトと CLR オブジェクトのデバッグをサポートします。
ms.date: 10/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: how-to
helpviewer_keywords:
- database objects [CLR integration], debugging
- permissions [CLR integration]
- debugging [CLR integration]
- building database objects [CLR integration], debugging
- common language runtime [SQL Server], debugging
ms.assetid: 1332035c-d6ed-424d-8234-46ad21168319
author: rothja
ms.author: jroth
ms.openlocfilehash: 1be293f98a3b78280b16f80ab7dcfcb656f7e0ec
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196906"
---
# <a name="how-to-debug-clr-database-objects"></a>CLR データベースオブジェクトをデバッグする方法

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、データベース内の [!INCLUDE[tsql](../../includes/tsql-md.md)] オブジェクトと CLR (共通言語ランタイム) オブジェクトのデバッグがサポートされます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でのデバッグの重要な特徴は、セットアップと使用が容易になったことと、SQL Server デバッガーと Microsoft Visual Studio デバッガーが統合されたことです。 さらに、複数の言語にまたがったデバッグを実行できます。 ユーザーは [!INCLUDE[tsql](../../includes/tsql-md.md)] から CLR オブジェクト (またはその逆) にシームレスにステップインできます。 SQL Server Management Studio の Transact-SQL デバッガーを使用してマネージド データベース オブジェクトをデバッグすることはできませんが、Visual Studio のデバッガーを使用すると、このオブジェクトをデバッグすることができます。 Visual Studio でのマネージド データベース オブジェクトのデバッグでは、サーバーで実行するルーチン内の "step into" ステートメントや "step over" ステートメントなど、一般的なデバッグ機能すべてがサポートされます。 デバッグ中は、ブレークポイントの設定、呼び出し履歴の調査、変数の調査、変数値の変更を行うことができます。 

> [!NOTE]
> Visual Studio .NET 2003 は、CLR 統合プログラミングまたはデバッグには使用できません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] には .NET Framework がプレインストールされていますが、Visual Studio .NET 2003 では .NET Framework 2.0 アセンブリを使用できません。  
  
## <a name="debugging-permissions-and-restrictions"></a>デバッグのアクセス許可と制限事項

デバッグは高度な権限を持つ操作であるため、では **sysadmin** 固定サーバーロールのメンバーだけがこの操作を実行でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
デバッグ中には、次の制限事項が適用されます。  
  
- CLR ルーチンを同時にデバッグできるデバッガー インスタンスは 1 つに制限されます。 この制限が適用されるのは、ブレークポイントに到達するとすべての CLR コードの実行が停止し、デバッガーがブレークポイントから先に動作を進めるまで、コードの実行を再開できないことが理由です。 ただし、他の接続での [!INCLUDE[tsql](../../includes/tsql-md.md)] のデバッグは続行できます。 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッグによりサーバーの他の実行が停止することはありませんが、デバッグがロックをかけると、他の接続が待機することになる場合があります。  
  
- デバッグできるのは、既存の接続ではなく新しい接続のみです。これは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が、接続が行われる前のクライアントとデバッガーの環境に関する情報を必要とするためです。  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)] コードと CLR コードのデバッグは、上記の制限事項により、実稼働サーバーではなくテスト サーバーで行うことをお勧めします。  
  
## <a name="overview"></a>概要

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のデバッグは、接続ごとのモデルに準拠します。 デバッガーは、デバッガーがアタッチされているクライアント接続のみに関係したアクティビティを検出してデバッグを実行することができます。 デバッガーの機能は、接続の種類による制限を受けないので、表形式のデータ ストリーム (TDS) 接続と HTTP 接続の両方をデバッグできます。 ただし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、既存の接続をデバッグできません。 デバッグでは、サーバーで実行するルーチン内のすべての一般的なデバッグ機能をサポートします。 デバッガーと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との間のやり取りは、分散 COM (コンポーネント オブジェクト モデル) 経由で行われます。  
  
マネージストアドプロシージャ、関数、トリガー、ユーザー定義型、および集計のデバッグの詳細およびシナリオについては、Visual Studio ドキュメントの「 [SQL SERVER CLR Integration Database デバッグ](/previous-versions/ms165050(v=vs.100)) 」を参照してください。  
  
Visual Studio を使用してリモートで開発およびデバッグを行うには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで TCP/IP ネットワーク プロトコルを有効にする必要があります。 サーバーで TCP/IP プロトコルを有効にする方法の詳細については、「 [クライアントプロトコルを構成する](../../database-engine/configure-windows/configure-client-protocols.md)」を参照してください。  
  
## <a name="debugging-steps"></a>デバッグ手順

Microsoft Visual Studio で CLR データベースオブジェクトをデバッグするには、次の手順に従います。

1. Microsoft Visual Studio を開き、新しい SQL Server プロジェクトを作成します。 Visual Studio に付属している SQL LocalDB インスタンスを使用できます。

2. 新しい SQL CLR 型を作成する (C#):

   1. **ソリューションエクスプローラー**で、プロジェクトを右クリックし、[**追加**]、[**新しい項目**] の順に選択します。 
   1. [ **新しい項目の追加** ] ウィンドウで、[ **Sql Clr c# ストアドプロシージャ**]、[Sql clr **c# User-Defined 関数**]、[ **sql clr C# User-Defined の種類**]、[ **Sql Clr c# トリガー**]、[ **sql clr c# 集計**]、または [ **クラス**] を選択します。
   1. 新しい種類のソースファイルの名前を指定し、[ **追加**] を選択します。

3. テキスト エディターに新しい型のコードを追加します。 ストアドプロシージャの例のサンプルコードについては、この記事の次の例のセクションを参照してください。

4. 型をテストするスクリプトを追加します。 

   1. **ソリューションエクスプローラー**で、プロジェクトノードを右クリックし、[**追加**]、[**スクリプト**] の順に選択します。 
   1. [ **新しい項目の追加** ] ウィンドウで、[ **スクリプト (ビルドではない)**] を選択し、などの名前を指定し `Test.sql` ます。 **[追加]** ボタンを選びます。
   1. **ソリューションエクスプローラー**で、ノードをダブルクリックし `Test.sql` て、既定のテストスクリプトソースファイルを開きます。
   1. テストスクリプト (デバッグ対象のコードを呼び出すコード) をテキストエディターに追加します。 サンプルスクリプトについては、次のセクションの例を参照してください。

5. ソース コードに 1 つ以上のブレークポイントを配置します。 デバッグする関数またはルーチンのテキストエディターで、コード行を右クリックします。 [ **ブレークポイント**]、[ **ブレークポイントの挿入**] を選択します。 ブレークポイントが追加され、コード行が赤で強調表示されます。

6. [ **デバッグ** ] メニューの [ **デバッグ開始** ] をクリックして、プロジェクトをコンパイル、配置、およびテストします。 のテストスクリプト `Test.sql` が実行され、マネージデータベースオブジェクトが呼び出されます。

7. 黄色の矢印 (命令ポインターを指定) がブレークポイントに表示されると、コードの実行は一時停止します。 その後、マネージデータベースオブジェクトをデバッグできます。

   1. [**デバッグ**] メニューの [**ステップオーバー** ] を使用して、命令ポインターを次のコード行に進めます。
   1. [ **ローカル** ] ウィンドウを使用して、命令ポインターで現在強調表示されているオブジェクトの状態を確認します。
   1. **ウォッチ**ウィンドウに変数を追加します。 命令ポインターで現在強調表示されているコード行に変数がない場合でも、デバッグセッション全体で監視対象の変数の状態を確認できます。 
   1. [**デバッグ**] メニューの [**続行**] を選択して、命令ポインターを次のブレークポイントに進めるか、ブレークポイントがなくなった場合はルーチンの実行を完了します。
  
## <a name="example-code"></a>コード例

次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンを呼び出し元に返します。  
  
```csharp
using System.Data.SqlClient;
using Microsoft.SqlServer.Server;

public class StoredProcedures
{
    [Microsoft.SqlServer.Server.SqlProcedure]
    public static void GetVersion()
    {
        using (var connection = new SqlConnection("context connection=true"))
        {
            connection.Open();
            var command = new SqlCommand("select @@version", connection);
            SqlContext.Pipe.ExecuteAndSend(command);
        }
    }
}
```

## <a name="example-test-script"></a>テストスクリプトの例

次のテストスクリプトは、 `GetVersion` 前の例で定義されているストアドプロシージャを呼び出す方法を示しています。  
  
```sql
EXEC GetVersion  
```  

## <a name="next-steps"></a>次のステップ
  
Visual Studio を使用したマネージコードのデバッグの詳細については、Visual Studio ドキュメントの「 [マネージコードのデバッグ](/visualstudio/debugger/debugging-managed-code) 」を参照してください。  

詳細については、「[共通言語ランタイムの統合のプログラミング概念](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)」を参照してください。  
