---
title: プログラミング ガイドライン (ODBC ドライバー)
description: macOS と Linux 上での Microsoft ODBC Driver for SQL Server のプログラミング機能は、SQL Server Native Client (ODBC) の ODBC に基づいています。
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: v-makouz
ms.author: v-daenge
ms.openlocfilehash: 6d602db9c189b6e7fce8b767b60204253ccb7f67
ms.sourcegitcommit: 15c7cd187dcff9fc91f2daf0056b12ed3f0403f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2021
ms.locfileid: "102464396"
---
# <a name="programming-guidelines"></a>プログラミング ガイドライン

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

macOS と Linux での [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のプログラミング機能は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ([SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)) の ODBC に基づいています。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client は、Windows Data Access Components の ODBC に基づいています ([ODBC プログラマー リファレンス](../../../odbc/reference/odbc-programmer-s-reference.md))。  

ODBC アプリケーションでは、unixODBC ヘッダー (`sql.h`、`sqlext.h`、`sqltypes.h`、`sqlucode.h`) をインクルードした後に `/usr/local/include/msodbcsql.h` をインクルードすることで、複数のアクティブな結果セット (MARS) やその他の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有の機能を使用できます。 次に、Windows ODBC アプリケーションで使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有の項目に、同じシンボル名を使用します。

## <a name="available-features"></a>利用可能な機能  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC 用 Native Client のドキュメント ([SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)) の次のセクションは、macOS と Linux で ODBC ドライバーを使用する場合に有効です。  

-   [SQL Server との通信 (ODBC)](../../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
-   [接続とクエリのタイムアウトのサポート](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
-   [カーソル](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
-   [日付/時刻の強化 (ODBC)](../../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
-   [クエリの実行 (ODBC)](../../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
-   [エラーとメッセージの処理](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
-   [Kerberos 認証](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
-   [大きな CLR ユーザー定義型 (ODBC)](../../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)  
-   [トランザクションの実行 (ODBC) (分散トランザクションを除く)](../../../relational-databases/native-client/odbc/performing-transactions-in-odbc.md)  
-   [結果の処理 (ODBC)](../../../relational-databases/native-client-odbc-results/processing-results-odbc.md)  
-   [ストアド プロシージャの実行](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)
-   [スパース列のサポート (ODBC)](../../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md)
-   [検証を伴わない暗号化の使用](../../../relational-databases/native-client/features/using-encryption-without-validation.md)
-   [テーブル値パラメーター](../../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)
-   [コマンドおよびデータ API の UTF-8 および UTF-16](../../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)
-   [カタログ関数の使用](../../../relational-databases/native-client/odbc/using-catalog-functions.md)  

## <a name="unsupported-features"></a>サポートされていない機能

macOS および Linux 上のこのリリースの ODBC ドライバーでは、以下の機能が正しく動作することが確認されていません。

-   フェールオーバー クラスターの接続
-   [透過的なネットワーク IP の解決](../using-transparent-network-ip-resolution.md) (ODBC Driver 17 よりも前のバージョン)
-   [高度なドライバー トレース](/archive/blogs/mattn/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers)

macOS と Linux でのこのリリースの ODBC ドライバーでは、次の機能は利用できません。 

-   分散トランザクション (SQL_ATTR_ENLIST_IN_DTC 属性はサポートされていません)  
-   データベース ミラーリング  
-   FILESTREAM  
-   [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) で説明されている ODBC ドライバー パフォーマンスのプロファイリング、および次のパフォーマンス関連接続属性:  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect (バージョン 17.2 より前)
-   SQL_C_INTERVAL_YEAR_TO_MONTH などの C 時間隔型 (「[Data Type Identifiers and Descriptors](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)」(データ型識別子と記述子) を参照)
-   SQLSetConnectAttr 関数の SQL_ATTR_ODBC_CURSORS 属性の SQL_CUR_USE_ODBC 値。

## <a name="character-set-support"></a>文字セットのサポート

ODBC Driver 13 および 13.1 の場合、SQLCHAR データは UTF-8 である必要があります。 その他のエンコードはサポートされません。

ODBC Driver 17 の場合、次のいずれかの文字セット/エンコードの SQLCHAR データがサポートされます。

> [!NOTE]  
> `musl` と `glibc` には `iconv` の違いがあるため、これらのロケールの多くは、Alpine Linux ではサポートされていません。
>
> 詳細については、「[Functional differences from glibc (glibc との機能の違い)](https://wiki.musl-libc.org/functional-differences-from-glibc.html)」を参照してください。

|名前|説明|
|-|-|
|UTF-8|Unicode|
|CP437|MS-DOS ラテン アメリカ|
|CP850|MS-DOS ラテン 1|
|CP874|ラテン/タイ語|
|CP932|日本語、Shift-JIS|
|CP936|簡体中国語、GBK|
|CP949|韓国語、EUC-KR|
|CP950|繁体字中国語、Big5|
|CP1251|キリル文字|
|CP1253|ギリシャ語|
|CP1256|アラビア語|
|CP1257|バルト語|
|CP1258|ベトナム語|
|ISO-8859-1 / CP1252|ラテン-1|
|ISO-8859-2 / CP1250|ラテン-2|
|ISO-8859-3|ラテン-3|
|ISO-8859-4|ラテン-4|
|ISO-8859-5|ラテン/キリル文字|
|ISO-8859-6|ラテン/アラビア語|
|ISO-8859-7|ラテン/ギリシャ語|
|ISO-8859-8 / CP1255|ヘブライ語|
|ISO-8859-9 / CP1254|トルコ語|
|ISO-8859-13|ラテン-7|
|ISO-8859-15|ラテン-9|

接続時に、読み込まれているプロセスの現在のロケールがドライバーによって検出されます。 上記のいずれかのエンコードを使用している場合、ドライバーでは SQLCHAR (ナロー文字) データにそのエンコードが使用されます。それ以外の場合は、既定の UTF-8 が使用されます。 すべてのプロセスは既定で "C" ロケールで開始されます (従ってドライバーは既定で UTF-8 になります)。そのため、アプリケーションが上記のエンコードのいずれかを使用する必要がある場合は、接続前に **setlocale** 関数を使用してロケールを適切に設定する必要があります。そのために、目的のロケールを明示的に指定するか、`setlocale(LC_ALL, "")` などの空の文字列を使用して環境のロケール設定を使用します。

そのため、エンコードが UTF-8 である一般的な Linux または macOS 環境では、ODBC Driver 13 または 13.1 から 17 にアップグレードしても違いはありません。 ただし、`setlocale()` を介して上記の一覧で UTF-8 以外のエンコードを使用するアプリケーションでは、ドライバーとの間でやり取りするデータに UTF-8 ではなくそのエンコードを使用する必要があります。

SQLWCHAR データは UTF 16LE (リトル エンディアン) である必要があります。

入力パラメーターを SQLBindParameter とバインドするときに、SQL_VARCHAR などのナロー文字の SQL 型を指定すると、ドライバーでは、指定されたデータがクライアントのエンコードから既定 (通常はコードページ 1252) の [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] エンコードに変換されます。 出力パラメーターの場合、ドライバーでは、データに関連付けられている照合順序情報に指定されたエンコードからクライアントのエンコードに変換されます。 ただし、データの損失が発生する可能性があります。ターゲット エンコードで表現できないソース エンコードの文字は、疑問符 ('?') に変換されます。

入力パラメーターをバインドするときのこのデータの損失を回避するには、SQL_NVARCHAR などの Unicode SQL 文字型を指定します。 この場合、ドライバーでは、クライアントのエンコードから UTF-16 に変換されます。これですべての Unicode 文字を表現することができます。 さらに、サーバー上の対象となる列またはパラメーターも、Unicode 型 (**nchar**、**nvarchar**、**ntext**)、または元のソース データのすべての文字を表現できる照合順序/エンコード付きの型にする必要があります。 出力パラメーターを指定してデータ損失を回避するには、Unicode SQL 型と、Unicode C 型 (SQL_C_WCHAR) のいずれかを指定します。こうすると、ドライバーからデータが UTF-16 として返されるようになります。または、ナロー C 型を使用し、クライアントのエンコードがソース データのすべての文字を表現できるようにします (これは、UTF-8 であれば常に可能です)。

照合順序とエンコードについて詳しくは、「[照合順序と Unicode のサポート](../../../relational-databases/collations/collation-and-unicode-support.md)」をご覧ください。

Windows と、Linux および macOS 上の iconv ライブラリの一部のバージョンとの間には、エンコード変換の違いがいくつかあります。 コードページ 1255 (ヘブライ語) のテキスト データには、Unicode への変換時に動作が異なる 1 つのコード ポイント (0xCA) があります。 Windows 上では、この文字は 0x05BA の UTF-16 コード ポイントに変換されます。 libiconv のバージョンが 1.15 より前の macOS および Linux 上では、0x00CA に変換されます。 iconv ライブラリが Big5/CP950 の 2003 リビジョン (名称は `BIG5-2003`) をサポートしていない Linux 上では、そのリビジョンで追加された文字が正しく変換されません。 コードページ 932 (日本語、Shift-JIS) では、元のエンコード規格で定義されていない文字のデコード結果も異なります。 たとえば、Windows 上ではバイト 0x80 は U+0080 に変換されますが、Linux および macOS 上では iconv のバージョンによっては U+30FB に変換される場合があります。

ODBC Driver 13 および 13.1 では、UTF-8 マルチバイト文字または UTF-16 サロゲートが SQLPutData バッファー間で分割されている場合、データの破損が発生します。 部分文字エンコーディングで終了していないストリーミング SQLPutData にバッファーを使用します。 この制限は、ODBC Driver 17 で削除されました。

## <a name="openssl"></a><a name="bkmk-openssl"></a>OpenSSL
バージョン 17.4 以降では、ドライバーによって OpenSSL が動的に読み込まれ、別のドライバー ファイルを必要とせずに、バージョン 1.0 または 1.1 のいずれかのシステムで実行できます。 複数バージョンの OpenSSL が存在する場合、ドライバーによって最新のバージョンの読み込みが試行されます。 このドライバーは、現在、OpenSSL 1.0. x と 1.1. x をサポートしています。

> [!NOTE]  
> ドライバー (またはそのコンポーネントのいずれか) を使用するアプリケーションが OpenSSL の異なるバージョンにリンクされているか、異なるバージョンを動的に読み込んでいる場合、競合が発生する可能性があります。 システムに複数バージョンの OpenSSL が存在し、アプリケーションにそれが使用されている場合、アプリケーションとドライバーによって読み込まれたバージョンが不一致にならないように特に注意することを強くお勧めします。エラーによりメモリが破損する可能性があり、必ずしも明白なまたは一貫した方法で示されるとは限らないためです。

## <a name="alpine-linux"></a><a name="bkmk-alpine"></a>Alpine Linux
この記事の執筆時点では、MUSL の既定のスタック サイズは 128K です。これは基本的な ODBC ドライバーの機能には十分ですが、アプリケーションの処理によっては、特に複数のスレッドからドライバーを呼び出す場合は、この制限をたやすく超えます。 Alpine Linux 上で `-Wl,-z,stack-size=<VALUE IN BYTES>` を使用して ODBC アプリケーションをコンパイルし、スタック サイズを大きくすることをお勧めします。 参照の場合、ほとんどの GLIBC システムの既定のスタック サイズは 2 MB です。

## <a name="additional-notes"></a>追加情報  

1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証と **host,port** を使用して、専用管理者接続 (DAC) を作成できます。 Sysadmin ロールのメンバーはまず、DAC ポートを検出する必要があります。 方法については、「[データベース管理者用の診断接続](../../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md#dac-port)」を参照してください。 たとえば、DAC ポートが 33000 である場合、次のように `sqlcmd` でそれに接続することができます。  

    ```
    sqlcmd -U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > DAC 接続では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 認証を使用する必要があります。  
    
2.  UnixODBC ドライバー マネージャーは、すべてのステートメント属性に対し、それらが SQLSetConnectAttr 経由で渡される場合に、「属性またはオプション識別子が無効です」を返します。 Windows で、SQLSetConnectAttr がステートメント属性値を受け取ると、ドライバーは接続ハンドルの子であるすべてのアクティブなステートメントにその値を設定します。  

3.  高度なマルチスレッド アプリケーションでドライバーを使用する場合、unixODBC のハンドル検証がパフォーマンスのボトルネックになる可能性があります。 このようなシナリオでは、`--enable-fastvalidate` オプションを使用して unixODBC をコンパイルすることで、大幅にパフォーマンスを向上させることができます。 ただし、これにより、アプリケーションから無効なハンドルが ODBC API に渡されると、`SQL_INVALID_HANDLE` エラーが返されずにクラッシュする可能性があることに注意してください。

## <a name="see-also"></a>参照  
[よく寄せられる質問](frequently-asked-questions-faq-for-odbc-linux.yml)

[このバージョンのドライバーの既知の問題](known-issues-in-this-version-of-the-driver.md)

[リリース ノート](release-notes-odbc-sql-server-linux-mac.md)
