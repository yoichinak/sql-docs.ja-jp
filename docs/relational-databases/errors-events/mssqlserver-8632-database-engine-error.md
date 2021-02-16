---
description: MSSQLSERVER_8632
title: MSSQLSERVER_8632
ms.custom: ''
ms.date: 10/27/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 8632 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: b7c59634423bd6df623725720bf8bd0d262d5be0
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100348694"
---
# <a name="mssqlserver_8632"></a>MSSQLSERVER_8632
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|8632|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|QUERY_EXPRESSION_TOO_COMPLEX|
|メッセージ テキスト|内部エラー:Expression Service の制限に達しました。 クエリを確認し、複雑な式がある場合は簡素化してください。|
||

## <a name="explanation"></a>説明

1 つの式に多数の識別子と定数を含む [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でクエリを実行すると、エラー 8632 が発生します。 次のようなエラー メッセージがユーザーに報告されます。

> サーバー: メッセージ 8632、レベル 17、状態 2、行 1  
内部エラー:Expression Service の制限に達しました。 クエリを確認し、複雑な式がある場合は簡素化してください。

## <a name="cause"></a>原因

この問題が発生するのは、1 つのクエリ式に含めることができる識別子と定数の数が [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって制限されるためです。 上限は 65,535 個です。 たとえば、次のクエリには式が 1 つだけ含まれています。

```sql
select a, b + c, d + e
```

この式は、5 つの列をすべて取得し、加算演算子を計算して、3 つの予想される結果をクライアントに送信します。

識別子と定数の数のテストは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって参照されているすべての識別子と定数が展開された後に実行されます。 たとえば、次の項目を展開できます。

- 選択リストのアスタリスク (*)
- ビュー
- 計算列の定義

展開後の数値が制限を超えている場合は、クエリを実行できません。

## <a name="user-action"></a>ユーザー アクション

この問題を回避するには、クエリを書き直してください。 クエリの最大の式で参照する識別子と定数を減らします。 クエリの各式の識別子と定数の数が制限を超えないようにする必要があります。 これを行うには、クエリを複数の単一クエリに分割することが必要になる場合があります。 次に、一時的な中間結果を作成します。
