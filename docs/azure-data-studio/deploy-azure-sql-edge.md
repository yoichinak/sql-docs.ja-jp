---
title: Azure Data Studio を使用して Azure SQL Edge をデプロイする
description: Azure Data Studio で Azure SQL Edge インスタンスをデプロイする方法
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: 74901a5360e4b9badcc7569211bfaea90d2b94a3
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725223"
---
# <a name="deploy-azure-sql-edge-with-azure-data-studio-preview"></a>Azure Data Studio を使用して Azure SQL Edge をデプロイする (プレビュー)

[Azure SQL Edge](/azure/azure-sql-edge/overview) は、IoT および Azure IoT Edge のデプロイ向けに最適化されたリレーショナル データベース エンジンです。 これは、IoT のアプリケーションおよびソリューションに向けて、パフォーマンスの高いデータ ストレージと処理レイヤーを作成する機能を提供します。 この記事では、Azure Data Studio を使用して Azure SQL Edge インスタンスをデプロイする方法と、デプロイ ウィザードでサポートされているデプロイ シナリオを示します。  

Azure Data Studio のデプロイ ウィザードでは、次のシナリオがサポートされています。

- ローカル コンテナー インスタンス
- リモート コンテナー インスタンス
- 新しい Azure IoT Hub と VM
- Azure IoT Hub の既存のデバイス
- Azure IoT Hub の複数のデバイス

| 必要なツール | `Docker` | `Azure CLI` |
| ------------- | :---: | :---: |
| ローカル コンテナー インスタンス | x | |
| リモート コンテナー インスタンス | | |
| 新しい Azure IoT Hub と VM | | x |
| Azure IoT Hub の既存のデバイス |  | x |
| Azure IoT Hub の複数のデバイス |   |  x |

> [!NOTE]
> Azure SQL Edge のデプロイ (プレビュー) は、拡張機能である "Azure SQL Edge デプロイ拡張機能" を通じて使用できますが、これらの機能はプレビュー段階です。 機能を使用できるようにするために、Azure Data Studio に拡張機能をインストールしてください。

Azure Data Studio でデプロイを開始するには、 **[接続]** ビューでメニューを開き、 **[新しいデプロイ...]** オプションを選択します。  すべての Azure SQL Edge シナリオについて、次の画面で **[Azure SQL Edge]** を選択し、 **[デプロイ ターゲット]** ドロップダウンから目的のシナリオを選びます。 デプロイ ウィザードによって、デプロイを完了するために実行できる TSQL ノートブックが生成されます。 既定では、SQL 管理者パスワードなどの接続情報がノートブックに含まれていることに注意してください。

![デプロイの概要](media/deploy-azure-sql-edge/deploy-overview.png)

## <a name="local-container-instance"></a>ローカル コンテナー インスタンス

Azure SQL Edge は、コンテナー名、`sa` ユーザー パスワード、および Azure SQL Edge 接続用のホスト ポートを指定することで、localhost 上の Docker コンテナーにデプロイできます。  デプロイが完了した後、ノートブックの下部にあるいくつかのリンクを使用して、さらに操作を行うことができます。

- **ここを選択して、Azure SQL Edge インスタンスに接続する**: Azure Data Studio で新しい Azure SQL Edge インスタンスへの接続を作成します
- **ターミナル ウィンドウを開く**: Azure Data Studio で (既存または新規の) ターミナルを開きます
- **コンテナーを停止する**: ユーザーが実行したときにコンテナーを停止するコマンドをターミナルにコピーします
- **コンテナーを削除する**: ユーザーが実行したときにコンテナーを削除するコマンドをターミナルにコピーします

## <a name="remote-container-instance"></a>リモート コンテナー インスタンス

Azure SQL Edge は、Docker がインストールされているリモート ホスト上の Docker コンテナーにデプロイできます。そのためには、コンテナー情報およびターゲットとホスト マシンの情報を指定します。  デプロイが完了した後、ノートブックの下部にある接続リンクを使用できます。  リモート コンテナー ホスト環境であるため、コンテナーを停止または削除するには、コマンドをコピーしてリモート シェルで実行する必要があります。

## <a name="new-azure-iot-hub-and-vm"></a>新しい Azure IoT Hub と VM

Azure SQL Edge デプロイ ウィザードでは、Azure IoT ハブに接続されているエッジ対応仮想マシン (VM) をデプロイするために必要ないくつかの Azure リソースを作成できます。 アクティブな Azure サブスクリプションが必要です。 このデプロイによって次のものが作成されます。

- リソース グループ (現在のリソース グループが選択されていない場合)
- ネットワーク セキュリティ グループ
- 仮想マシン
- 静的パブリック IP アドレス

必要に応じて、dacpac ファイルをフォルダーに圧縮し、プロセスの一部として新しい Azure SQL Edge インスタンスにデプロイすることができます。  dacpac ファイルが指定されている場合は、同じリソース グループ内に Azure Blob Storage アカウントが作成されます。

## <a name="existing-device-of-an-azure-iot-hub"></a>Azure IoT Hub の既存のデバイス

既存の IoT ハブと接続されているデバイスがある場合は、リソース グループ、IoT ハブ名、およびデバイス ID に基づいて、Azure SQL Edge をデバイスにデプロイすることができます。
デプロイ ウィザードで指定された IP アドレスを利用して、ノートブックの下部にクイック接続リンクが生成されます。

必要に応じて、dacpac ファイルをフォルダーに圧縮し、プロセスの一部として新しい Azure SQL Edge インスタンスにデプロイすることができます。  dacpac ファイルが指定されている場合は、同じリソース グループ内に Azure Blob Storage アカウントが作成されます。

## <a name="multiple-devices-of-an-azure-iot-hub"></a>Azure IoT Hub の複数のデバイス

既存の IoT ハブと接続されているデバイスがある場合は、リソース グループ、IoT ハブ名、およびデバイスを選択するための[ターゲット条件](/azure/iot-edge/module-deployment-monitoring#target-condition)に基づいて、デバイスに Azure SQL Edge をデプロイしすることができます。
デプロイ ウィザードで指定された IP アドレスを利用して、ノートブックの下部にクイック接続リンクが生成されます。

必要に応じて、dacpac ファイルをフォルダーに圧縮し、プロセスの一部として新しい Azure SQL Edge インスタンスにデプロイすることができます。  dacpac ファイルが指定されている場合は、同じリソース グループ内に Azure Blob Storage アカウントが作成されます。

## <a name="next-steps"></a>次のステップ

- [Azure SQL Edge についてさらに学習する](/azure/azure-sql-edge/)