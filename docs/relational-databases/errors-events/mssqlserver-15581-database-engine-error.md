---
description: MSSQLSERVER_15581
title: MSSQLSERVER_15581
ms.custom: ''
ms.date: 09/03/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha, VenCher
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 15581 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: fd227045a859f81fc6f96ba99cc402032ee00e99
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100343149"
---
# <a name="mssqlserver_15581"></a>MSSQLSERVER_15581
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|15581|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|SEC_NODBMASTERKEYERR|
|メッセージ テキスト|この操作を実行するには、マスター キーをデータベースに作成するか、またはセッション内のマスター キーを開いてください。|
||

## <a name="explanation"></a>説明

エラー 15581 は、透過的なデータ暗号化 (TDE) が有効になっているデータベースを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で復旧できない場合に発生します。 次のようなエラー メッセージが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のエラー ログに記録されます

> 2020-01-14 22:16: 26.47 spid20s エラー: 15581、重大度: 16、状態: 3。  
2020-01-14 22:16:26.47 spid20s この操作を実行するには、マスター キーをデータベースに作成するか、またはセッション内のマスター キーを開いてください。

## <a name="possible-cause"></a>考えられる原因

この問題は、次のコマンドが実行されたときに、master データベース内のデータベース マスター キーのサービス マスター キーの暗号化が削除された場合に発生します。

```sql
Use master
go
alter master key drop encryption by service master key
```

サービス マスター キーは、データベース マスター キーで使われる証明書を暗号化するために使用されます。 TDE が有効なデータベースを使用してみる場合は、master データベース内のデータベース マスター キーへのアクセスが必要になります。 [OPEN MASTER KEY (Transact-SQL)](../../t-sql/statements/open-master-key-transact-sql.md) ステートメントを、マスター キーへのアクセスを必要とする各セッションのパスワードと共に使用して、サービス マスター キーによって暗号化されていないマスター キーを開く必要があります。 このコマンドはシステム セッションでは実行できないため、TDE が有効なデータベースでは復旧を完了できません。

## <a name="user-action"></a>ユーザー アクション

この問題を解決するには、マスター キーの自動暗号化解除を有効にします。 これを行うには、次のコマンドを実行します。

```sql
Use master
go
open master key DECRYPTION BY PASSWORD = 'password'
alter master key add encryption by service master key
```

次のクエリを使用して、サービス マスター キーによるマスター キーの自動暗号化解除が master データベースに対して無効になっているかどうかを判断します。

```sql
select is_master_key_encrypted_by_server from sys.databases where name = 'master'
```

このクエリで値 0 が返された場合、サービス マスター キーによるマスター キーの自動暗号化解除は無効になっています。

## <a name="more-information"></a>説明を見る

場合によっては、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで応答なしと表示されることがあります。 動的管理ビューに対して `sys.dm_exec_requests` クエリを実行すると、DML 操作を行っている `LogWriter` スレッドおよびその他のスレッドが WRITELOG wait_type で無期限に待機していることがわかります。 他のセッションも、ロックを取得しようとしている間に待機している可能性があります。