---
description: MSSQLSERVER_18482
title: MSSQLSERVER_18482
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 18482 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 42e8bf7a80659467c489d86b8a3ca944ceebe360
ms.sourcegitcommit: d819173fb91af6f20ca6ee59686c35c71b060fbc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/28/2020
ms.locfileid: "97797813"
---
# <a name="mssqlserver_18482"></a>MSSQLSERVER_18482
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|18482|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|REMLOGIN_INVALID_SITE|
|メッセージ テキスト|サーバー '%.ls' に接続できませんでした。'%. ls' はリモート サーバーとして定義されていません。 正しいサーバー名を指定していることを確認してください。 %.*ls|
||

## <a name="explanation"></a>説明

このエラーは、あるサーバーから別のサーバーへのリモート プロシージャ コール (RPC) の実行を試行すると (たとえば、`EXEC SERV_REMOTE.pubs..byroyalty` などのステートメントを使用してリモート コンピューター上でストアド プロシージャを実行すると) 発生します。 次のようなエラー メッセージがユーザーに報告されます。

> エラー 18482:サーバー \<SERV_REMOTE> に接続できませんでした。\<SERV_REMOTE> はリモート サーバーとして定義されていません。 正しいサーバー名を指定していることを確認してください。

## <a name="cause"></a>原因

このエラーは、SQL Server でリモート プロシージャ コールを実行できない場合に発生します。 これは、ローカル サーバーが正しく構成されていないことが原因である可能性があります。 リモート プロシージャ コールを行うには、SQL Server では最初に、sysservers で srvid = 0 を使用してサーバー名を探すことで、ローカル サーバーを特定します。 srvid = 0 のエントリが sysservers に見つからない場合、または srvid = 0 のサーバー名がローカルの Windows コンピューター名とは異なるサーバー名に属している場合は、エラーが表示されます。

## <a name="user-action"></a>ユーザー アクション

ローカル サーバーが正しく構成されているかどうかを確認するには、master..sysservers の `srvstatus` 列を調べます。 ローカル サーバーの場合、この値は 0 になります。

たとえば、ローカル サーバーの名前が SERV_LOCAL で、リモート サーバーの名前が *SERV_REMOTE* であり、sysservers に次の情報が含まれているとします。

|srvid|srvstatus|srvname|srvname|
|---|---|---|---|
|1|2|SERV_LOCAL|SERV_LOCAL|
|2|1|SERV_REMOTE|SERV_REMOTE|
||||

上記の出力では、SERV_LOCAL はローカル サーバーですが、srvid は 1 になっています。これは 0 である必要があります。 これを修正するには、次の手順のようにします。

1. `sp_dropserver` local_server_name, droplogins を実行します (この例では、`sp_dropserver SERV_LOCAL, droplogins` を実行します)。
1. `sp_addserver` local_server_name, LOCAL を実行します (この例では、`sp_addserver SERV_LOCAL, LOCAL` を実行します)。
1. SQL Server を停止して再起動します。

これらの手順を実行すると、sysservers テーブルは次のようになります。

|srvid|srvstatus|srvname|srvname|
|---|---|---|---|
|0|0|SERV_LOCAL|SERV_LOCAL|
|2|1|SERV_REMOTE|SERV_REMOTE|
||||

> [!NOTE]
> ローカル サーバーの場合、サーバー ID (srvid) は 0 になります。

sysservers テーブルのエントリが正しく表示される場合もありますが、`select @@servername` を実行すると NULL が返されます。 これらのシナリオでも、上記の手順 1 から 3 を実行して問題を解決する必要があります。

## <a name="more-information"></a>説明

レプリケーションをインストールするときに、レプリケーションに関係するサーバー間でリモート プロシージャ コールが行われるため、このエラー メッセージが表示されることがあります。
