---
title: SSMS オプション ページ - クエリ実行
description: SSMS オプション (クエリ実行)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Query_Execution.Sql_Server.General
dev_langs:
- TSQL
author: markingmyname
ms.author: maghan
ms.date: 01/13/2021
ms.openlocfilehash: 29ee1a365031eedae80abcffdb1147053d56f069
ms.sourcegitcommit: 23649428528346930d7d5b8be7da3dcf1a2b3190
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2021
ms.locfileid: "98241773"
---
# <a name="options-query-execution---general"></a>オプション (クエリ実行 - 全般)

このページを使用すると、 Microsoft SQL Server クエリを実行するためのオプションを指定できます。 このダイアログ ボックスにアクセスするには、クエリ エディター ウィンドウ内で右クリックし、 **[クエリ オプション]** を選択するか、上部のメニュー バーから **[ツール] > [オプション] > [クエリ実行]** の順に選択します。

- **SET ROWCOUNT** 既定値の 0 は、SQL Server がすべての結果を受け取るまで待機することを意味します。 SQL Server が指定された行数を取得した後にクエリを停止するように設定するには、0 より大きい値を指定します。 このオプションをオフにして、すべての行が返されるようにするには、SET ROWCOUNT 0 を指定してください。

- **SET TEXTSIZE** 既定値の 2,147,483,647 バイトは、SQL Server が text、ntext、nvarchar(max)、および varchar(max) の各データ フィールドの上限まで、完全なデータ フィールドを提供することを示します。 XML データ型は影響を受けません。 大きな値の結果を制限するには、より小さい数値を指定します。 指定されたサイズよりも大きい列は切り捨てられます。

- **Execution time-out** は、クエリを取り消す前に待機する秒数を指定するために使用します。 値 0 は、待ち時間が無限 (タイムアウトなし) であることを示します。

- **Batch separator** Transact-SQL ステートメントをバッチに分けるために使用する単語を入力します。 既定値は GO です。

- **[既定で、新しいクエリを SQLCMD モードで開始する]** 新しいクエリを SQLCMD モードで開始するには、このチェック ボックスをオンにします。 このチェック ボックスは、[ツール] メニューからダイアログ ボックスを開いたときだけ表示されます。

    このオプションを選択する場合は、次の制限事項に注意してください。

    - データベース エンジン クエリ エディターの IntelliSense が無効になります。

    - クエリ エディターはコマンド ラインから実行できないため、変数などのコマンド ライン パラメーターを渡すことはできません。

    - クエリ エディターはオペレーティング システムのプロンプトに応答できないため、対話型のステートメントを実行しないように注意する必要があります。

- **[既定値にリセット]** このページ上のすべての値を元の既定値にリセットします。