---
description: MSSQLSERVER_5180
title: MSSQLSERVER_5180
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, Masha
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5180 (Database Engine error)
ms.assetid: ''
author: rgward
ms.author: ramakoni
ms.openlocfilehash: cbdc30c1e05d50bb20df3f9e3ebf54097c770743
ms.sourcegitcommit: ead0b8c334d487a07e41256ce5d6acafa2d23c9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2020
ms.locfileid: "92418824"
---
# <a name="mssqlserver_5180"></a>MSSQLSERVER_5180
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>詳細

|属性|値|
|---|---|
|製品名|SQL Server|
|イベント ID|5180|
|イベント ソース|MSSQLSERVER|
|コンポーネント|SQLEngine|
|シンボル名|DSK_BAD_FCB_FILEID|
|メッセージ テキスト|データベース '%.*ls' で無効な ID %d のファイル制御ブロック (FCB) を開けませんでした。 ファイルの場所を確認してください。 DBCC CHECKDB を実行します。|
||

## <a name="explanation"></a>説明

[!INCLUDE[ssDENoVersion](../../includes/ssdenoversion_md.md)]によって無効なファイル ID が参照されると、クエリまたは操作がエラー 5180 で失敗することがあります。 次に例を示します。

> メッセージ 5180、レベル 22、状態 1、行 1  
データベース '%.*ls' で無効な ID %d のファイル制御ブロック (FCB) を開けませんでした。 ファイルの場所を確認してください。 DBCC CHECKDB を実行します。

重大度 22 のエラーが発生するため、ユーザーのセッションは切断されます。 このエラー メッセージは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログと Windows アプリケーション イベント ログに EventID = 5180 で記録されます。

## <a name="possible-causes"></a>考えられる原因

[!INCLUDE[ssDENoVersion](../../includes/ssdenoversion-md.md)]は、さまざまな状況で (ファイル ID はページ ID の最初の部分であるため、ほとんどはページ ID を参照するときに)、ファイル ID を参照します。 何らかの理由で、参照されているファイル ID が 0 未満であるか、データベース内の有効なファイル ID ではない (sys.database_files などのシステム カタログ ビューに示されている有効なファイル ID と比較) 場合は、5180 エラーが発生するおそれがあります。

考えられる原因の 1 つは、格納されているファイル ID が無効であることです。 行内の転送されたレコードは別のページを参照するため、そのページにアクセスしたときにファイル ID が無効である場合は、5180 エラーが発生するおそれがあります。 この状態は、転送されたレコードを含むページでのデータベース破損エラーになります (この例では、`DBCC CHECKDB` によってメッセージ 8993 が報告されます)。

もう 1 つの例としては、次または前のページ ID のページ ヘッダーに格納されている、ページ ID の一部としての無効なファイル ID が挙げられます。 このフィールドは、クラスター化インデックスのなどの一連のページをリンクするために使用されます。 前のページまたは次のページのファイル ID が無効である場合に、次のページまたは前のページに移動するためにエンジンでこの ID を参照する必要があれば、5180 エラーが発生するおそれがあります (この例では、`DBCC CHECKDB` によってメッセージ 8981 が報告されます)。

格納されたページ ID が破損しているためにファイル ID が無効であることが問題の原因でない場合は、[!INCLUDE[ssDENoVersion](../../includes/ssdenoversion-md.md)]内に問題があるおそれがあります。

## <a name="user-action"></a>ユーザー アクション

このエラーが発生した場合は、エラー メッセージに示されているデータベースに対して `DBCC CHECKDB` を実行する必要があります。 エラーが見つかった場合は、正常だとわかっているバックアップから復元する必要があります。 バックアップから復元できない場合は、`DBCC CHECKDB` の出力で推奨されているように、その修復オプションを使用することをお勧めします。 ほとんどの場合、この種類のエラーを修復すると、データが失われます。 データベース破損の問題の対応と原因の詳細については、次の記事を参照してください。「[DBCC CHECKDB によって報告された、データベースの整合性エラーのトラブルシューティング方法](https://support.microsoft.com/kb/2015748)」。

`DBCC CHECKDB` によってエラーが報告されず、問題が引き続き発生する場合は、Microsoft テクニカル サポートにお問い合わせください。 5180 エラーが発生しているクエリを提供できるように準備してください。 エラーが発生したクエリを確認する方法については、「[詳細情報](#more-information)」を参照してください。

## <a name="more-information"></a>詳細情報

ファイル制御ブロック (FCB) は、データベースに関連付けられているファイルに関する重要な情報を追跡する内部メモリ構造です。 ファイル ID は、データベースの FCB を一意に識別するために使用されます。 サーバー エンジンが無効なファイル ID を参照しようとすると、FCB 構造が見つからず、5180 エラー状態がトリガーされます。

このエラーが発生したクエリを確認するには、次の方法を使用します。

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 以降のバージョンについては、system_health セッションにエラーの記録があるかどうかを確認してください。これにはクエリ テキストが含まれます。 system_health セッションの詳細については、資料: 「[SQL Server 2008 のサポート: system_health セッション](https://techcommunity.microsoft.com/t5/sql-server-support/supporting-sql-server-2008-the-system-health-session/ba-p/315509)」を参照してください。
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler を使用して、`SQL:BatchStarting`、`RPC:Starting`、および例外イベントをキャプチャします。 5180 の例外イベントに関連付けられているセッションについて、この例外イベントの前にあるクエリを見つけます。
