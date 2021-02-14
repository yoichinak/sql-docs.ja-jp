---
title: WideWorldImportersDW-ETL workflow |Microsoft Docs
description: ETL パッケージと SQL Server Integration Services (SSIS) を使用して、WideWorldImporters データベースから WideWorldImportersDW に定期的にデータを移行します。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ce9cd8ee5a4153cb1d744d505a26b400497b460b
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100354050"
---
# <a name="wideworldimportersdw-etl-workflow"></a>WideWorldImportersDW ETL ワークフロー
[!INCLUDE [SQL Server Azure SQL Database](../includes/applies-to-version/sql-asdb.md)]
データの変更に応じて、WideWorldImporters データベースから WideWorldImportersDW データベースにデータを移行するには、 *WWI_Integration* ETL パッケージを使用します。 パッケージは定期的に (通常は毎日) 実行されます。

このパッケージは、SQL Server Integration Services を使用して、(Integration Services で個別の変換ではなく) 一括 T-sql 操作を調整することで、高いパフォーマンスを保証します。

まずディメンションが読み込まれ、次にファクトテーブルが読み込まれます。 エラーが発生すると、いつでもパッケージを再実行できます。

ワークフローは次のようになります。

 ![WideWorldImporters ETL ワークフロー](media/wide-world-importers/wideworldimporters-etl-workflow.png)

ワークフローは、適切な終了時間を決定する式タスクから始まります。 終了時刻は、現在の時刻から数分を引いた値です。 (このアプローチは、現在の時刻に対してデータを要求するよりも堅牢です)。時間が経過すると、任意のミリ秒が切り捨てられます。

メインの処理は、Date ディメンションテーブルを作成することによって開始されます。 この処理により、現在の年のすべての日付がテーブルに設定されます。

次に、一連のデータフロータスクによって各ディメンションが読み込まれます。 次に、各ファクトを読み込みます。

## <a name="prerequisites"></a>必須コンポーネント

- WideWorldImporters および WideWorldImportersDW データベースを含む 2016 (またはそれ以降) の SQL Server (同じまたは異なるインスタンスの SQL Server)
- SQL Server Management Studio
- SQL Server 2016 Integration Services
  - Integration Services カタログを作成していることを確認します。 Integration Services カタログを作成するには、SQL Server Management Studio オブジェクトエクスプローラーで [ **Integration Services**] を右クリックし、[ **カタログの追加**] を選択します。 既定のオプションをそのまま使用します。 SQLCLR を有効にし、パスワードを入力するように求められます。


## <a name="download"></a>ダウンロード

このサンプルの最新リリースについては、「 [wide world-輸入-リリース](https://go.microsoft.com/fwlink/?LinkID=800630)」を参照してください。 *日次 ETL. ispac* Integration Services パッケージファイルをダウンロードします。

サンプルデータベースを再作成するソースコードについては、「 [wide world-インポーター](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/wwi-ssis)」を参照してください。

## <a name="install"></a>インストール

1. Integration Services パッケージを展開します。
   1. Windows エクスプローラーで、毎日の *ETL. ispac* パッケージを開きます。 これにより、SQL Server Integration Services 配置ウィザードが起動します。
   2. [ **ソースの選択**] で、プロジェクトの配置の既定値に従い、 *1 日の ETL. ispac* パッケージを指すパスを使用します。
   3. [ **ターゲットの選択**] で、Integration Services カタログをホストするサーバーの名前を入力します。
   4. たとえば、 *WideWorldImporters* という名前の新しいフォルダーで、Integration Services カタログの下にあるパスを選択します。
   5. [ **配置** ] を選択してウィザードを終了します。

2. ETL プロセス用の SQL Server エージェントジョブを作成します。
   1. Management Studio で、[ **SQL Server エージェント**] を右クリックし、[**新しい** ジョブ] を選択し  >  ます。
   2. *WIDEWORLDIMPORTERS ETL* などの名前を入力します。
   3. 種類 **SQL Server Integration Services パッケージ** の **ジョブステップ** を追加します。
   4. Integration Services カタログがあるサーバーを選択し、 *毎日の ETL* パッケージを選択します。
   5. [**構成**] [  >  **接続マネージャー**] で、ソースとターゲットへの接続が正しく構成されていることを確認します。 既定では、ローカルインスタンスに接続します。
   6. [ **OK** ] を選択してジョブを作成します。

3. ジョブを実行またはスケジュールします。
