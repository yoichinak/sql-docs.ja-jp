---
title: ブレークポイントの有効化、無効化、および削除
description: '[ブレークポイント] ウィンドウを使用して、ブレークポイントの表示、削除、無効化、および有効化を行う方法について説明します。'
titleSuffix: T-SQL debugger
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 357b5874-273f-43a9-8e30-83872bdea5dc
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 091f6a4fbe7650152eaf7b3c605618875013f92a
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92039058"
---
# <a name="enable-disable-and-delete-breakpoints"></a>ブレークポイントの有効化、無効化、および削除

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

開かれているすべてのブレークポイントを表示および管理するには、 **[ブレークポイント]** ウィンドウを使用します。 ブレークポイントの情報を表示し、各種の操作 (ブレークポイントの削除、無効化、有効化など) を実行するには、このウィンドウを使用します。

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]
  
## <a name="the-breakpoints-window"></a>[ブレークポイント] ウィンドウ  
 **[ブレークポイント]** ウィンドウには、ブレークポイントが設定されているコード行などの情報が表示されます。 **[ブレークポイント]** ウィンドウでは、ブレークポイントの削除、無効化、および有効化を行うこともできます。 **[ブレークポイント]** ウィンドウの詳細については、「 [[ブレークポイント] Window](./transact-sql-debugger-breakpoints-window.md)」を参照してください。  
  
 ブレークポイントを無効化した場合、そのブレークポイントで実行は一時停止されませんが、後でブレークポイントを有効化できるように、定義がその位置に保持されます。 削除したブレークポイントは完全に削除されます。 そのステートメントで実行を一時停止するには、新たにブレークポイントを設定する必要があります。  
  
## <a name="to-open-the-breakpoints-window"></a>[ブレークポイント] ウィンドウを開くには  
 **To open the Breakpoints window**  
  
 **[ブレークポイント]** ウィンドウを開くには、次のいずれかの方法を使用します。  
  
-   **[デバッグ]** メニューの **[ウィンドウ]** をポイントし、 **[ブレークポイント]** をクリックします。  
  
-   **[デバッグ]** ツール バーの **[ブレークポイント]** ボタンをクリックする。  
  
-   Ctrl + Alt + B キーを押す。  
  
## <a name="to-disable-a-single-breakpoint"></a>単一のブレークポイントを無効にするには  
 **To disable a single breakpoint**  
  
 単一のブレークポイントを無効にするには、次のいずれかの方法を使用します。  
  
-   クエリ エディター ウィンドウで、ブレークポイントを右クリックし、 **[ブレークポイントの無効化]** をクリックする。  
  
-   [ブレークポイント] ウィンドウで、ブレークポイントの左側のチェック ボックスをオフにする。  
  
## <a name="to-disable-all-breakpoints"></a>すべてのブレークポイントを無効にするには  
 **To disable all breakpoints**  
  
 すべてのブレークポイントを無効にするには、次のいずれかの方法を使用します。  
  
-   **[デバッグ]** メニューの **[すべてのブレークポイントを無効にする]** をクリックする。  
  
-   **[ブレークポイント]** ウィンドウのツール バーの **[すべてのブレークポイントを無効にする]** ボタンをクリックする。  
  
## <a name="to-enable-a-single-breakpoint"></a>単一のブレークポイントを有効にするには  
 **To enable a single breakpoint**  
  
 単一のブレークポイントを有効にするには、次のいずれかの方法を使用します。  
  
-   クエリ エディター ウィンドウで、ブレークポイントを右クリックし、 **[ブレークポイントの有効化]** をクリックする。  
  
-   [ブレークポイント] ウィンドウで、ブレークポイントの左側のボックスをオンにする。  
  
## <a name="to-enable-all-breakpoints"></a>すべてのブレークポイントを有効にするには  
 **To enable all breakpoints**  
  
 すべてのブレークポイントを有効にするには、次のいずれかの方法を使用します。  
  
-   **[デバッグ]** メニューの **[すべてのブレークポイントを有効にする]** をクリックする。  
  
-   **[ブレークポイント]** ウィンドウのツール バーの **[すべてのブレークポイントを有効にする]** ボタンをクリックする。  
  
## <a name="to-delete-a-single-breakpoint"></a>単一のブレークポイントを削除するには  
 **To delete a single breakpoint**  
  
 単一のブレークポイントを削除するには、次のいずれかの方法を使用します。  
  
-   クエリ エディター ウィンドウで、ブレークポイントを右クリックし、 **[ブレークポイントの削除]** をクリックする。  
  
-   [ブレークポイント] ウィンドウで、ブレークポイントを右クリックし、ショートカット メニューの **[削除]** をクリックする。  
  
-   [ブレークポイント] ウィンドウで、ブレークポイントを選択し、Del キーを押す。  
  
## <a name="to-delete-all-breakpoints"></a>すべてのブレークポイントを削除するには  
 **To delete all breakpoints**  
  
 すべてのブレークポイントを削除するには、次のいずれかの方法を使用します。  
  
-   **[デバッグ]** メニューの **[すべてのブレークポイントの削除]** をクリックする。  
  
-   **[ブレークポイント]** ウィンドウのツール バーの **[すべてのブレークポイントの削除]** ボタンをクリックする。  
  
## <a name="see-also"></a>参照  
 [ブレークポイントの切り替え](./toggle-a-breakpoint.md)  
  
