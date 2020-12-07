---
title: Machine Learning の拡張機能で予測を行う
description: Azure Data Studio の Machine Learning 拡張機能を使用して、データベースの ONNX モデルで予測を行う方法について説明します。
ms.prod: azure-data-studio
ms.technology: machine-learning
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.reviewer: sstein
ms.custom: ''
ms.date: 06/09/2020
ms.openlocfilehash: 2b68f15f69d3efb0a773022e87615d298da07706
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725158"
---
# <a name="make-predictions-with-machine-learning-extension-for-azure-data-studio-preview"></a>Azure Data Studio の Machine Learning 拡張機能を使用して予測を行う (プレビュー)

[Azure Data Studio の Machine Learning 拡張機能](machine-learning-extension.md)を使用して、データベースの ONNX モデルで予測を行う方法について説明します。 拡張機能では、[PREDICT](../../t-sql/queries/predict-transact-sql.md) を使用して T-SQL スクリプトを生成し、以前にインポートされたモデル、ローカル ファイル内に存在するモデル、または Azure Machine Learning からのモデルを使用して、テーブルに格納されているデータセットに対して予測を行います。

> [!IMPORTANT]
> Machine Learning 拡張機能を使用した予測では、現在、[Azure SQL Managed Instance での Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview) と、[ONNX を使用した Azure SQL Edge](/azure/azure-sql-edge/onnx-overview) のみがサポートされています。

## <a name="prerequisites"></a>前提条件

- [Azure Data Studio の Machine Learning 拡張機能](machine-learning-extension.md)のインストールと構成。 [[拡張機能の設定] で Python インストール パス](machine-learning-extension.md#settings)を指定する必要があります。

- **onnxruntime**、**mlflow**、および **mlflow-dbstore** の各 Python パッケージ。 パッケージがまだインストールされていない場合は、Machine Learning 拡張機能によってインストールするように求められます。

## <a name="make-predictions-from-onnx-model"></a>ONNX モデルから予測を行う

ONNX モデルを使用して予測を行うには、次の手順に従います。

1. **[Make predictions]\(予測を行う\)** を選択します。

1. **onnxruntime**、**mlflow**、**mlflow-dbstore** をインストールするように求められた場合は、 **[はい]** を選択します。

1. モデルが配置されている場所を選択し、 **[次へ]** を選択します。 使用できるもの:
    - **インポートされたモデル**。 データベースに既に格納されているモデルを使用する場合は、このオプションを選択します。 モデルが配置されている**モデル データベース**と**モデル テーブル**を選択し、使用するモデルを選択し、 **[次へ]** を選択します。
    - **ファイルのアップロード**。 ファイルからモデルを使用する場合は、これを選択します。 **[ソース ファイル]** でモデル ファイルを選択し、 **[次へ]** を選択します。
    - **Azure Machine Learning**。 Azure Machine Learning のモデルを使用するには、これを選択します。 最初に、**Azure にサインイン**します。 次に、ご自分の **Azure アカウント**、**Azure サブスクリプション**、**Azure リソース グループ**、**Azure ML ワークスペース**を選択します。 使用するモデルを選択し、 **[次へ]** を選択します。

1. ソース データをモデルにマップします。
    - 予測を適用するデータ セットを含む**ソース データベース**と**ソース テーブル**を選択します。
    - **[Model Input mapping]\(モデルの入力のマッピング\)** と **[モデルの出力]** の下に列をマップします。 この拡張機能では、同じ名前とデータ型の列が自動的にマップされます。

1. **[予測]** を選択します。

Azure Data Studio によって、[PREDICT](../../t-sql/queries/predict-transact-sql.md) を使用して新しい T-SQL クエリが作成されます。これを使用して、データの予測を行うことができます。

## <a name="next-steps"></a>次のステップ

- [Azure Data Studio の Machine Learning 拡張機能](machine-learning-extension.md)
- [データベースでのパッケージの管理](machine-learning-extension-manage-packages.md)
- [モデルのインポートまたは表示](machine-learning-extension-import-view-models.md)
- [Azure Data Studio のノートブック](../notebooks/notebooks-guidance.md)
- [SQL の機械学習のドキュメント](../../machine-learning/index.yml)
- [Azure SQL Managed Instance の Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)
- [SQL Edge (プレビュー) での ONNX を使用した機械学習と AI](/azure/azure-sql-edge/onnx-overview)