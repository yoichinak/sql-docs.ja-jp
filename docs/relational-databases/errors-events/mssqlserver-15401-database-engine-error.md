---
description: MSSQLSERVER_15401
title: MSSQLSERVER_15401
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 15401 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: ab9739d17fbe36bb8a703dd06ee85a32e93e7662
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100349031"
---
# <a name="mssqlserver_15401"></a>MSSQLSERVER_15401
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|15401|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|SEC_INVALIDLOGINORGROUP|
|メッセージ テキスト|Windows NT ユーザーまたはグループ '%s' が見つかりませんでした。 名前を再確認してください。|
||

## <a name="explanation"></a>説明

このエラーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって Windows プリンシパル (ドメイン ユーザーや Windows ドメイン グループなど) に基づいてログインが作成されない場合に発生します。 次のようなエラー メッセージがユーザーに報告されます。

> エラー 15401:Windows NT ユーザーまたはグループ '%s' が見つかりませんでした。 名前を再確認してください。

## <a name="cause"></a>原因

このエラーは、次のいずれかが原因で発生することがあります。

- ログインが Active Directory に存在しない。
- ドメイン コントローラーを使用できない。
- ローカル アカウントを追加するときに、ドメイン名として BUILTIN を使用していない。
- 名前解決の問題。

## <a name="user-action"></a>ユーザー アクション

上記のさまざまな原因に対して取ることができるアクションについては、次のセクションを参照してください。

### <a name="verify-the-login-you-are-trying-to-add"></a>追加しようとしているログインを確認する

1. Windows ログインがドメインにまだ存在していることを確認します。 ネットワーク管理者が特定の理由で Windows ログインを削除した可能性があり、ユーザーがそのログイン アクセスを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に許可できないことがあります。
1. ドメインとログイン名のスペルが正しいこと、および使用している形式が `Domain\User` であることを確認します。
1. ログインが存在し、かつそれが正しい場合でもエラーが発生する場合は、この記事の次のセクションに進んでください。

### <a name="verify-if-the-domain-controller-is-available"></a>ドメイン コントローラーを使用できることを確認する

ログインが存在するドメイン (同じドメインまたは別のドメイン) のドメイン コントローラーをなんらかの理由で使用できないときは、エラー 15401 が表示されることがあります。

ログインが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] とは異なるドメインにある場合は、それらのドメイン間に正しい信頼が存在することを確認します。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されているコンピューターから ping コマンドを使用して、そのログインのドメイン コントローラーにアクセスできることを確認します。 IP アドレスとドメイン コントローラーの名前の両方を確認してください。

### <a name="verify-the-domain-name-for-local-accounts"></a>ローカル アカウントのドメイン名を確認する

ローカル (ドメイン以外の) アカウントには、特別な処理が必要です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されているローカル コンピューターからローカル アカウントを追加しようとしている場合は、ドメイン名として BUILTIN を使用していることを確認してください。

### <a name="check-for-name-resolution-issues"></a>名前解決の問題を確認する

ログインまたはグループの追加に関与しているコンピューター名の解決に問題がある場合は、エラー 15401 が表示されることがあります。

名前解決メカニズム (WINS、DNS、HOSTS、LMHOSTS など) が正しく構成されていることを確認してください。

## <a name="see-also"></a>関連項目

- [ローカル コンピューターとそのドメインの間のチャネルをテストする](/powershell/module/microsoft.powershell.management/test-computersecurechannel#example-1--test-a-channel-between-the-local-computer-and-its-domain)
- [LogonSessions v1.4](/sysinternals/downloads/logonsessions)
- [sp_change_users_login (Transact-SQL)](../system-stored-procedures/sp-change-users-login-transact-sql.md)