---
description: MSSQLSERVER_6522
title: MSSQLSERVER_6522
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 6522 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: f48534e104139ee7cbd4eb7602fce2a8e51eeb73
ms.sourcegitcommit: d8cdbb719916805037a9167ac4e964abb89c3909
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/20/2021
ms.locfileid: "98597140"
---
# <a name="mssqlserver_6522"></a>MSSQLSERVER_6522
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|6522|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|SQLCLR_UDF_EXEC_FAILED|
|メッセージ テキスト|ユーザー定義ルーチンまたは集計 "%.*ls" の実行中に .NET Framework エラーが発生しました: %ls。|
||

## <a name="explanation"></a>説明

次のシナリオで考えてみましょう。

### <a name="scenario-1"></a>シナリオ 1

Microsoft .NET Framework アセンブリを参照する共通言語ランタイム (CLR) ルーチンを作成します。 .NET Framework アセンブリは [922672](/troubleshoot/sql/database-design/policy-untested-net-framework-assemblies) には記載されていません。 次に、.NET Framework 3.5 または .NET Framework 2.0 ベースの修正プログラムをインストールします。

### <a name="scenario-2"></a>シナリオ 2

アセンブリを作成し、そのアセンブリを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに登録します。 次に、そのアセンブリの別のバージョンをグローバル アセンブリ キャッシュ (GAC) にインストールします。

CLR ルーチンを実行するか、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のいずれかのシナリオのアセンブリを使用すると、次のようなエラー メッセージが表示されます。

> サーバー: メッセージ 6522、レベル 16、状態 2、行 1  
ユーザー定義ルーチンまたは集計 'getsid' の実行中に .NET Framework エラーが発生しました:
>
> System.IO.FileLoadException:ファイルまたはアセンブリ System.DirectoryServices, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a'、またはその依存関係の 1 つが読み込めませんでした。 ホスト ストア内のアセンブリには、GAC 内のアセンブリとは異なるシグネチャがあります。 (HRESULT からの例外:0x80131050)

## <a name="possible-cause"></a>考えられる原因

