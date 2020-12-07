---
title: コード内とテキスト内の移動
description: さまざまな手法 (場所のブックマークを設定して、その場所に簡単に戻る、インクリメンタル検索を行う、マウスとキーボードを使用する、[ジャンプ] コマンドを使用して、行番号を指定してその行にジャンプする) でドキュメント内を移動する方法について説明します。
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- searches [SQL Server Management Studio], incremental
- mouse [SQL Server Management Studio]
- bookmarks [SQL Server Management Studio]
- Query Editor [SQL Server Management Studio], navigating code
- Query Editor [SQL Server Management Studio], Go To Command
- incremental searches [SQL Server Management Studio]
- Query Editor [SQL Server Management Studio], bookmarks
- Query Editor [SQL Server Management Studio], mouse
- navigating code
- Go To command
ms.assetid: f63247ff-9751-4e99-8ee3-0772ad4009d0
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 69892b05d5e9d34784a06551b929fe9664e2ca4b
ms.sourcegitcommit: 9e1f1c6ee8f5a10d18a2599bfd9f3eb6081829e1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2020
ms.locfileid: "89093494"
---
# <a name="navigate-code-and-text"></a>コード内とテキスト内の移動

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

以下の方法で、テキスト内を移動することができます。  
  
-   ブックマーク  
  
-   インクリメンタル検索  
  
-   マウスと方向キー  
  
-   **[ジャンプ]** コマンド  
  
> [!NOTE]  
>  キーボード ショートカット キーの完全な一覧については、「 [SQL Server Management Studio のキーボード ショートカット](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)」を参照してください。  
  
## <a name="navigating-with-bookmarks"></a>ブックマークを使用した移動  
 ドキュメントの任意の箇所を編集した後に、元の位置に戻れるようにするには、ブックマークを追加します。 ブックマークの設定と、ブックマークへの移動には、キーボード ショートカットを使用できます。 ブックマーク ウィンドウでブックマークを表示できます。  
  
## <a name="incremental-search"></a>インクリメンタル検索  
 インクリメンタル検索では、検索文字を入力すると、現在のドキュメント内の該当する場所に直接移動できます。 インクリメンタル検索の実行には、キーボード ショートカットを使用できます。  
  
## <a name="navigating-with-the-mouse-and-keyboard"></a>マウスとキーボードによる移動  
 テキスト内を移動するには、マウスと方向キーを使用するのが最も一般的な方法です。  
  
-   1 文字ずつ移動する場合は、右方向キーと左方向キーを使用します。1 単語ずつ移動する場合は、Ctrl キーを押しながら方向キーを押します。 1 行ずつ移動する場合は、上方向キーと下方向キーを使用します。  
  
-   カーソルを置く場所でクリックします。  
  
-   スクロール バーまたはマウス ホイールを使用して、テキスト内を移動します。  
  
-   Home キー、End キー、PageUp キー、および PageDown キーを使用して、テキスト内を移動します。  
  
-   Ctrl キーを押しながら PageUp キーを押すとウィンドウの先頭に、Ctrl キーを押しながら PageDown キーを押すとウィンドウの最後に、カーソルが移動します。  
  
-   Ctrl キーを押しながら上方向キーまたは下方向キーを押すと、カーソルの位置を変えずにテキストをスクロールできます。  
  
## <a name="go-to-command"></a>[ジャンプ] コマンド  
 **[ｼﾞｬンプ]** コマンドを使用して、特定の行番号にジャンプできます。 行番号を表示するには、 **[オプション]** ダイアログ ボックスで、 **[テキスト エディター]** 、 **[すべての言語]** 、 **[全般]** の順にクリックし、 **[行番号]** チェック ボックスをオンにします。  
  
 **特定の行番号にジャンプするには**  
  
1.  **[編集]** メニューの **[ジャンプ]** をクリックします。  
  
2.  表示する行番号を入力します。