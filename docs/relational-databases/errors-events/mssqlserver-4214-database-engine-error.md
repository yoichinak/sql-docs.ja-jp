---
description: MSSQLSERVER_
title: MSSQLSERVER_4214
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 4214 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: b448b97f5f6eeaf403b0c5c218edb8cd7dd7f8ca
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98101870"
---
# <a name="mssqlserver_4214"></a>MSSQLSERVER_4214
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|4214|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|DMPX_NODBBACKUP|
|メッセージ テキスト|現在、データベースのバックアップが存在しないので、BACKUP LOG を実行できません|
||

## <a name="explanation"></a>説明

このエラーは、データベースを完全バックアップする前にトランザクション ログのバックアップを試行すると発生します。 データベースのトランザクション ログをバックアップする前に、データベースの完全バックアップを実行する必要があります。 また、エラー ログに次のメッセージが表示されます。

> \<Datetime> バックアップ    エラー:3041、重大度:16、状態: 1.  
\<Datetime>  バックアップ     BACKUP でコマンド BACKUP LOG \<db_name> を完了できませんでした。 詳細メッセージについては、バックアップ アプリケーション ログを確認してください。

## <a name="user-action"></a>ユーザー アクション

データベースのトランザクション ログをバックアップする前に、データベースの完全バックアップを実行してください。

## <a name="more-information"></a>詳細情報

詳細については、以下を参照してください: 「[SQL Server データベースのバックアップと復元](../backup-restore/back-up-and-restore-of-sql-server-databases.md)」。