---
description: MSSQLSERVER_17112
title: MSSQLSERVER_17112
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17112 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 870f9b9f4d3fcc8186ed1d16faee861ed63e4135
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418800"
---
# <a name="mssqlserver_17112"></a>MSSQLSERVER_17112
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|17112|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|INIT_INVCOMMAND|
|メッセージ テキスト|レジストリまたはコマンド プロンプトから、無効なスタートアップ オプションが指定されました。 オプションを修正または削除してください。|
||

## <a name="explanation"></a>説明

このエラーは、無効な[データベース エンジン サービスのスタートアップ オプション](/sql/database-engine/configure-windows/database-engine-service-startup-options)が指定されたことを示しています。 スタートアップ オプションが正しく指定されていない場合、SQL Server が起動に失敗するか、想定どおりに実行されないおそれがあります。 エラー 17112 も発生します。

場合によっては、インスタンスが開始されることもありますが、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログを確認すると、スタートアップ パラメーターが正しくありません。

> \<Datetime> サーバー レジストリのスタートアップ パラメーター:  
\<Datetime> Server -d D:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\DATA\master.mdf  
\<Datetime> Server -e D:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\LOG\ERRORLOG  
\<Datetime> Server -l D:\Program Files\Microsoft SQL Server\MSSQL.1\MSSQL\DATA\mastlog.ldf  
\<Datetime> Server -T1118 -g512

最後の 2 つのスタートアップ パラメーターが同じ行にあることに注目してください。

また、必要なスタートアップ パラメーターを追加しても、サーバーの動作に意図した効果が得られない場合もあります。

## <a name="possible-causes"></a>考えられる原因

これらの問題は、次の理由により発生します。

- スタートアップ パラメーターの有効なリストに存在しないスタートアップ パラメーターを使用している
- 適切な区切り記号 [;] を使用せずにスタートアップ パラメーターを指定している
- 表示されない特殊文字 (-T の前の空白など) を含むテキスト エディターからスタートアップ パラメーターをコピーして貼り付ける
- スタートアップ パラメーターの大文字と小文字を正しく区別していない

## <a name="user-action"></a>ユーザー アクション

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager ツールを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに対して指定されたスタートアップ パラメーターを指定して検証します。 確実に、それぞれのスタートアップ パラメーターが正しく区切られていて、特殊文字が存在しないようにします。

## <a name="more-information"></a>詳細情報

このトピックの詳細については、次のトピックを参照してください。

- [データベース エンジン サービスのスタートアップ オプション](/sql/database-engine/configure-windows/database-engine-service-startup-options)
- [SCM サービス - サーバー起動オプションを構成する](/sql/database-engine/configure-windows/scm-services-configure-server-startup-options)
