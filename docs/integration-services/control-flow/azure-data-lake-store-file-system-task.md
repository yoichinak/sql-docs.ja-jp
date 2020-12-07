---
description: Azure Data Lake Store ファイル システム タスク
title: Azure Data Lake Store ファイル システム タスク | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: Lingxi-Li
ms.author: lingxl
ms.reviewer: maghan
ms.openlocfilehash: 27ee71393bfbad6c824de25bd95c9ca465cf2a51
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96123643"
---
# <a name="azure-data-lake-store-file-system-task"></a>Azure Data Lake Store ファイル システム タスク

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]



Azure Data Lake Store ファイル システム タスクでは、ユーザーは [Azure Data Lake Store (ADLS)](https://azure.microsoft.com/services/data-lake-store/) でさまざまなファイル システム操作を実行できます。

Azure Data Lake Store ファイル システム タスクは、[SQL Server Integration Services (SSIS) Feature Pack for Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md) のコンポーネントです。

## <a name="configure-the-azure-data-lake-store-file-system-task"></a>Azure Data Lake Store ファイル システム タスクの構成

パッケージに Azure Data Lake Store ファイル システム タスクを追加するには、SSIS ツールボックスからデザイナー キャンバスにドラッグします。 次に、タスクをダブルクリックするか、右クリックして **[編集]** を選択し、**[Azure Data Lake Store File System Task Editor]\(Azure Data Lake Store ファイル システム タスク エディター\)** ダイアログ ボックスを開きます。

**[操作]** プロパティでは、実行するファイル システム操作を指定します。 以下の操作のいずれかを選択します。

- **CopyToADLS:** ADLS にファイルをアップロードします。
- **CopyFromADLS:** ADLS からファイルをダウンロードします。

## <a name="configure-the-properties-for-the-operation"></a>操作のプロパティの構成
操作に対して、Azure Data Lake 接続マネージャーを指定する必要があります。

各操作に固有のプロパティを以下に示します。

### <a name="copytoadls"></a>CopyToADLS
- **LocalDirectory:** アップロードするファイルを含むローカル ソース ディレクトリを指定します。
- **FileNamePattern:** ソース ファイルのファイル名フィルターを指定します。 名前が指定されたパターンと一致するファイルのみがアップロードされます。 ワイルドカードの `*` と `?` がサポートされています。
- **SearchRecursively:** アップロードするファイルのソース ディレクトリ内で再帰的に検索するかどうかを指定します。
- **AzureDataLakeDirectory:** ファイルのアップロード先となる ADLS ディレクトリを指定します。
- **FileExpiry:** ADLS にアップロードされたファイルの有効期限の日時を指定します。 ファイルの有効期限が切れないようにする場合は、このプロパティを空白のままにします。

### <a name="copyfromadls"></a>CopyFromADLS
- **AzureDataLakeDirectory:** ダウンロードするファイルを含む ADLS ソース ディレクトリを指定します。
- **SearchRecursively:** ダウンロードするファイルのソース ディレクトリ内で再帰的に検索するかどうかを指定します。
- **LocalDirectory:** ダウンロードしたファイルの格納先となるディレクトリを指定します。
