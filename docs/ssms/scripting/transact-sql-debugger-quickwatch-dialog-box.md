---
title: '[クイック ウォッチ] ダイアログ ボックス'
description: コードのデバッグ時に [クイック ウォッチ] ダイアログ ボックスを使用して、変数など、1 つの Transact-SQL 式のデータ型や値をすばやく表示する方法について説明します。
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vs.debug.quickwatch
helpviewer_keywords:
- QuickWatch Dialog [Transact-SQL]
ms.assetid: d6bbb373-1452-41f2-bdc5-86ae689c3dc0
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 54e2bb30bb2527d8b932b64b037a5809587173b4
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036121"
---
# <a name="transact-sql-debugger---quickwatch-dialog-box"></a>Transact-SQL デバッガー - [クイック ウォッチ] ダイアログ ボックス

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

**コードのデバッグ時に** [クイック ウォッチ] [!INCLUDE[tsql](../../includes/tsql-md.md)] ダイアログ ボックスを使用すると、変数やパラメーターなど、1 つの [!INCLUDE[tsql](../../includes/tsql-md.md)] 式のデータ型や値をすばやく表示できます。 複数の式を確認するために、 **[ウォッチ]** ウィンドウに式を追加することもできます。  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="task-list"></a>タスク一覧

 **[クイック ウォッチ] ダイアログ ボックスにアクセスするには**  
  
-   **[デバッグ]** メニューの **[クイック ウォッチ]** をクリックします。  
  
 **式に関する情報を表示するには**  
  
1.  **[式]** ボックスで、目的の式を入力または選択します。 次の [!INCLUDE[tsql](../../includes/tsql-md.md)] 式がサポートされています。  
  
    -   変数。  
  
    -   パラメーター。  
  
    -   名前が @@ で始まるシステム関数。  
  
    -   1 つまたは複数の変数、パラメーター、またはシステム関数に演算子を適用して作成された式 (@IntegerCounter + 1、FirstName + LastName など)。  
  
    -   単一の値を返す Transact-SQL ステートメント(SELECT CharacterCol FROM MyTable WHERE PrimaryKey = 1 など)。  
  
2.  **[再評価]** をクリックします。  
  
 **[ウォッチ] ウィンドウにクイック ウォッチの式を追加するには**  
  
-   **[ウォッチ式の追加]** をクリックします。  
  
 **クイック ウォッチの式の値を変更するには**  
  
-   式を右クリックし、 **[値の編集]** を選択します。  
  
## <a name="options"></a>Options  
 **[式の一覧]**  
 現在選択されている式を表示します。 このドロップダウン リストには、選択して表示できる式のセットが含まれています。 一覧の式は、 **[呼び出し履歴]** ウィンドウで現在選択されているスタック フレームのスコープで使用できる式です。 別の式を表示するには、式を入力するか、一覧から式を選択します。 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーでは、変数、パラメーター、および名前が @@ で始まるシステム関数の式がサポートされます。  
  
 **[値グリッド]**  
 現在監視されている式のプロパティを表示します。  
  
 **名前**  
 監視対象の [!INCLUDE[tsql](../../includes/tsql-md.md)] 式です。  
  
 **Value**  
 式に現在割り当てられている値を表示します。 式に現在値がない場合は、空白になります。  
  
 式の長さが **[値]** 列の幅よりも長い場合は、その式の **[値]** セルにポインターを移動するとツールヒントに完全な値が表示されます。  
  
 **[値]** セルの虫眼鏡アイコンは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガー ビジュアライザーが使用可能であることを示します。 一覧では、 **[テキスト ビジュアライザー]** 、 **[XML ビジュアライザー]** 、または **[HTML ビジュアライザー]** を指定できます。 デバッガー ビジュアライザーを開始するには、虫眼鏡アイコンをクリックします。 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーによりダイアログ ボックスが開き、データがそのデータ型に適した形式で表示されます。  
  
 **Type**  
 式のデータ型を表示します。  
  
## <a name="see-also"></a>参照  
 [Transact-SQL デバッガー](./transact-sql-debugger.md)   
 [Transact-SQL デバッガー情報](./transact-sql-debugger-information.md)   
 [[ウォッチ] ウィンドウ](./transact-sql-debugger-watch-window.md)   
 [[ローカル] ウィンドウ](./transact-sql-debugger-locals-window.md)   
 [[呼び出し履歴] ウィンドウ](./transact-sql-debugger-call-stack-window.md)   
 [式 &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)  
  
