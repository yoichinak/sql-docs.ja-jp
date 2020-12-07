---
title: sqlservr アプリケーション
description: コマンド プロンプトから sqlservr アプリケーションを使用して、SQL Server のインスタンスの起動、停止、一時停止、および続行を行います。
ms.custom: seo-lt-2019
ms.date: 07/22/2020
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server], sqlservr
- command prompt [SQL Server], pausing/resuming instance of SQL Server
- starting instance of SQL Server
- command prompt [SQL Server], continuing instance of SQL Server
- sqlservr utility
- pausing instance of SQL Server
- stopping instance of SQL Server
- resuming SQL Server
- command prompt [SQL Server], stopping instance of SQL Server
- command prompt [SQL Server], starting instance of SQL Server
- continuing instance of SQL Server
ms.assetid: 60e8ef0a-0851-41cf-a6d8-cca1e04cbcdb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 36fde81f6317d45b2169282d99e4eef27b3467b3
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2020
ms.locfileid: "88714270"
---
# <a name="sqlservr-application"></a>sqlservr アプリケーション

[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

コマンド プロンプトから **sqlservr** アプリケーションを使用して、[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスの起動、停止、一時停止、続行を行います。

## <a name="syntax"></a>構文

```cmd
sqlservr [-s instance_name] [-c] [-d master_path] [-f] 
     [-e error_log_path] [-l master_log_path] [-m]
     [-n] [-T trace#] [-v] [-x]
```

## <a name="arguments"></a>引数

**-s** *instance_name*: 接続先の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスを指定します。 名前付きインスタンスを指定しない場合、 **sqlservr** は [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]の既定のインスタンスを起動します。

> [!IMPORTANT]
>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンスを起動する場合、そのインスタンス用の適切なディレクトリで **sqlservr** アプリケーションを使用する必要があります。 既定のインスタンスの場合は、\MSSQL\Binn ディレクトリで **sqlservr** を実行します。 名前付きインスタンスの場合は、\MSSQL$ **instance_name** \Binn ディレクトリで*sqlservr*を実行します。

 **-c**: Windows サービス コントロール マネージャーに依存せずに、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスを起動します。 このオプションは、コマンド プロンプトから [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を起動して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の起動に要する時間を短縮する場合に使用します。

> [!NOTE]
>ただし、このオプションを使用すると、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] サービス マネージャーまたは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] net stop **コマンドを使用して** を停止することはできません。また、コンピューターからログオフすると、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] は停止します。

**-d** *master_path*: **master** データベース ファイルの完全修飾パスを指定します。 **-d** と *master_path*の間には空白を入れません。 このオプションを省略すると、レジストリ内にあるパラメーターが使用されます。

**-f**: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスを最小構成で起動します。 設定値によりサーバーが起動できないとき (たとえば使用できるメモリが不足している場合) などに便利です。

**-e** *error_log_path*: エラー ログ ファイルの完全修飾パスを指定します。 指定していない場合、既定の場所は、既定のインスタンスの場合は `*\<Drive>*:\Program Files\Microsoft SQL Server\MSSQL\Log\Errorlog`、名前付きインスタンスの場合は `*\<Drive>*:\Program Files\Microsoft SQL Server\MSSQL$*instance_name*\Log\Errorlog` になります。 **-e** と *error_log_path*の間には空白を入れません。

**-l** *master_log_path*: **master** データベース トランザクション ログ ファイルの完全修飾パスを指定します。 **-l** と *master_log_path*の間には空白を入れません。

**-m**: シングル ユーザー モードで [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスを起動します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] をシングル ユーザー モードで起動した場合、1 人のユーザーのみ接続できます。 CHECKPOINT メカニズムは起動しません。CHECKPOINT メカニズムとは、完了したトランザクションをディスク キャッシュからデータベース デバイスに正しく書き込むことを保証する機能です。 一般的に、システム データベースを修復する必要がある問題が発生したときに、このオプションを使用します。このオプションによって **sp_configure allow updates** オプションが有効になります。 既定の設定では、 **allow updates** は無効になります。

**-n**: [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の名前付きインスタンスの起動を可能にします。 **-s** パラメーターを設定しない場合、既定のインスタンスが起動します。 **sqlservr.exe**を開始する前に、コマンド プロンプトで、インスタンスの適切な BINN ディレクトリに移動する必要があります。 たとえば、Instance1 がバイナリ用に \mssql$Instance1 を使用する場合、ユーザーは \mssql$Instance1\binn ディレクトリで **sqlservr.exe -s instance1**を起動する必要があります。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] -n **オプションで** のインスタンスを起動する場合は、 **-e** オプションも使用してください。このオプションを指定しないと、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のイベントは記録されません。

**-T** *trace#* : 指定された、有効なトレース フラグ (*trace#* ) を使用して [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスを起動します。 トレース フラグを使用してサーバーが起動すると、標準的な動作とは異なります。 詳細については、「[トレース フラグ &#40;Transact-SQL&#41;](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)」を参照してください。

>[!IMPORTANT]
>トレース フラグを指定するときは、 **-T** を使用してトレース フラグ番号を渡してください。 **では小文字の t (** -t [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]) も入力できますが、 **-t** では、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のサポート エンジニアが必要とする他の内部トレース フラグが設定されます。

**-v**: サーバーのバージョン番号を表示します。

**-x**: CPU 時間とキャッシュ ヒット率統計の管理を禁止します。 パフォーマンスは最大になります。

## <a name="remarks"></a>解説
ほとんどの場合、sqlserver.exe プログラムはトラブルシューティングや主なメンテナンスのみに使用されます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] がコマンド プロンプトから sqlservr.exe で起動された場合、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] はサービスとしては起動しないため、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] net **コマンドを使用して** を停止することはできません。 ユーザーは [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]に接続することができますが、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ツールによってサービスのステータスが表示されるため、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーはサービスが停止されたことを適切に示すことができます。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] もサーバーに接続することができますが、同じようにサービスが停止されたことを示すことができます。

## <a name="compatibility-support"></a>互換性サポート
次のパラメーターは廃止され、[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] でサポートされていません。

|パラメーター | 詳細情報|
|:-----|:-----|
|**-h** | 以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の 32 ビットのインスタンスで、AWE が有効になっている場合に、ホット アド メモリ メタデータ用の仮想メモリ アドレス空間を確保します。 [!INCLUDE[sssql14](../includes/sssql14-md.md)] を介してサポートされています。 詳細については、「 [SQL Server 2016 で提供が中止された機能](../database-engine/discontinued-database-engine-functionality-in-sql-server.md?view=sql-server-ver15)」を参照してください。|
|**-g** | *memory_to_reserve*<br/><br>[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の 32 ビット インスタンスの以前のバージョンに適用されます。 [!INCLUDE[sssql14](../includes/sssql14-md.md)] を介してサポートされています。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] メモリ プール外にある [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロセス内に、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] がメモリ割り当て用の領域として残すメモリの容量を、整数で指定します (メガバイト単位)。 詳細については、[サーバー メモリ構成オプションに関する SQL Server 2014 ドキュメント](/previous-versions/sql/2014/database-engine/configure-windows/server-memory-server-configuration-options?view=sql-server-2014)を参照してください。|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>参照
 [データベース エンジン サービスのスタートアップ オプション](../database-engine/configure-windows/database-engine-service-startup-options.md)