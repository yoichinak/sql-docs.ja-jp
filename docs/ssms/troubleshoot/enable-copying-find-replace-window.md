---
description: '[検索と置換] ウィンドウからのコピーを有効にするための回避策 '
title: '[検索と置換] ウィンドウからのコピーを有効にする'
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan, sstein
ms.custom: seo-lt-2019
ms.date: 11/03/2020
ms.openlocfilehash: ea5ae3f9fa941e723d3bdf10de0ec900310cc28d
ms.sourcegitcommit: 985e2e8e494badeac6d6b652cd35765fd9c12d80
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2020
ms.locfileid: "93328782"
---
# <a name="workaround-to-enable-copying-from-find-and-replace-window"></a>[検索と置換] ウィンドウからのコピーを有効にするための回避策

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

[検索と置換] ウィンドウからのコピーを有効にするには、回避策が必要です。  SQL Server Management Studio の [検索と置換] ウィンドウからコピーできない場合は、下記の「[回避策](#workaround)」に従ってください。

## <a name="error-message"></a>エラー メッセージ

SQL Server Management Studio の [検索と置換] ウィンドウからテキストをコピーしようとすると、エラー メッセージが表示されます。

> 未保存のドキュメントをその他のファイル プロジェクトから切り取ったり、クリップボードにコピーしたりすることはできません。 切り取りやコピーを実行する前に、未保存のドキュメントを保存する必要があります。

![次のエラー ダイアログが表示されます。未保存のドキュメントをその他のファイル プロジェクトから切り取ったり、クリップボードにコピーしたりすることはできません。 切り取りやコピーを実行する前に、未保存のドキュメントを保存する必要があります。](../media/troubleshoot/unable-copy-find-replace-window.png)

## <a name="workaround"></a>回避策

[検索と置換] ウィンドウからテキストをコピーできるようにするには、次の手順を行います。

1. **[ツール]** メニューで、 **[オプション]** を開きます。

2. **[環境]** > **[ドキュメント]** の順に進み、[その他のファイルをソリューション エクスプローラーに表示] の項目をオフにします。

3. SQL Server Management Studio を閉じ、再度開きます。

![[その他のファイルをソリューション エクスプローラーに表示] がオフになっている [オプション] ウィンドウ](../media/troubleshoot/fix-copy-find-replace-window.png)

