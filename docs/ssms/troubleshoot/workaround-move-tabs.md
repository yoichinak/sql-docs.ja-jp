---
description: タブ移動の回避策
title: SSMS がクラッシュすることなくタブを移動できるようにする
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
ms.openlocfilehash: ae7c79792d962ce578059e672de7165f477f1c4a
ms.sourcegitcommit: 6c93282cce1216dac327cb28848a3ab4d51b776e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/18/2021
ms.locfileid: "100654632"
---
# <a name="workaround-to-move-tabs"></a>タブ移動の回避策

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

ウィンドウ内で、または以前に削除したタブをドッキングする場合でも、クエリ エディターのタブを移動できるようにするために、回避策が必要になる場合があります。使用可能なすべての Windows 更新プログラムを適用していて、クラッシュを発生させずにクエリ エディターのタブを操作できない場合は、次の[回避策](#workaround)に従ってください。

## <a name="applicable-environments"></a>適用可能な環境
.NET Framework に対する Windows 更新プログラムで既知の問題が発生しました。これにより、タブをドッキングしたりウィンドウを分割したりするときに、SQL Server Management Studio (SSMS) のアプリケーションがクラッシュします。  最新の情報については [SQL Server ユーザー フィードバック](https://feedback.azure.com/forums/908035/suggestions/42651556)を参照してください。

## <a name="workaround"></a>回避策

利用可能なすべての Windows 更新プログラムを適用した後もクラッシュが続く場合は、次の手順に従って問題を軽減してください。

1. すべての SQL Server Management Studio (SSMS) インスタンスを閉じます。

2. SSMS アプリケーション ファイル (exe) を見つけます。  これは通常、`C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE` にあります。

3. メモ帳でファイル `Ssms.exe.config` を管理者として開きます。

4. `AppContextSwitchOverrides` ノードを見つけ、これら 2 つのプロパティを値に追加します。
    ```
    ;Switch.System.Windows.Interop.MouseInput.OptOutOfMoveToChromedWindowFix=true; Switch.System.Windows.Interop.MouseInput.DoNotOptOutOfMoveToChromedWindowFix=true
    ```

    ![ssms.exe.config の編集](../media/troubleshoot/execonfig-edit.png)

5. 構成ファイルを保存し、SSMS を再度開きます。
