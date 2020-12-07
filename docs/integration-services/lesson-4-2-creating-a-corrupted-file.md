---
description: レッスン 4-2:破損したファイルを作成する
title: 手順 2:破損ファイルの作成 | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: cd0b18dc-66c3-4d88-86ef-8e40cb660fae
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 81bee95c84aabe02f2964f41849051a7c8c7052a
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88449640"
---
# <a name="lesson-4-2-create-a-corrupted-file"></a>レッスン 4-2:破損したファイルを作成する

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



変換エラーの構成と処理を体験するには、コンポーネントの処理が失敗するサンプル フラット ファイルが必要です。  
  
この実習では、既存のサンプル フラット ファイルのコピーを作成します。 メモ帳でファイルを開き、**CurrencyID** 列を編集し、参照に失敗する正しくない値を入力します。 破損ファイルの処理時、参照が失敗すると Lookup Currency Key 変換は失敗し、それ以降のパッケージも失敗します。 破損しているサンプル ファイルを作成したら、パッケージを実行して、パッケージのエラーを確認します。  
  
## <a name="create-a-corrupted-sample-flat-file"></a>破損しているサンプル フラット ファイルを作成する  
  
1.  メモ帳などのテキスト エディターで **Currency_VEB.txt** ファイルを開きます。  
  
2.  テキスト エディターの検索置換機能を使用し、 **VEB** と表示されているすべての箇所を **BAD** に置換します。  
  
3.  他のサンプル データ ファイルと同じフォルダーに、修正したファイルを保存します。このファイルには「 **Currency_BAD.txt**」という名前を付けてください。  
  
    > [!NOTE]  
    > **Currency_BAD.txt** が他のサンプル データ ファイルと同じフォルダーに保存されていることを確認してください。  
  
4.  テキスト エディターを閉じます。  
  
## <a name="verify-that-an-error-occurs-during-run-time"></a>実行時にエラーが発生することを確認する  
  
1.  **[デバッグ]** メニューの **[デバッグの開始]** をクリックします。  
  
    データ フローの 3 つ目の反復処理で、Lookup Currency Key 変換が **Currency_BAD.txt** ファイルを処理しようとし、変換が失敗します。 この変換エラーにより、パッケージ全体が失敗します。  
  
2.  **[デバッグ]** メニューの **[デバッグの停止]** を選択します。  
  
3.  デザイン画面で、**[実行結果]** タブを選択します。  
  
4.  ログの内容を参照し、次の処理不能エラーが発生していることを確認します。  
  
    ```
    [Lookup Currency Key[27]] Error: Row yielded no match during lookup.
    ```
  
    > [!NOTE]  
    > 数値 27 はコンポーネントの ID です。 この値はデータ フローを構築したときに割り当てられるもので、パッケージの値とは異なることがあります。  
  
## <a name="go-to-next-task"></a>次のタスクに進む  
[ステップ 3:エラー フロー リダイレクションを追加する](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
  
  
