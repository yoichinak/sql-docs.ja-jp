---
title: 修正されたバグの一覧
description: このページには Microsoft ODBC Driver 17 for SQL Server 以降の各リリースで修正されたバグの一覧が記載されています。
ms.custom: ''
ms.date: 04/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: v-chojas
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: fb686e3c70723cf847853ad558f47cf37da23972
ms.sourcegitcommit: bc10ec0be5ddfc5f0bc220a9ac36c77dd6b80f1d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87544305"
---
# <a name="list-of-bugs-fixed"></a>修正されたバグの一覧

このページには [!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 以降の各リリースで修正されたバグの一覧が記載されています。

### <a name="bug-fixes-in-the-msconame-odbc-driver-176-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.6 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバグを修正しました

- フェデレーション アカウントで認証するときの ADAL エラーを修正しました (Windows)
- 非同期通知操作中にタイムアウトが発生するとき、ドライバーが応答しなくなる問題を修正しました
- Alpine Linux のアップグレード時のドライバー参照カウントを修正しました
- Ubuntu の libc6 依存関係バージョンを修正しました
- Linux/Mac msodbcsql.h に足りない定義を追加しました

### <a name="bug-fixes-in-the-msconame-odbc-driver-17522-for-ssnoversion-alpine-linux-only"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.5.2.2 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバグ修正 (Alpine Linux のみ)

- Alpine Linux 上で、セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するとクラッシュする問題を修正しました

### <a name="bug-fixes-in-the-msconame-odbc-driver-1752-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.5.2 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバグ修正

- Alpine Linux パッケージに msodbcsql.h を追加しました

### <a name="bug-fixes-in-the-msconame-odbc-driver-175-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.5 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバグ修正

- Linux または macOS 上で AKV CMK メタデータ ハッシュの計算を修正しました
- OpenSSL 1.0.0 の読み込み時のエラーを修正しました
- ISO-8859-1 および ISO-8859-2 のコードページを使用するときの変換の問題を修正しました
- バージョン番号を含めるように macOS 上の内部ライブラリ名を修正しました
- 個別の長さとインジケーターのバインドが使用されている場合の null インジケーターの設定を修正しました

### <a name="bug-fixes-in-the-msconame-odbc-driver-1742-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.4.2 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバグ修正

 - プロセス ID とアプリケーション名が SQL Server に正しく送信されない問題を修正しました (sys.dm_exec_sessions 分析の場合) (Linux)
 - libuuid の冗長な依存関係が削除されました (Linux)
 - SQL Server 2019 に UTF8 データを送信する際のバグを修正しました
 - 末尾が "@euro" のロケールが正しく検出されなかったバグを修正しました (Linux)
 - XML データが、Always Encrypted の使用時に出力パラメーターとしてフェッチされる場合に誤って返される問題を修正しました

### <a name="bug-fixes-in-the-msconame-odbc-driver-174-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.4 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバグ修正

- ドライバーが応答を停止し、複数のアクティブな結果セット (MARS) が有効となっている場合の断続的な問題を修正しました
- ドライバーが応答を停止し、非同期通知が有効となっている場合の接続の回復性の問題を修正しました
- マルチスレッド接続試行の診断レコードを取得するときのクラッシュを修正しました
- SQL_USER_NAME および SQL_DATA_SOURCE_READ_ONLY を使用して SQLGetInfo() を呼び出した後、再接続時に発生する 'サポートされない暗号化' を修正しました
- Azure Active Directory 対話型認証の実行中の COM 初期化エラーを修正しました
- 複数バイトの UTF8 データの SQLGetData() を修正しました
- SQLGetData() を使用して sql_variant 列の長さの取得に関する問題を修正しました
- bcp を使用して、7992 バイトを超える sql_variant 列のインポートを修正しました
- 半角文字データの正しいエンコードをサーバーに送信する際の問題を修正しました

### <a name="bug-fixes-in-the-msconame-odbc-driver-173-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.3 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバグ修正

- TCP 送信通知イベント ハンドルのメモリ リークを修正しました。
- msodbcsql.h ヘッダー ファイルの enum _SQL_FILESTREAM_DESIRED_ACCESS の再定義の問題を修正しました
- Linux 用の msodbcsql.h ヘッダー ファイルに存在しない ACCESS_TOKEN および AUTHENTICATION 関連の定義を修正しました

### <a name="bug-fixes-in-the-msconame-odbc-driver-172-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.2 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバグ修正

- Azure Active Directory 認証に関するエラー メッセージを修正しました
- ロケール環境変数の設定が異なる場合のエンコード検出を修正しました
- 接続の回復が進行中に発生する切断時のクラッシュを修正しました
- 接続の活性の検出を修正しました
- 閉じたソケットの誤った検出を修正しました
- 回復に失敗したときにステートメント ハンドルを解放しようとしたときに待機が無限になる問題を修正しました
- Windows にバージョン 13 と 17 の両方のバージョンがインストールされている場合の正しくないアンインストール動作を修正しました
- 以前の Windows プラットフォーム (Windows 7、8、および Server 2012) での復号化動作を修正しました
- Windows 上で ADAL 認証を使用するときのキャッシュの問題を修正しました
- Windows 上のトレース ログがロックされ、上書きされていた問題を修正しました

### <a name="bug-fixes-in-the-msconame-odbc-driver-171-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバグ修正

- MARS を有効にして接続属性 "Encrypt = yes" を指定して SQLFreeHandle を呼び出すときの 1 秒の遅延を修正しました
- 渡されたバッファーのサイズが取得中のデータよりも小さい場合の SQLGetData のエラー 22003 クラッシュを修正しました (Windows)
- 切り詰められた ADAL エラー メッセージを修正しました
- 浮動小数点数を整数に変換するときに、32 ビット版 Windows でまれに発生するバグを修正しました
- Always Encrypted がオンの状態で 10 進数フィールドに double を挿入すると、データ切り捨てエラーが返される問題を修正しました
- macOS インストーラーの警告を修正しました
- 接続の回復性と接続プールの両方が有効な場合、セッション回復の試行中に SQL Server に誤った状態が送信され、サーバーによってセッションがドロップされる原因となっていた問題を修正しました

### <a name="bug-fixes-in-the-msconame-odbc-driver-17-for-ssnoversion"></a>[!INCLUDE[msCoName](../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバグ修正

- Kerberos 認証を使用すると、一括挿入が "アクセスが拒否されました" エラーで失敗するバグを修正しました
- 2\.3.1 より前のバージョンに存在する unixODBC のバグ (ドライバーから unixODBC に渡される特定のバッファーのサイズは 2 倍になっていました) の回避策を削除しました
- ColumnEncryption=enabled を使用する場合に応答が停止する接続の回復性 (再接続) を修正しました
- [Active Directory 対話型認証] オプションを使用すると、Azure 認証ウィンドウが応答しなくなる DSN 作成のバグを修正しました (Windows)
- 非同期実行が有効な場合に ODBC シャットダウン時にまれに発生するクラッシュを修正しました (接続ハンドルをクリアするときに発生しました)
- 長いストアド プロシージャの実行中に SQL ドライバーの CPU 使用率が高くなる問題を修正しました
- 暗号化された varbinary(max) 列のデータを変換なしで取得できない問題を修正しました
- 静的カーソルに対して SQLGetData() を使用して暗号化された null varchar(max) 列がフェッチされた後、データがある場合でも次の列も null になる問題を修正しました
- Always Encrypted をオンにして varbinary (max) フィールドをフェッチする際の問題を修正しました
- setlocale() を Always Encrypted と併用できない問題を修正しました
- Always Encrypted をオンにして XML 型のストアド プロシージャ パラメーターに対して呼び出したときに、SQLDescribeParam() からエラーが返される問題を修正しました
- SQLTables で動作しないエスケープされたアンダースコアを修正しました
- Linux 上で全角文字として返されるときにヘブライ語データ (varchar) が切り詰められるバグを修正しました
- UTF-8 アプリケーションからの Shift-JIS でエンコードされた char/varchar のクエリに関する問題を修正しました
- macOS 上で SQL_DRIVER_NAME パラメーターを指定して SQLGetInfo を呼び出すと、Linux スタイルのファイル名が返されるバグを修正しました
- BCP ユーティリティを使用して 32k バイトを超える入力ファイルを VARCHAR 列に使用して Windows-1252 文字データを読み込むとエラーが発生する問題を修正しました
