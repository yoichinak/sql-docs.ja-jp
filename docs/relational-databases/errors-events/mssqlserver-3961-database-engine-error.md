---
description: MSSQLSERVER_3961
title: MSSQLSERVER_3961 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3961 (Database Engine error)
ms.assetid: 3bbc6965-6445-400c-940a-2d85b037513f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 837215560e15ff01a84f614ac087ff96930db3cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456138"
---
# <a name="mssqlserver_3961"></a>MSSQLSERVER_3961
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>詳細  
  
| 属性 | 値 |  
| :-------- | :---- |  
|製品名|SQL Server|  
|イベント ID|3961|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|XACT_METADATA_INVALID|  
|メッセージ テキスト|データベース '%.*ls' でスナップショット分離トランザクションが失敗しました。ステートメントからアクセスされるオブジェクトが、このトランザクションの開始後に別の同時トランザクションの DDL ステートメントで変更されました。  メタデータはバージョン管理されないため、この操作は許可されません。 メタデータに対する同時更新は、スナップショット分離と組み合わせると一貫性を損なう結果になる可能性があります。|  
  
## <a name="explanation"></a>説明  
このエラーは、スナップショット分離でメタデータのクエリを実行していて、かつスナップショット分離でアクセスされているメタデータを更新する同時 DDL ステートメントがある場合に発生することがあります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、メタデータのバージョン管理はサポートされません。 このため、スナップショット分離で実行されている明示的なトランザクション内で実行できる DDL 操作には制限があります。 定義によると、暗黙のトランザクションとは、DDL ステートメントについてもスナップショット分離のセマンティクスの実行を可能にする単一ステートメントです。 スナップショット分離下では、BEGIN TRANSACTION ステートメントの後に、ALTER TABLE、CREATE INDEX、CREATE XML INDEX、ALTER INDEX、DROP INDEX、DBCC REINDEX、ALTER PARTITION FUNCTION、ALTER PARTITION SCHEME などの DDL ステートメントを実行することはできません。共通言語ランタイム (CLR) の DDL ステートメントも同様です。 暗黙のトランザクション内でスナップショット分離を使用しているときには、これらのステートメントは許可されます。 定義によると、暗黙のトランザクションとは、DDL ステートメントについてもスナップショット分離のセマンティクスの実行を可能にする単一ステートメントです。  
  
## <a name="user-action"></a>ユーザーの操作  
スナップショット分離レベルをスナップショット以外の分離レベル (メタデータに対してクエリを実行する前の READ COMMITTED など) に変更します。  
  
