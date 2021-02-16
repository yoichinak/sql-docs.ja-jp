---
description: MSSQLSERVER_3988
title: MSSQLSERVER_3988
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 3988 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 42e07f7731696e23579650ccbfe8ca3930c69cb9
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100348793"
---
# <a name="mssqlserver_3988"></a>MSSQLSERVER_3988
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|3988|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|XACT_UNSUPPORT_PARALLEL_TRAN2|
|メッセージ テキスト|新しいトランザクションは許可されません。他のスレッドがこのセッションで実行されています。|
||

## <a name="explanation"></a>説明

このエラーは、`XACT_ABORT` セッション設定が **ON** である間に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のリモート インスタンスによってホストされる複数のテーブルを結合する分散クエリを実行すると発生します。 次のようなエラー メッセージがユーザーに報告されます。

> メッセージ 3988、レベル 16、状態 1、行 #  
新しいトランザクションは許可されません。他のスレッドがこのセッションで実行されています。

## <a name="cause"></a>原因

次の条件に該当するとき、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に分散クエリ (DQ) を処理する方法には、いくつかの設計上の制限があります。

- SQL Server によって 1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リモート データ ソースの複数のテーブルが結合される。
- クエリを発行しているセッションが分散トランザクションに登録されていない。

この状況でクエリを実行しようとすると、「**説明**」セクションに記載されている 2 つのエラーのいずれかが発生する可能性があります。

## <a name="user-action"></a>ユーザー アクション

この問題を回避するには、分散クエリを 'begin distributed transaction' ステートメントで囲みます。

```sql
BEGIN DISTRIBUTED TRANSACTION <Distributed Query> COMMIT TRANSACTION
```
