---
title: Notebook を使用して Azure SQL Database をデプロイする
description: このチュートリアルでは、Azure SQL Database を作成する方法について説明します。
author: ninarn
ms.author: ninarn
ms.reviewer: alayu, markingmyname
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 10/16/2020
ms.openlocfilehash: 5b68bda566bdd28c8dd2e70f036dd8e17643f776
ms.sourcegitcommit: 43b92518c5848489d03c68505bd9905f8686cbc0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2020
ms.locfileid: "92155023"
---
# <a name="create-an-azure-sql-database-using-azure-data-studio"></a>Azure Data Studio を使用して Azure SQL Database を作成する

展開ウィザードとノートブックから、Azure Data Studio を使用して Azure SQL Database を作成できます。

## <a name="pre-requisites"></a>前提条件

 - [Azure Data Studio](download-azure-data-studio.md) がインストールされていること
 - アクティブな Azure アカウントとサブスクリプション。 ない場合は、[無料アカウントを作成](https://azure.microsoft.com/free/) します。

## <a name="use-the-deployment-wizard"></a>展開ウィザードを使用

次の手順に従って、展開ウィザードを使用します。これにより、簡単な UI エクスペリエンスで必要な設定を行うことができます。

まず、デプロイ ウィザードで Azure SQL Database を見つけて選択します。

 1. Azure Data Studio で、左側のナビゲーションにある [接続] ビューレットを選択します。
 2. [接続] パネルの上部にある **[...]** ボタンを選択し、 **[新しい展開...]** を選択します。
 3. 展開ウィザードで、 **[Azure SQL Database]** タイルを選択し、使用条件に同意するチェックボックスをオンにします。
 4. [リソースの種類] ドロップダウンで、作成するもの (データベース、データベース サーバー、エラスティック プールのいずれか) を選択します。 Azure に SQL データベースがない場合は、まずデータベースを作成することをお勧めします。
 5. サーバーまたはプールを作成するよう選択した場合は、 **[Azure portal で作成する]** を選択します。データベースを作成するよう選択した場合は、 **[選択]** を選択します。

データベースを作成するよう選択した場合は、次の手順に従います。

 1. Azure アカウントにまだサインインしていない場合は、サインインします。 ウィザードのこのページで問題が発生した場合は、接続を更新できます。
 2. 必要なサブスクリプションとサーバーを選択します。 **[次へ]** を選択します。
 3. データベース名を入力します。
 4. ファイアウォール規則の名前と、Azure Data Studio を実行しているローカル クライアント コンピューターの IP 範囲を入力します。 これにより、データベースの作成後すぐに、ADS からサーバーとデータベースに接続できるようになります。
 5. **[次へ]** を選択します。
 6. 入力したパラメーターを確認し、 **[ノートブックへのスクリプト]** を選択します。

Notebook が開いたら、コンテンツとコードを確認し、必要に応じて変更を加えることができます。 なお、パフォーマンスやコストについて特定の要件がある場合は、コンピューティングとストレージの設定を既定値から別の値へと変更できます。 ただし、Notebook に変更を加えると、検証エラーが発生する可能性があることに注意してください。

最後の手順で、 **[すべて実行]** を選択して、Notebook 内のすべてのセルを実行します。 この処理が完了すると、SQL Database の作成が完了し、ADS に接続してクエリを実行できるようになります。

## <a name="next-steps"></a>次のステップ

データベース、サーバー、またはプールを作成したら、Azure Data Studio でデータベースを[接続してクエリを実行](quickstart-sql-database.md)できます。
