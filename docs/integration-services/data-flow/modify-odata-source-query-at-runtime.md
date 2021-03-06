---
description: 実行時の OData ソース クエリの提供
title: 実行時の OData ソース クエリの提供 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: bcbba7f4-6e5d-46e6-a73a-3f17d3ff376a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3cddac6ff27883aac6840f9ce3c04ba4441d1e71
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100343238"
---
# <a name="provide-an-odata-source-query-at-runtime"></a>実行時の OData ソース クエリの提供

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


 データ フロー タスクの **[OData ソース].[クエリ]** プロパティに *式* を追加すると、OData ソースのクエリを実行時に変更できます。  
  
 返される列は、デザイン時に返されたものと同じ列である必要があります。それ以外の場合、パッケージの実行時にエラーが発生します。 $select クエリ オプションを使用する場合は、同じ列を (同じ順序で) 指定してください。 $select オプションを使用するより安全な代替手段は、ソース コンポーネント UI で、直接使用することを希望しない列を選択解除することです。  
  
 クエリの値を実行時に動的に設定するいくつかの方法があります。 次に、いくつかの一般的な方法を示します。  
  
## <a name="provide-the-query-as-a-parameter"></a>クエリをパラメーターとして指定する  
 次の手順では、OData ソース コンポーネントによって使用されるクエリを、パッケージのパラメーターとして公開する方法を示します。  
  
1.  **[データ フロー タスク]** を右クリックし、 **[パラメーター化]** オプションを選択します。  
  
2.  **[パラメーター化]** ダイアログで、 **[プロパティ]** に対して **[\<Name of the OData Source Component>].[Query]** を選択します。  
  
3.  **[新しいパラメーターの作成]** または **[既存のパラメーターを使用する]** のどちらかを選択します。  
  
4.  **[新しいパラメーターを作成する]** を選択した場合は、次の作業を実行します。  
  
    1.  パラメーターの **[名前]** と **[説明]** を入力します。  
  
    2.  パラメーターの既定の **[値]** を指定します。  
  
    3.  パラメーターに対応する **[スコープ]** ( **[パッケージ]** または **[プロジェクト]** ) を指定します。  
  
    4.  パラメーターが **[必須]** であるかどうかを指定します。  
  
5.  **[OK]** をクリックしてダイアログ ボックスを閉じます。  
  
## <a name="provide-the-query-with-an-expression"></a>クエリに式を指定する
 この方法は、クエリ文字列を実行時に動的に構築する場合に役立ちます。
  
1.  使用中の **[OData ソース]** を含む **[データ フロー タスク]** を選択します。  
  
2.  **[プロパティ]** ウィンドウで、 **[Expressions]** プロパティを強調表示します。  
  
3.  [...] (省略記号) をクリックすると、 **[プロパティ式エディター]** が表示されます。  
  
4.  **[OData ソース].[クエリ]** プロパティを選択します。  
  
5.  **[式]** に対応する [...] (省略記号) ボタンをクリックします。  
  
6.  **[式]** を入力します。  
  
7.  **[OK]** をクリックします。  
  
> [!NOTE]  
> この方法を使用する場合は、設定した値が正しく URL エンコードされていることを確認する必要があります。 ユーザー入力から値を受け取る (たとえば、パラメーターに基づいて個々のクエリ オプションの値を設定する) 場合は、SQL インジェクション型の攻撃の可能性を防止するために、値を検証する必要があります。  
  
  
