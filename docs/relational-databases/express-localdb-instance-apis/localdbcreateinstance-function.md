---
description: LocalDBCreateInstance 関数
title: LocalDBCreateInstance 関数 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
apiname:
- LocalDBCreateInstance
apilocation:
- sqluserinstance.dll
apitype: DLLExport
ms.assetid: 3eebb485-8a53-4a79-82a9-57b8de9f8e84
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e38bd02220fd7ba2d4bf4c5a170b90c6264c7b16
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544072"
---
# <a name="localdbcreateinstance-function"></a>LocalDBCreateInstance 関数
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  新しい SQL Server Express LocalDB インスタンスを作成します。  
  
 **ヘッダーファイル:** sqlncli  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT LocalDBCreateInstance(  
           PCWSTR wszVersion,  
           PCWSTR pInstanceName,   
           DWORD dwFlags   
);  
```  
  
## <a name="parameters"></a>パラメーター  
 *wszVersion*  
 [入力] LocalDB バージョン (11. 0 や 11.0.1094.2 など)。  
  
 *pInstanceName*  
 [入力] 作成する LocalDB インスタンスの名前。  
  
 *dwFlags*  
 [入力] 将来の使用のために予約されています。 現時点では、0 に設定する必要があります。  
  
## <a name="returns"></a>戻り値  
 S_OK  
 関数が正常に実行されました。  
  
 [LOCALDB_ERROR_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-not-installed.md)  
 SQL Server Express LocalDB は、コンピューターにインストールされていません。  
  
 [LOCALDB_ERROR_INVALID_PARAMETER](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-parameter.md)  
 指定した 1 つまたは複数の入力パラメーターが無効です。  
  
 [LOCALDB_ERROR_INVALID_INSTANCE_NAME](../../relational-databases/express-localdb-error-messages/localdb-error-invalid-instance-name.md)  
 指定したインスタンス名は無効です。  
  
 [LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG](../../relational-databases/express-localdb-error-messages/localdb-error-instance-folder-path-too-long.md)  
 インスタンスを格納するパスの長さが MAX_PATH を超過しています。  
  
 [LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION](../../relational-databases/express-localdb-error-messages/localdb-error-instance-exists-with-lower-version.md)  
 指定したインスタンスは既に存在しますが、そのバージョンは要求よりも低いバージョンです。  
  
 [LOCALDB_ERROR_UNKNOWN_VERSION](../../relational-databases/express-localdb-error-messages/localdb-error-unknown-version.md)  
 指定したバージョンは使用できません。  
  
 [LOCALDB_ERROR_VERSION_REQUESTED_NOT_INSTALLED](../../relational-databases/express-localdb-error-messages/localdb-error-version-requested-not-installed.md)  
 指定したパッチ レベルはインストールされていません。  
  
 [LOCALDB_ERROR_CANNOT_CREATE_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-create-instance-folder.md)  
 %userprofile% の下にはフォルダーを作成できません。  
  
 [LOCALDB_ERROR_CANNOT_GET_USER_PROFILE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-get-user-profile-folder.md)  
 ユーザー プロファイル フォルダーを取得できません。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_FOLDER](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-folder.md)  
 インスタンス フォルダーにアクセスできません。  
  
 [LOCALDB_ERROR_CANNOT_ACCESS_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-access-instance-registry.md)  
 インスタンス レジストリにアクセスできません。  
  
 [LOCALDB_ERROR_CANNOT_MODIFY_INSTANCE_REGISTRY](../../relational-databases/express-localdb-error-messages/localdb-error-cannot-modify-instance-registry.md)  
 インスタンス レジストリを変更できません。  
  
 [LOCALDB_ERROR_SQL_SERVER_STARTUP_FAILED](../../relational-databases/express-localdb-error-messages/localdb-error-sql-server-startup-failed.md)  
 SQL Server プロセスが開始されましたが、SQL Server の起動に失敗しました。  
  
 [LOCALDB_ERROR_INSTANCE_CONFIGURATION_CORRUPT](../../relational-databases/express-localdb-error-messages/localdb-error-instance-configuration-corrupt.md)  
 インスタンス構成が破損しています。  
  
 [LOCALDB_ERROR_INTERNAL_ERROR](../../relational-databases/express-localdb-error-messages/localdb-error-internal-error.md)  
 予期しないエラーが発生しました。 詳細をイベント ログで確認してください。  
  
## <a name="remarks"></a>解説  
 指定の名前を持つ完全に機能する LocalDB インスタンスが既にあり、そのバージョンが要求されたバージョン以上である場合、結果は S_OK です。  
  
 既存のインスタンスが破損した場合、以降の **Localdbcreateinstance** API メソッドの呼び出しは失敗します。 破損したインスタンスは、手動で修正するか明示的に削除しないと、再度使用できるようになりません。  
  
 LocalDB API を使用するコードサンプルについては、 [Localdb リファレンスの SQL Server Express](../../relational-databases/sql-server-express-localdb-reference.md)を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server Express LocalDB ヘッダーとバージョン情報](../../relational-databases/express-localdb-instance-apis/sql-server-express-localdb-header-and-version-information.md)  
  
  