CLR によってアセンブリが読み込まれると、CLR では同じアセンブリが GAC 内にあることを確認します。 同じアセンブリが GAC 内にある場合、CLR ではこれらのアセンブリのモジュール バージョン ID (MVID) が一致することを確認します。 これらのアセンブリの MVID が一致しない場合は、「[説明](#explanation)」セクションに記載されているエラー メッセージが表示されます。

アセンブリが再コンパイルされると、そのアセンブリの MVID が変わります。 したがって、.NET Framework を更新した場合、.NET Framework アセンブリは再コンパイルされるため、それらのアセンブリの MVID は異なります。 また、独自のアセンブリを更新した場合、そのアセンブリは再コンパイルされます。 したがって、そのアセンブリの MVID も異なります。

## <a name="user-action"></a>ユーザー アクション

### <a name="action-1"></a>Action1

「[説明](#explanation)」セクションのシナリオ 1 を回避するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で .NET Framework アセンブリを手動で更新する必要があります。 これを行うには、`ALTER ASSEMBLY` ステートメントを使用して、次のフォルダーにある .NET Framework アセンブリの新しいバージョンをポイントします。

`%Windir%\Microsoft.NET\Framework\Version`

> [!NOTE]
> **Version** は、インストールまたは更新した .NET Framework のバージョンを表します。

### <a name="action-2"></a>アクション 2

「[説明](#explanation)」セクションのシナリオ 2 を回避するには、`ALTER ASSEMBLY` ステートメントを使用してデータベース内のアセンブリを更新します。

これを行った後にもその問題がある場合は、アセンブリをデータベースから削除し、新しいバージョンのアセンブリをデータベースに登録します。

## <a name="more-information"></a>説明

「[SQL Server CLR でホストされている環境でテストされていない .NET Framework アセンブリのサポート ポリシー](/troubleshoot/sql/database-design/policy-untested-net-framework-assemblies)」に記載されていない .NET Framework アセンブリは使用しないことをお勧めします。 ここには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR でホストされている環境でテスト済みのアセンブリの一覧があります。

### <a name="description-of-clr-routines"></a>CLR ルーチンの説明

CLR ルーチンには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 統合を使用して .NET Framework CLR に実装される次のオブジェクトが含まれます。

- スカラー UDF (ユーザー定義スカラー値関数)
- ユーザー定義 TVF (テーブル値関数)
- UDP (ユーザー定義プロシージャ)
- ユーザー定義トリガー
- ユーザー定義データ型
- ユーザー定義集計

### <a name="assemblies-to-update-after-you-install-the-net-framework-35"></a>.NET Framework 3.5 をインストールした後に更新するアセンブリ

.NET Framework 3.5 をインストールした後は、ALTER ASSEMBLY ステートメントを使用して、次のアセンブリを更新する必要があります。

- Accessibility.dll
- AspNetMMCExt.dll
- Cscompmgd.dll
- IEExecRemote.dll
- IEHost.dll
- IIEHost.dll
- Microsoft.Build.Conversion.dll
- Microsoft.Build.Engine.dll
- Microsoft.Build.Framework.dll
- Microsoft.Build.Tasks.dll 
- Microsoft.Build.Utilities.dll 
- Microsoft.CompactFramework.Build.Tasks.dll 
- Microsoft.JScript.dll 
- Microsoft.VisualBasic.Vsa.dll 
- Microsoft.Vsa.dll 
- Microsoft.Vsa.Vb.CodeDOMProcessor.dll 
- Microsoft_VsaVb.dll 
- Sysglobl.dll 
- System.Configuration.Install.dll 
- System.Design.dll 
- System.DirectoryServices.dll 
- System.DirectoryServices.Protocols.dll 
- System.Drawing.dll 
- System.Drawing.Design.dll 
- System.EnterpriseServices.dll 
- System.Management.dll 
- System.Messaging.dll 
- System.Runtime.Serialization.Formatters.Soap.dll 
- System.ServiceProcess.dll 
- System.Web.dll 
- System.Data.Entity.dll 
- System.Web.RegularExpressions.dll 

これらのアセンブリは、次のフォルダーにあります。

`%Windir%\Microsoft.NET\Framework\v2.0.50727`

### <a name="how-to-preserve-the-data-from-user-defined-data-types-after-you-drop-an-assembly"></a>アセンブリを削除した後にユーザー定義データ型からデータを保持する方法

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で使用されるユーザー定義データ型のアセンブリを削除する場合は、次のいずれかの方法を使用してデータを保持できます。

次のシナリオがあるとします。

- *MyAssembly.dll* という名前のアセンブリを作成します。
- MyAssembly アセンブリは `System.DirectoryServices.dll` アセンブリを参照します。
- *MyDateTime* という名前のユーザー定義データ型があります。
- *MyDateTime* データ型では、*MyAssembly.dll* アセンブリが使用されます。
- *MyTable* という名前のテーブルを作成します。
- *MyTable* テーブルには、*MyDateTime* データ型のデータが含まれています。

#### <a name="method-1-use-the-bcpexe-utility"></a>方法 1:bcp.exe ユーティリティを使用する

1. -n スイッチと共に Bcp.exe ユーティリティを使用して、MyTable テーブルからファイルにデータをコピーします。 たとえば、コマンド プロンプトで次のコマンドを実行します。

    ```console
    bcp MyDatabase.dbo.MyTable out C:\MyFile.bcp -n -SSQLServerName -T
    ```

2. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio で、次の手順を実行します。
   1. MyTable テーブルを削除します。
   2. MyDateTime データ型を削除します。
   3. `System.DirectoryServices.dll` アセンブリを削除します。
   4. MyAssembly アセンブリを削除します。
3. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio で、次の手順を実行します。

   1. `System.DirectoryServices.dll` アセンブリを登録します。
   2. MyAssembly アセンブリを登録します。
   3. MyDateTime データ型を作成します。
   4. MyTable テーブルと同じテーブル構造を持つ新しいテーブルを作成します。
4. -n スイッチと共に Bcp.exe ユーティリティを使用して、ファイルから MyTable テーブルにデータをインポートします。 たとえば、コマンド プロンプトで次のコマンドを実行します。
  
    ```console
    bcp MyDatabase.dbo.MyTable in C:\MyFile.bcp -n -SSQLServerName -T
    ```

#### <a name="method-2-use-the-insert--select-statement"></a>方法 2:INSERT ...SELECT ステートメント

MyDateTime データ型によってストレージで 9 バイトが占有されているとします。

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio で、次のステートメントを実行して、`VARBINARY(9)` データ型の列を含む新しいテーブルを作成します。

    ```sql
    CREATE TABLE TempTable (c1 VARBINARY(9));
    ```

2. 次の INSERT ...SELECT ステートメントを実行して、TempTable テーブルにデータを入力します。

    ```sql
    INSERT INTO TempTable SELECT CAST(c1 as VARBINARY(9)) FROM MyTable;
    ```

3. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio で、次の手順を実行します。
   1. MyTable テーブルを削除します。
   2. MyDateTime データ型を削除します。
   3. System.DirectoryServices.dll アセンブリを削除します。
   4. MyAssembly アセンブリを削除します。
4. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio で、次の手順を実行します。
   1. System.DirectoryServices.dll アセンブリを登録します。
   2. MyAssembly アセンブリを登録します。
   3. MyDateTime データ型を作成します。
   4. MyTable テーブルと同じテーブル構造を持つ新しいテーブルを作成します。
5. 次の INSERT ...SELECT ステートメントを実行して、MyTable テーブルにデータを入力します。

    ```sql
    INSERT INTO MyTable SELECT c1 FROM TempTable;
    ```

## <a name="references"></a>リファレンス

- アセンブリのバージョンの詳細については、「[Visual Studio 2005 の提供終了済みドキュメント](https://www.microsoft.com/download/details.aspx?id=55984)」を参照してください。
- アセンブリを更新する方法の詳細については、「[ALTER ASSEMBLY (Transact-SQL)](../../t-sql/statements/alter-assembly-transact-sql.md)」を参照してください。
- アセンブリを削除する方法の詳細については、「[DROP ASSEMBLY (Transact-SQL)](../../t-sql/statements/drop-assembly-transact-sql.md)」を参照してください。
- アセンブリを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに登録する方法の詳細については、「[CREATE ASSEMBLY (Transact-SQL)](../../t-sql/statements/create-assembly-transact-sql.md)」を参照してください。
- Bcp.exe ユーティリティの詳細については、[https://msdn2.microsoft.com/library/ms162802.aspx](../../tools/bcp-utility.md) を参照してください。