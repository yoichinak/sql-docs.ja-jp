---
title: Linux および macOS での ODBC ドライバーに関する既知の問題
description: Linux および macOS での Microsoft ODBC Driver for SQL Server に関する既知の問題と、接続に関する問題をトラブルシューティングするための手順について説明します。
ms.date: 09/01/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: af611dcc4ca45ae18d650af6248b0f53ab8bcb0b
ms.sourcegitcommit: 9122251ab8bbd46ea3c699e741d6842c995195fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91847302"
---
# <a name="known-issues-for-the-odbc-driver-on-linux-and-macos"></a>Linux および macOS での ODBC ドライバーに関する既知の問題

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

この記事では、Linux と macOS 上の Microsoft ODBC Driver 13、13.1、17 for SQL Server に関する既知の問題の一覧を示します。 また、接続の問題のトラブルシューティングを行うための手順も記載されています。

## <a name="known-issues"></a>既知の問題

その他の問題は、[SQL Server ドライバーのブログ](https://techcommunity.microsoft.com/t5/SQL-Server/bg-p/SQLServer/label-name/SQLServerDrivers)に投稿されます。  

- システム ライブラリの制限により、Alpine Linux では、サポートされる文字エンコーディングとロケールが少なくなっています。 たとえば、en_US.UTF-8 は使用できません。 詳細については、[「musl libc」の glibc との機能の違いに関するページ](https://wiki.musl-libc.org/functional-differences-from-glibc.html)を参照してください。

- Windows、Linux、および macOS では、私用領域 (PUA) またはエンド ユーザー定義文字 (EUDC) の文字を異なる方法で変換します。 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 内のサーバーで実行される変換では、Windows 変換ライブラリを使用します。 ドライバーでの変換では、Windows、Linux、または macOS 変換ライブラリを使用します。 各ライブラリは、これらの変換を実行するときに異なる結果を生成する可能性があります。 詳細については、「[エンド ユーザーによって定義されており、秘密の使用領域文字](/windows/desktop/Intl/end-user-defined-characters)」を参照してください。

- クライアント エンコードが UTF-8 の場合、ドライバー マネージャーは、UTF-8 から UTF-16 へ常に正しく変換するとは限りません。 現時点では、文字列内の 1 つ以上の文字が有効な UTF-8 文字でない場合、データの破損が発生します。 ASCII 文字は正しくマップされます。 SQLCHAR バージョンの ODBC API (たとえば、SQLDriverConnectA) を呼び出すときに、ドライバー マネージャーはこの変換を試行します。 SQLWCHAR バージョンの ODBC API (たとえば、SQLDriverConnectW) を呼び出す際には、ドライバー マネージャーはこの変換を試行しません。  

- **SQLBindParameter** の *ColumnSize* パラメーターは SQL 型の文字数を示し、*BufferLength* はアプリケーションのバッファー内のバイト数を示します。 ただし、SQL データ型が `varchar(n)` または `char(n)` であり、アプリケーションによってパラメーターが SQL_C_CHAR (C 型)、または SQL_CHAR か SQL_VARCHAR (SQL 型) としてバインドされ、クライアントの文字エンコードが UTF-8 である場合は、*ColumnSize* の値がサーバー上のデータ型のサイズに揃っていても、ドライバーから "文字列データの右側が切り捨てられました" というエラーを受け取る可能性があります。 このエラーは、文字エンコード間の変換によってデータの長さが変更された場合に発生します。 たとえば、正しいアポストロフィ文字 (U+2019) が CP-1252 では半角の 0x92 としてエンコードされたが、UTF-8 では 3 バイトのシーケンス 0xe2 0x80 0x99 としてエンコードされた場合です。

たとえば、エンコードが UTF-8 の場合に、out パラメーターに対して **SQLBindParameter** の *BufferLength* と *ColumnSize* の両方に 1 を指定してから、(CP-1252 を使用して) サーバー上の `char(1)` 列に格納されている前の文字を取得しようとすると、ドライバーはこの文字を 3 バイトの UTF-8 エンコードに変換しようとしますが、結果は 1 バイトのバッファーに収まりません。 逆方向では、クライアントとサーバー上の異なるコード ページ間で変換を行う前に、ドライバーは *ColumnSize* を **SQLBindParameter** の *BufferLength* と比較します。 *ColumnSize* 1 が *BufferLength* (たとえば) 3 より小さいので、ドライバーはエラーを生成します。 このエラーを回避するには、変換後のデータの長さが、指定したバッファーまたは列に適合することを確認します。 `varchar(n)` 型では、*ColumnSize* を 8000 よりも大きくすることはできません。

## <a name="troubleshooting-connection-problems"></a><a id="connectivity"></a>接続の問題のトラブルシューティング  

ODBC ドライバーを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続できない場合、次の情報を使用して問題を特定します。  
  
最も一般的な接続の問題は、2 つの UnixODBC ドライバー マネージャーがインストールされている場合です。 /usr で libodbc\*.so\*を検索します。 複数バージョンのファイルがある場合、複数のドライバー マネージャーがインストールされている可能性があります。 また、アプリケーションに不適切なバージョンが使用される可能性があります。
  
これらの項目と共に次のセクションを含めるよう `/etc/odbcinst.ini` ファイルを編集することで、接続ログを有効にします。

```
[ODBC]
Trace = Yes
TraceFile = (path to log file, or /dev/stdout to output directly to the terminal)
```  
  
別の接続エラーが発生し、ログ ファイルが見つからない場合、コンピューターに 2 つのドライバー マネージャーが存在する可能性があります。 それ以外の場合、ログの出力は次のようになります。  
  
```
[ODBC][28783][1321576347.077780][SQLDriverConnectW.c][290]  
        Entry:  
            Connection = 0x17c858e0  
            Window Hdl = (nil)  
            Str In = [DRIVER={ODBC Driver 17 for SQL Server};SERVER={contoso.com};Trusted_Connection={YES};WSID={mydb.contoso.com};AP...][length = 139 (SQL_NTS)]  
            Str Out = (nil)  
            Str Out Max = 0  
            Str Out Ptr = (nil)  
            Completion = 0  
        UNICODE Using encoding ASCII 'UTF8' and UNICODE 'UTF16LE'  
```  
  
ASCII 文字エンコードが UTF-8 ではない場合の例: 
  
```
UNICODE Using encoding ASCII 'ISO8859-1' and UNICODE 'UCS-2LE'  
```  
  
複数のドライバー マネージャーがインストールされており、アプリケーションが不適切なドライバー マネージャーを使用しているか、またはライバー マネージャーが正しくビルドされていません。  
  
接続エラーの解決の詳細については、以下を参照してください。  

- [SQL の接続問題のトラブルシューティングの手順](/archive/blogs/sql_protocols/steps-to-troubleshoot-sql-connectivity-issues)  
  
- [SQL Server 2005 Connectivity Issue Troubleshoot - Part I (SQL Server 2005 の接続に関する問題のトラブルシューティング - パート 1)](https://techcommunity.microsoft.com/t5/sql-server/sql-server-2005-connectivity-issue-troubleshoot-part-i/ba-p/383034)  
  
- [Connectivity troubleshooting in SQL Server 2008 with the Connectivity Ring Buffer (接続リング バッファーを使用している SQL Server 2008 の接続のトラブルシューティング)](https://techcommunity.microsoft.com/t5/sql-server/connectivity-troubleshooting-in-sql-server-2008-with-the/ba-p/383393)  
  
- [SQL Server Authentication Troubleshooter (SQL Server 認証のトラブルシューティング)](/archive/blogs/sqlsecurity/sql-server-authentication-troubleshooter)  

## <a name="next-steps"></a>次のステップ

ODBC ドライバーのインストール手順については、次の記事を参照してください。

- [Linux に Microsoft ODBC Driver for SQL Server をインストールする](installing-the-microsoft-odbc-driver-for-sql-server.md)
- [macOS に Microsoft ODBC Driver for SQL Server をインストールする](install-microsoft-odbc-driver-sql-server-macos.md)

詳細については、「[プログラミング ガイドライン](programming-guidelines.md)」と[リリースノート](release-notes-odbc-sql-server-linux-mac.md)に関するページを参照してください。
