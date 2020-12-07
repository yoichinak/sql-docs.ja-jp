---
description: MSSQLSERVER_17659
title: MSSQLSERVER_17659
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17659 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 5e4656c437e1b1a19382222107add8392e0c47e4
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418792"
---
# <a name="mssqlserver_17659"></a>MSSQLSERVER_17659
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|17659|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|DEMO_SYSCATUPDATE|
|メッセージ テキスト|システム テーブル ID \% がデータベース ID \% で直接更新されました。キャッシュの一貫性が維持されていないおそれがあります。 <br/> SQL Server を再起動してください。|
||

## <a name="explanation"></a>説明

このエラーは、システム オブジェクトが直接更新されたことを示します。 システム テーブルを手動で更新することはサポートされていません。 システム テーブルは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース エンジンによってのみ更新される必要があります。 ユーザーがシステム テーブルの変更を始めたことが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって検出されると、エラー 17659 が発生します。 このシナリオの場合、イベント ビューアーの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログまたはアプリケーション ログに次のようなイベントが記録されます。

> ログ名:Application  
ソース:MSSQLServer  
イベント ID:17659  
タスク カテゴリ:サーバー  
レベル: Information  
説明: 警告:システム テーブル ID \% がデータベース ID %d で直接更新されました。キャッシュの一貫性が維持されていないおそれがあります。 SQL Server を再起動してください。

## <a name="user-action"></a>ユーザー アクション

この問題を解決するには、次の方法のいずれかを使用します。

- 方法 1  
    データベースのクリーン バックアップがある場合は、バックアップからデータベースを復元します。  
    > [!NOTE]
    > この方法は、バックアップにメタデータの不整合がない場合にのみ機能します。  

- 方法 2  
    バックアップからデータベースを復元できない場合は、データとオブジェクトを新しいデータベースにエクスポートします。 次に、手動で更新されたデータベースの内容を新しいデータベースに転送します。 DBCC CHECKDB コマンドの REPAIR オプションを使用して、システム カタログの不整合を修復することはできないことにご注意ください。 したがって、コマンドでメタデータの破損を修復できないため、推奨される修復レベルは提供されません。

> [!NOTE]
> システム テーブル内のデータは、システム カタログ ビューを使用して表示できます。

## <a name="more-information"></a>詳細情報

詳細については、以下を参照してください: 「[システム ベース テーブル](/sql/relational-databases/system-tables/system-base-tables)」。
