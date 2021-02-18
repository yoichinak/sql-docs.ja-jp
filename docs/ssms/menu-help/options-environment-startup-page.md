---
title: " SQL Server の [オプション] ページ - [環境] - [スタートアップ]"
description: '[オプション] ([環境] - [スタートアップ] ページ)'
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.date: 11/05/2018
ms.openlocfilehash: a409fc3687adfe00bdbdd091708dbb7b672506a0
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100341073"
---
# <a name="options-environment---startup-page"></a>[オプション] ([環境] - [スタートアップ] ページ)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

**[オプション]** ダイアログ ボックスを使用すると、[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] スタートアップ アクション、全般的なウィンドウ管理オプション、およびその他の全般設定を構成できます。 **[ツール]** メニューの **[オプション]** をクリックし、 **[環境]** フォルダーを展開して **[スタートアップ]** をクリックします。

## <a name="ui-element-list"></a>UI 要素の一覧

**[スタートアップ時]**

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] の起動時に実行されるアクションを選択します。 オプションは次のとおりです。

- **[オブジェクト エクスプローラーを開く]** 。接続を要求してからオブジェクト エクスプローラーを開きます。

- **[新しいクエリ ウィンドウを開く]** 。接続を要求してから SQL クエリ エディターを開きます。

- **[オブジェクト エクスプローラーとクエリ ウィンドウを開く]** 。接続を要求してから、その接続を使用してオブジェクト エクスプローラーおよび SQL クエリ エディターの両方を開きます。

- **[オブジェクト エクスプローラーと利用状況モニターを開く]**

- **[空の環境を開く]** 。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を開きますが、[SQL クエリ エディター] ウィンドウを表示せず、オブジェクト エクスプローラーをサーバーに接続しません。

**[オブジェクト エクスプローラーのシステム オブジェクトを非表示にする]**

このチェック ボックスをオンにすると、システム データベース、システム テーブル、システム ビュー、およびシステム ストアド プロシージャがオブジェクト エクスプローラーのツリー ビューから削除されます。 システム関数およびシステム型は非表示になりません。 このオプションは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにのみ適用され、既にオブジェクト エクスプローラーに接続されているサーバーに影響を与えません。

## <a name="see-also"></a>参照

- [[オプション] ダイアログ ボックスの F1 ヘルプ](options-dialog-boxes-f1-help.md)
- [[オプション] ([環境] - [全般] ページ)](options-environment-general-page.md)
