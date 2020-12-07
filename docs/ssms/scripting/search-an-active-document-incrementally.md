---
title: アクティブ ドキュメントのインクリメンタル検索
description: 1 つのドキュメントまたはウィンドウをインクリメンタル検索する方法について説明します。 入力すると、インクリメンタル検索操作によって、その時点までに入力した内容の次の出現箇所が強調表示されます。 非表示のテキストは無視されます。
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- searches [SQL Server Management Studio], incremental
- Query Editor [SQL Server Management Studio], incremental search
- incremental searches [SQL Server Management Studio]
ms.assetid: 490bb36c-dd43-4219-9e2a-ff27046b9395
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6e28ed3ad28a47fba60a703882684a1625523675
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036415"
---
# <a name="search-an-active-document-incrementally"></a>アクティブ ドキュメントのインクリメンタル検索
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  テキストを入力して、1 つのドキュメント内またはウィンドウ内のインクリメンタル検索を実行できます。 検索操作では、ドキュメント内またはウィンドウ内のインクリメンタル検索の対象として入力した文字の最初の一致項目のセットが強調表示されます。 インクリメンタル検索では、ドキュメント内またはウィンドウ内のテキストのうち、非表示になっているテキストが検索対象から自動的に除外されます。  
  
 インクリメンタル検索の場合、 **[大文字と小文字を区別する]** オプションに関しては、直前の検索の基準がそのまま使用されます。 たとえば、 **[フォルダーを指定して検索]** ダイアログ ボックスを使用して複数のファイルの検索を実行したときに **[大文字と小文字を区別する]** をオンにしていれば、次回のインクリメンタル検索でも大文字と小文字が区別されます。  
  
### <a name="to-search-incrementally"></a>インクリメンタル検索を実行するには  
  
1.  検索するファイルまたはウィンドウを開きます。  
  
2.  **[編集]** メニューの **[詳細設定]** をポイントし、 **[インクリメンタル検索]** をクリックします。  
  
     カーソルのアイコンが、検索方向を示す矢印の付いた双眼鏡に変わり、ステータス バーに [インクリメンタル検索] と表示されます。  
  
3.  テキスト文字列の入力を始めます。  
  
     入力しているテキストがステータス バーに表示され、そのテキストの最初の一致項目がエディターで強調表示されます。 入力を続けると、エディターでは次の一致項目に移動して、その項目が強調表示されます。 一致項目がない場合は、ステータス バーに以下のメッセージが表示されます。  
  
    ```  
    Incremental Search: <text> (not found)  
    ```  
  
 インクリメンタル検索は、ドキュメント内の現在の位置を起点として、上から下へ、左から右へと進んでいきます。 キーボード ショートカット キーを使用してインクリメンタル検索を実行することも可能です。  
  
> [!NOTE]  
>  キーボード ショートカット キーの完全な一覧については、「 [SQL Server Management Studio のキーボード ショートカット](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [検索と置換](./search-and-replace.md)   
 [ドキュメントの対話形式の検索](./search-documents-interactively.md)   
 [結果一覧を使用してドキュメントを検索する方法](./search-documents-using-results-lists.md)   
 [ワイルドカードを使用したテキスト検索](./search-text-with-wildcards.md)   
 [正規表現によるテキストの検索](./search-text-with-regular-expressions.md)  
  
