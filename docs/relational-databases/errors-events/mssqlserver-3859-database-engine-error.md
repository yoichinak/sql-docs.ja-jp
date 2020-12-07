---
description: MSSQLSERVER_3859
title: MSSQLSERVER_3859
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3859 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 4a3857e9e98bfbe7fcc86ee07272698f0fcac763
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418774"
---
# <a name="mssqlserver_3859"></a>MSSQLSERVER_3859
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|3859|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|DBCC_CHECKCAT_DIRECT_UPDATE|
|メッセージ テキスト|警告:システム カタログがデータベース ID \%d で直接更新されました。最新の更新は %S_DATE で行われました|
||

## <a name="explanation"></a>説明

このエラーは、ユーザーがシステム テーブルの変更を始めたことを示します。 システム テーブルを手動で更新することはサポートされていません。 システム テーブルは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース エンジンによってのみ更新される必要があります。 ユーザーがシステム テーブルの変更を始めたことが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって検出されると、次の 2 つのシナリオでエラー 3859 が発生します。

- シナリオ 1

    手動で更新されたシステム テーブルが含まれる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを開始すると、次のようなイベントが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログまたはイベント ビューアーのアプリケーション ログに記録されます。

    > ログ名:Application  
    ソース:MSSQLSERVER イベント ID: 3859  
    タスク カテゴリ:サーバー  
    レベル: Information  
    説明: 警告:システム カタログがデータベース ID \%d で直接更新されました。最新の更新は **date_time** で行われました  

- シナリオ 2  

    システム テーブルが手動で更新された後に `DBCC_CHECKDB` コマンドを実行すると、次の警告メッセージが返されます。

    > ' **database_name** ' の DBCC 結果。  
    メッセージ 8992、レベル 16、状態 1、行 1  
    カタログ メッセージ 3859 の確認、状態 1: 警告:システム カタログがデータベース ID \%d で直接更新されました。最新の更新は **date_time** で行われました。  
    CHECKDB により、データベース ' **db_name** ' に 0 個のアロケーション エラーと 0 個の一貫性エラーが見つかりました。  
    DBCC の実行が完了しました。 DBCC がエラー メッセージを出力した場合は、システム管理者に相談してください。

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
