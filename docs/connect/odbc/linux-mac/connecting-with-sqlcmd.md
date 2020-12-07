---
title: sqlcmd による接続
description: Linux と macOS の Microsoft ODBC Driver for SQL Server で sqlcmd ユーティリティを使用する方法について説明します。
ms.custom: ''
ms.date: 06/22/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sqlcmd
ms.assetid: 61a2ec0d-1bcb-4231-bea0-cff866c21463
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d69f1a19e0494b7426eebbac7d8732794f90be8
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91987908"
---
# <a name="connecting-with-sqlcmd"></a>sqlcmd による接続
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[sqlcmd](../../../tools/sqlcmd-utility.md) ユーティリティは、Linux と macOS の [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で使用できます。
  
次のコマンドは、Windows 認証 (Kerberos) と [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証の使用方法をそれぞれ示しています。
  
```console
sqlcmd -E -Sxxx.xxx.xxx.xxx  
sqlcmd -Sxxx.xxx.xxx.xxx -Uxxx -Pxxx  
```  
  
## <a name="available-options"></a>利用可能なオプション

現在のリリースでは、次のオプションを使用できます。  
  
- -? `sqlcmd` の使用状況を表示します。  
  
- -a パケット サイズを要求します。  
  
- -b エラーがある場合にバッチ ジョブを終了します。  
  
- -c *batch_terminator* バッチ ターミネータを指定します。  
  
- -C サーバー証明書を信頼します。  

- -d *database_name*  `sqlcmd` の開始時に `USE` *database_name* ステートメントを発行します。  

- -D `sqlcmd` -S オプションに渡された値が、データ ソース名 (DSN) として解釈されるようにします。 詳細については、このトピックの最後の「`sqlcmd` および `bcp` の DSN サポート」を参照してください。  
  
- -e 入力スクリプトを標準出力デバイス (stdout) に書き込みます。

- -E 信頼関係接続 (統合認証) を使用します。Linux クライアントまたは macOS クライアントからの統合認証を使用する信頼関係接続の作成の詳細については、「[統合認証を使用する](using-integrated-authentication.md)」を参照してください。

- -f codepage | i:codepage[,o:codepage] | o:codepage[,i:codepage] 入力と出力のコード ページを指定します。 コード ページ番号は、インストールされた Linux コード ページを指定する数値です。
(17.5.1.1 以降で利用可能)

- -h *number_of_rows*  列ヘッダーの間に出力する行数を指定します。  
  
- -H ワークステーション名を指定します。  
  
- -i *input_file*[,*input_file*[,...]] SQL ステートメントまたはストアド プロシージャのバッチを含むファイルを指定します。  
  
- -I  `SET QUOTED_IDENTIFIER` 接続オプションを ON に設定します。  
  
- -k  制御文字を削除するか、置き換えます。  
  
- **-K**_application\_intent_  
アプリケーションがサーバーに接続するときのワークロードのタイプを宣言します。 現在サポートされている値は、 **ReadOnly**だけです。 **-K** を指定しない場合、`sqlcmd` では AlwaysOn 可用性グループのセカンダリ レプリカへの接続がサポートされません。 詳細については、[Linux と macOS の ODBC ドライバー - 高可用性とディザスター リカバリー](odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)に関するページをご覧ください。  
  
> [!NOTE]  
> **-K** は、CTP for SUSE Linux ではサポートされていません。 ただし、**に渡される DSN ファイルで**ApplicationIntent=ReadOnly`sqlcmd` キーワードを指定できます。 詳細については、このトピックの最後の「`sqlcmd` および `bcp` の DSN サポート」を参照してください。  
  
- -l *timeout* サーバーへの接続の試行時に、`sqlcmd` のログインがタイムアウトするまでの秒数を指定します。

- -m *error_level* stdout に送信されるエラー メッセージを制御します。  
  
- **-M**_multisubnet\_failover_  
[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 可用性グループまたは [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] フェールオーバー クラスター インスタンスの可用性グループ リスナーに接続する際には、必ず **-M** を指定してください。 **-M** を指定すると、フェールオーバーを迅速に検出して、(現在) アクティブなサーバーに接続できます。 **-M** を指定しない場合、 **-M** は無効になります。 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)] について詳しくは、「[Linux と macOS の ODBC ドライバーでの高可用性とディザスター リカバリーのサポート](odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)」をご覧ください。  
  
> [!NOTE]  
> **-M** は、CTP for SUSE Linux ではサポートされていません。 ただし、`sqlcmd` に渡される DSN ファイルで **MultiSubnetFailover=Yes** キーワードを指定できます。 詳細については、このトピックの最後の「`sqlcmd` および `bcp` の DSN サポート」を参照してください。  
  
- -N 接続を暗号化します。  
  
- -o *output_file*`sqlcmd` からの出力を受信するファイルを指定します。  
  
- -p  すべての結果セットのパフォーマンス統計を出力します。  
  
- -P  ユーザー パスワードを指定します。  
  
- -q *commandline_query*  `sqlcmd` の起動時にクエリを実行しますが、クエリの実行が完了しても終了しません。  

- -Q *commandline_query*  `sqlcmd` の起動時にクエリを実行します。 クエリが終了すると `sqlcmd` は終了します。  

- -r エラー メッセージを stderr にリダイレクトします。

- -R ドライバーがクライアントの地域別設定を使用して、通貨および日時データを文字データへ変換します。 現時点では、en_US (英語 (米国)) 書式設定のみを使用します。
  
- -s *column_separator_char*  列の区切り文字を指定します。  

- -S [*protocol*:] *server*[ **,** _port_]  
接続する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスを指定します。または、-D が使用されている場合、DSN です。 Linux および macOS の ODBC ドライバーには -S が必要です。 **tcp** が唯一の有効なプロトコルであることに注意してください。  
  
- -t *query_timeout* コマンド (または SQL ステートメント) がタイムアウトになるまでの時間を秒数で指定します。  
  
- -u input_file の形式に関係なく、output_file を Unicode 形式で格納するように指定します。  
  
- -U *login_id* ユーザーのログイン ID を指定します。  
  
- -V *error_severity_level* ERRORLEVEL 変数を設定するために使用される重大度レベルを制御します。  
  
- -w *column_width* 出力用の画面幅を指定します。  
  
- -W 列から後続の空白を削除します。  
  
- -x 変数の代入を無効にします。  
  
- -X コマンド、スタートアップ スクリプト、および環境変数を無効にします。  
  
- -y *variable_length_type_display_width* `sqlcmd` スクリプト変数 `SQLCMDMAXFIXEDTYPEWIDTH` を設定します。
  
- -Y *fixed_length_type_display_width* `sqlcmd` スクリプト変数 `SQLCMDMAXVARTYPEWIDTH` を設定します。


## <a name="available-commands"></a>使用可能なコマンド

現在のリリースでは、次のコマンドを使用できます。  
  
-   [:]!!  
  
-   :Connect  
  
-   :Error  
  
-   [:]EXIT  
  
-   GO [*count*]  
  
-   :Help  
  
-   :List  
  
-   :Listvar  
  
-   :On Error  
  
-   :Out  
  
-   :Perftrace  
  
-   [:]QUIT  
  
-   :r  
  
-   :RESET  
  
-   :setvar  
  
## <a name="unavailable-options"></a>利用できないオプション
現在のリリースでは、次のオプションは使用できません。  

- -A  専用管理者接続 (DAC) を使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にログインします。 専用管理者接続 (DAC) を作成する方法については、「[プログラミング ガイドライン](programming-guidelines.md)」を参照してください。  
  
- -L  ローカルに構成されたサーバー コンピューターと、ネットワーク上でブロードキャストしているサーバー コンピューター名の一覧を表示します。  
  
- -v  `sqlcmd` スクリプトで使用できる `sqlcmd` スクリプト変数を作成します。  
  
次の代替方法を使用できます。パラメーターを 1 つのファイル内に配置すると、それを別のファイルに追加することができます。 これにより、パラメーター ファイルを使用して値を置き換えることができます。 たとえば、次のコンテンツを使用して、`a.sql` というファイル (パラメーター ファイル) を作成します。
  
```console
    :setvar ColumnName object_id  
    :setvar TableName sys.objects  
```
  
次に、置換のためのパラメーターを使用して、`b.sql` というファイルを作成します。  
  
```sql
    select $(ColumnName) from $(TableName)  
```

コマンド ラインで、次のコマンドを使用して `a.sql` と `b.sql` を `c.sql` へと結合します。  
  
```console
    cat a.sql > c.sql 
  
    cat b.sql >> c.sql  
```
  
`sqlcmd` を実行し、入力ファイルとして `c.sql` を使用します。  
  
```console
    sqlcmd -S<...> -P<..> -U<..> -I c.sql  
```

- -z *password* パスワードを変更します。  
  
- -Z *password* パスワードを変更して終了します。  

## <a name="unavailable-commands"></a>利用できないコマンド

現在のリリースでは、次のコマンドは利用できません。  
  
-   :ED  
  
-   :ServerList  
  
-   :XML  
  
## <a name="dsn-support-in-sqlcmd-and-bcp"></a>sqlcmd および bcp の DSN サポート

`-D` を指定した場合は、**sqlcmd** または **bcp** `-S` オプション (または **sqlcmd**: 接続コマンド) でサーバー名ではなくデータ ソース名 (DSN) を指定できます。 `-D` を指定すると、**sqlcmd** または **bcp** が、`-S` オプションを使用して DSN で指定されたサーバーに接続されます。  
  
システム DSN は、ODBC SysConfigDir ディレクトリ (標準インストールでは `/etc/odbc.ini`) 内の `odbc.ini` ファイルに格納されます。 ユーザー DSN は、ユーザーのホーム ディレクトリ (`~/.odbc.ini`) 内の `.odbc.ini` に格納されます。

Windows システムでは、システム DNS とユーザー DNS はレジストリに格納され、odbcad32.exe を介して管理されます。 ファイル DSN は、bcp および sqlcmd によるサポートの対象ではありません。

ドライバーがサポートするエントリの一覧については、「[DSN と接続文字列のキーワードと属性](../dsn-connection-string-attribute.md)」を参照してください。

DSN では、DRIVER エントリのみが必要ですが、リモート サーバーに接続するには、`sqlcmd` または `bcp` が SERVER 要素内に値を必要とします。 SERVER 要素が空であるか、DSN に存在しない場合は、`sqlcmd` と `bcp` によって、ローカルシステム上の既定のインスタンスへの接続が試行されます。

Windows システムで bcp を使用する場合、[!INCLUDE [sssql17-md](../../../includes/sssql17-md.md)] 以前では、SQL Native Client 11 ドライバー (sqlncli11.dll) が必要であり、[!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] 以降では、Microsoft ODBC Driver 17 for SQL Server ドライバー (msodbcsql17.dll) が必要です。  

DSN と `sqlcmd` または `bcp` コマンド ラインの両方で同じオプションが指定されている場合は、コマンドライン オプションが、DSN で使用される値をオーバーライドします。 たとえば、DSN に DATABASE エントリがあり、`sqlcmd` コマンドラインに **-d** が含まれる場合、 **-d** に渡される値が使用されます。 DSN で **Trusted_Connection=yes** が指定されている場合は、Kerberos 認証が使用され、ユーザー名 ( **-U**) とパスワード ( **-P**) は無視されます (指定されている場合)。

エイリアス `alias isql="sqlcmd -D"` を定義して、`isql` を呼び出す既存のスクリプトを、`sqlcmd` を使用するように変更できます。  

## <a name="see-also"></a>参照  
[**bcp** による接続](connecting-with-bcp.md)  
[リリース ノート](release-notes-tools.md)
