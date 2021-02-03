---
description: MSSQLSERVER_3989
title: MSSQLSERVER_3989
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 3989 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: b7932f2e15170ed2601c35c82a2880f390953d4b
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99185168"
---
# <a name="mssqlserver_3989"></a>MSSQLSERVER_3989
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|3989|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|XACT_UNSUPPORT_PARALLEL_TRAN3|
|メッセージ テキスト|新しい要求は、有効なトランザクション記述子を含んでいる必要があるので、この要求を開始できません。|
||

## <a name="explanation"></a>説明

このエラーは、`XACT_ABORT` セッション設定が **ON** である間に、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のリモート インスタンスによってホストされる複数のテーブルを結合する分散クエリを実行すると発生します。 次のようなエラー メッセージがユーザーに報告されます。

> メッセージ 3989、レベル 16、状態 １、行 #  
新しい要求は、有効なトランザクション記述子を含んでいる必要があるので、この要求を開始できません。

## <a name="cause"></a>原因

次の条件に該当するとき、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に分散クエリ (DQ) を処理する方法には、いくつかの設計上の制限があります。

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって 1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リモート データ ソースの複数のテーブルが結合される。
- クエリを発行しているセッションが分散トランザクションに登録されていない。

この状況でクエリを実行しようとすると、「**説明**」セクションに記載されている 2 つのエラーのいずれかが発生する可能性があります。

## <a name="user-action"></a>ユーザー アクション

この問題を回避するには、分散クエリを 'begin distributed transaction' ステートメントで囲みます。

```sql
BEGIN DISTRIBUTED TRANSACTION <Distributed Query> COMMIT TRANSACTION
```
