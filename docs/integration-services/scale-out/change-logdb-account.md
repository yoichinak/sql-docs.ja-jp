---
title: Scale Out ログのアカウントの変更 | Microsoft Docs
description: SQL Server Integration Services (SSIS) Scale Out のログに使用するアカウントを変更する方法について説明します。
ms.custom: performance
ms.date: 06/29/2020
ms.prod: sql
ms.technology: integration-services
ms.topic: conceptual
author: haoqian
ms.author: haoqian
ms.reviewer: maghan
ms.openlocfilehash: b36b01a416a5468def2baa66cd4395b0944a49cd
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100354898"
---
# <a name="change-the-account-for-scale-out-logging"></a>Scale Out ログのアカウントの変更

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


Scale Out で SSIS パッケージを実行すると、イベント メッセージが、 **##MS_SSISLogDBWorkerAgentLogin##** という名前の自動作成ユーザー アカウントで SSISDB データベースにログ記録されます。 このユーザーのログインでは、SQL Server 認証が使用されます。

Scale Out ログ記録で使用されるアカウントを変更する場合は、以下の操作を行います。

> [!NOTE]
> ログ記録に Windows ユーザー アカウントを使用する場合は、Scale Out Worker サービスを実行するアカウントと同じアカウントを使用します。 それ以外の場合は、SQL Server にログインできません。

## <a name="1-create-a-user-for-ssisdb"></a>1.SSISDB のユーザーを作成する
データベース ユーザーの作成手順については、「[データベース ユーザーの作成](../../relational-databases/security/authentication-access/create-a-database-user.md)」を参照してください。

## <a name="2-add-the-user-to-the-database-role-ssis_cluster_worker"></a>2.データベース ロール ssis_cluster_worker にユーザーを追加する

データベース ロールの追加手順については、「[ロールの追加](../../relational-databases/security/authentication-access/join-a-role.md)」を参照してください。

## <a name="3-update-the-logging-information-in-ssisdb"></a>3.SSISDB のログイン情報を更新する
以下の例に示すように、パラメーターとして SQL Server 名と接続文字列を指定してストアド プロシージャ `[catalog].[update_logdb_info]` を呼び出します。

```sql
SET @serverName = CONVERT(sysname, SERVERPROPERTY('servername'))
SET @connectionString = 'Data Source=' + @serverName + ';Initial Catalog=SSISDB;Integrated Security=SSPI;'
EXEC [internal].[update_logdb_info] @serverName, @connectionString
GO
```

## <a name="4-restart-the-scale-out-worker-service"></a>4.Scale Out Worker サービスを再起動する
Scale Out Worker サービスを再起動して、変更を有効にします。

## <a name="next-steps"></a>次のステップ
-   [Integration Services Scale Out Manager](integration-services-ssis-scale-out-manager.md)
