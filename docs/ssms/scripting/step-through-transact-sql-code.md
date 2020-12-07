---
title: Transact-SQL コードのステップ実行
description: Transact-SQL デバッガーを使用して、データベース エンジン クエリ エディター ウィンドウで実行される Transact-SQL ステートメントを制御する方法について説明します。
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, debugging code
- Transact-SQL debugger, step over
- Transact-SQL debugger, step out
- Transact-SQL debugger, step into
ms.assetid: e09079b8-c4c9-42b4-821b-4ce81a98a086
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2a953cd71bc267622dd158569da80bc924e89b83
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036235"
---
# <a name="step-through-transact-sql-code"></a>Transact-SQL コードのステップ実行

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] クエリ エディター ウィンドウでどの [!INCLUDE[ssDE](../../includes/ssde-md.md)] ステートメントを実行するかを制御できます。 個々のステートメントでデバッガーを一時停止して、その時点のコード要素の状態を確認できます。  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="breakpoints"></a>ブレークポイント

ブレークポイントは、特定の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントで実行を一時停止することをデバッガーに指示するために使用します。 ブレークポイントの詳細については、「[Transact-SQL ブレークポイント](./transact-sql-breakpoints.md)」を参照してください。  
  
## <a name="controlling-statement-execution"></a>ステートメントの実行の制御

[!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] コードの現在のステートメントからの実行について、次のオプションを指定できます。

- 次のブレークポイントまで実行する。

- 次のステートメントにステップ インする。  

    次のステートメントで [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャ、関数、またはトリガーが呼び出される場合、モジュールのコードが含まれた新しいクエリ エディター ウィンドウが表示されます。 ウィンドウはデバッグ モードに設定され、実行はモジュールの最初のステートメントで一時停止します。 その後、モジュールのコードに対して、ブレークポイントの設定やコードのステップ実行などの操作を行うことができます。

- 次のステートメントにステップ オーバーする。

    次のステートメントが実行されます。 ただし、ステートメントでストアド プロシージャ、関数、またはトリガーが呼び出される場合、モジュールのコードは完了するまで実行され、その結果が呼び出し元のコードに返されます。 ストアド プロシージャにエラーがないことがわかっている場合は、ストアド プロシージャにステップ オーバーできます。 実行は、ストアド プロシージャ、関数、またはトリガーの呼び出しに続くステートメントで一時停止します。

- ストアド プロシージャ、関数、またはトリガーからステップ アウトする。  

    実行は、ストアド プロシージャ、関数、またはトリガーの呼び出しに続くステートメントで一時停止します。  

- すべてのブレークポイントを無視して、現在の位置からポインターの現在の位置まで実行する。  

 [!INCLUDE[tsql](../../includes/tsql-md.md)] デバッガーでのステートメントの実行を制御するためのさまざまな操作方法を次の表に示します。  
  
|アクション|実行するアクション:|  
|------------|---------------------|  
|現在のステートメントから次のブレークポイントまですべてのステートメントを実行する。|**[デバッグ]** メニューの **[続行]** をクリックする。<br /><br /> **[デバッグ]** ツール バーの **[続行]** ボタンをクリックする。|  
|次のステートメントまたはモジュールにステップ インする。|**[デバッグ]** メニューの **[ステップ イン]** をクリックする。<br /><br /> **[デバッグ]** ツール バーの **[ステップ イン]** ボタンをクリックする。<br /><br /> F11 キーを押す。|  
|次のステートメントまたはモジュールにステップ オーバーする。|**[デバッグ]** メニューの **[ステップ オーバー]** をクリックする。<br /><br /> **[デバッグ]** ツール バーの **[ステップ オーバー]** ボタンをクリックする。<br /><br /> F10 キーを押す。|  
|モジュールからステップ アウトする。|**[デバッグ]** メニューの **[ステップ アウト]** をクリックする。<br /><br /> **[デバッグ]** ツール バーの **[ステップ アウト]** ボタンをクリックする。<br /><br /> Shift&lt;/localizedText&gt; + &lt;localizedText&gt;F11&lt;/localizedText&gt; キーを押す。|  
|現在のカーソル位置まで実行する。|クエリ エディター ウィンドウ内で右クリックし、 **[カーソルまで実行]** をクリックする。<br /><br /> Ctrl</localizedText> + <localizedText>F10</localizedText> キーを押す。|  
  
## <a name="see-also"></a>参照

- [Transact-SQL デバッガー情報](./transact-sql-debugger-information.md)