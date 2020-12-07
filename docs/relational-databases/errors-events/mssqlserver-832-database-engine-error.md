---
description: MSSQLSERVER_832
title: MSSQLSERVER_832
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 832 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 846ce27ff8e7d9560a6d4cc691d1523fddd913fa
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418829"
---
# <a name="mssqlserver_832"></a>MSSQLSERVER_832
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|832|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|B_CONSTPAGECHANGED|
|メッセージ テキスト|変更不可のページが変更されています (正しいチェックサム: \<expected value>、実際のチェックサム: \<actual value>、データベース \<dbid>、ファイル \'<filename>'、ページ \<pageno>)。 これは一般的に、メモリの障害、またはハードウェアか OS の破損を示します。|
||

## <a name="explanation"></a>説明

外部要因により、データベース ページの変更に使用される通常の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エンジン コードの外部で、データベース ページが変更されました。  次の条件が考えられます。  

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロセスで実行中のスレッドによりデータベース ページへの不正な書き込みが行われている。 これは、多くの場合、"スクリブラー" と呼ばれます
- データベース ページをバックアップしているメモリが不正に変更されたり、破損したりしているハードウェアまたはオペレーティングシステムの問題。  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってこの動作が検出されると、エラー 832 が発生します。

## <a name="user-action"></a>ユーザー アクション

エラーの原因を調べるには、次のオプションを検討してください。

- 通常のハードウェアまたはシステムのチェックを実行して、メモリ、CPU、またはその他のハードウェア関連の問題が発生しているかどうかを確認する必要があります。 すべてのシステム ドライバー、オペレーティング システムの更新プログラム、およびハードウェアの更新プログラムが確実にシステムに適用されていることを確かめます。 メモリ関連のテストを含む、ハードウェアの製造元の診断を実行することを検討します。
- 拡張ストアド プロシージャ、COM オブジェクト、またはデータベース ページ用に予約されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メモリに誤った変更を加えているおそれがあるその他の DLL など、この問題の原因となった可能性がある "外部" DLL のどれを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に読み込むことができるかを評価します。  

このエラーが発生した場合は、エラーメッセージで \<dbid> によって参照されているデータベースに対して、`DBCC CHECKDB` を実行することをすぐに検討する必要があります。

## <a name="more-information"></a>詳細情報

このエラーは、多くの場合 LazyWriter と呼ばれるバックグラウンド タスクによって検出されます。 (このタスクの "コマンド" は LAZY WRITER として表示されます。) そのため、このエラーはクライアント アプリケーションに返されません。 エラーは、EventID=832 として Windows アプリケーション イベント ログに書き込まれます。  

現在キャッシュ内で変更されていない (つまり "ダーティ" な) ページだけがチェックされます。 メッセージで "変更不可" という用語が使用されているのは、ページはディスクから読み取られてから変更されていないためです。 さらに、ページにチェックサム値があり、チェックサム エラー (メッセージ 824) が発生していないため、ページはディスクから "クリーン" の状態で読み取られました。 ただし、このエラーの発生後、ある時点でページが変更され、誤った変更でディスクに書き込まれたおそれがあります。 このエラーが発生した場合、新しいチェックサムは、ディスクに書き込まれる前のすべての変更に基づいて計算されます。 このため、ページがディスク上で破損していても、その後のディスクからの読み取りによってチェックサム エラーが発生しない場合があります。 このエラーによって参照されているすべてのデータベースで `DBCC CHECKDB` を実行することが重要です。  

ディスクへの書き込み後、この状態にあるページに関するエラーが `DBCC CHECKDB` によって報告されない場合もあります。 これは、誤った変更が、データが一切保持されていない、または重要なページまたは行構造の情報が含まれていないページ上の場所で発生したか、あるいは CHECKDB で検出されないデータに対する変更である可能性があるためです。  

メッセージ 832 の詳細情報については、ホワイトペーパー「[SQL Server 入出力の基礎、第 2 章](https://docs.microsoft.com/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))」でも確認できます。
