---
description: LocalDBStartInstance 関数
title: LocalDBStartInstance 関数 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBStartInstance
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: cb325f5d-10ee-4a56-ba28-db0074ab3926
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 723f63b2b41b04b76c62f8cb3bc58ae917519b72
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544024"
---
# <a name="localdbstartinstance-function"></a>LocalDBStartInstance 関数
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  指定した名前の SQL Server Express LocalDB インスタンスを起動します。  
  
 **ヘッダーファイル:** sqlncli  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT LocalDBStartInstance(  
           PCWSTR pInstanceName,  
           DWORD dwFlags,   
           LPWSTR wszSqlConnection,   
           LPDWORD lpcchSqlConnection   
);  
```  
  
## <a name="parameters"></a>パラメーター  
 *pInstanceName*  
 [入力] 起動する LocalDB インスタンスの名前。  
  
 *dwFlags*  
 [入力] 将来の使用のために予約されています。 現時点では、0 に設定する必要があります。  
  
 *wszSqlConnection*  
 [出力] LocalDB インスタンスへの接続文字列を格納するバッファー。  
  
 *lpcchSqlConnection*  
 [入力/出力]入力時には、末尾の null を含め、 *wszSqlConnection* バッファーのサイズを文字数で格納します。 出力時に、指定されたバッファーサイズが小さすぎる場合、には、末尾の null を含め、必要なバッファーサイズが文字数で格納されます。  
  
## <a name="returns"></a>戻り値  
 S_OK  
 関数が正常に実行されました。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB は、コンピューターにインストールされていません。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 指定した 1 つまたは複数の入力パラメーターが無効です。  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 指定したインスタンス名は無効です。  
  
 [LOCALDB_ERROR_UNKNOWN_INSTANCE](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-instance.md)  
 インスタンスは存在しません。  
  
 [LOCALDB_ERROR_INSUFFICIENT_BUFFER](../../relational-databases/express-localdb-error-messages/localdb-error-insufficient-buffer.md)  
 指定されたバッファー *wszSqlConnection* が小さすぎます。  
  
 [LOCALDB_ERROR_WAIT_TIMEOUT](../../relational-databases/express-localdb-error-messages/localdb-error-wait-timeout.md)  
 同期ロックを取得しようとしているときにタイムアウトが発生しました。  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../../relational-databases/express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 インスタンスを格納するパスの長さが MAX_PATH を超過しています。  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 ユーザー プロファイル フォルダーを取得できません。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 インスタンス フォルダーにアクセスできません。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 インスタンス レジストリにアクセスできません。  
  
 [LOCALDB_ERROR_CANNOT_MODIFY_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-modify-instance-registry.md)  
 インスタンス レジストリを変更できません。  
  
 [LOCALDB_ERROR_CANNOT_CREATE_SQL_PROCESS](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-create-sql-process.md)  
 SQL Server のプロセスを作成できません。  
  
 [LOCALDB_ERROR_SQL_SERVER_STARTUP_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-sql-server-startup-failed.md)  
 SQL Server プロセスが開始されましたが、SQL Server の起動に失敗しました。  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../../relational-databases/express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 インスタンス構成が破損しました。  
  
 [LOCALDB_ERROR_AUTO_INSTANCE_CREATE_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-auto-instance-create-failed.md)  
 自動インスタンスを作成できません。 エラーの詳細については、Windows アプリケーション イベント ログを参照してください。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 予期しないエラーが発生しました。 詳細をイベント ログで確認してください。  
  
## <a name="details"></a>詳細  
 接続バッファー引数 (*wszSqlConnection*) と接続バッファーサイズ引数 (*lpcchSqlConnection*) はどちらも省略可能です。 次の表は、これらの引数を使用するためのオプションとその結果を示しています。  
  
|バッファー|バッファーサイズ|理由|アクション|  
|------------|-----------------|---------------|------------|  
|NULL|NULL|ユーザーはインスタンスを起動しようとしますが、パイプ名は必要ありません。|インスタンスを起動します (パイプの戻り値と必要なバッファー サイズの戻り値なし)。|  
|NULL|存在|ユーザーが出力バッファー サイズを要求します  (次の呼び出しで、ユーザーはおそらく実際の起動を要求します)。|必要なバッファー サイズを返します (起動とパイプの戻り値なし)。 結果は S_OK です。|  
|存在|NULL|許可されていません。入力に誤りがあります。|返される結果は、LOCALDB_ERROR_INVALID_PARAMETER です。|  
|存在|存在|ユーザーはインスタンスを起動する必要があり、起動後に接続するパイプ名が必要です。|バッファー サイズを確認し、インスタンスを起動し、バッファーにあるパイプ名を返します。 <br />バッファーサイズ引数は、"server =" 文字列の長さを返します。終端の null は含まれません。|  
  
 LocalDB API を使用するコードサンプルについては、 [Localdb リファレンスの SQL Server Express](../../relational-databases/sql-server-express-localdb-reference.md)を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server Express LocalDB ヘッダーとバージョン情報](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
