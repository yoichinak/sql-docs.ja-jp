---
title: Azure Virtual Machines に SQL Server をデプロイする
description: このチュートリアルでは、Azure Virtual Machines 上で SQL Server を作成する方法について説明します
author: ninarn
ms.author: ninarn
ms.reviewer: alayu, maghan
ms.topic: tutorial
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 453ec8226b018b1d5d756ba96ac174823657c5dd
ms.sourcegitcommit: 76ab3b57718341c6057613c9bd38cf82fb17786e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92060883"
---
# <a name="create-sql-server-on-azure-virtual-machines-using-azure-data-studio"></a>Azure Data Studio を使用して Azure Virtual Machines 上に SQL Server を作成する

展開ウィザードとノートブックから Azure Data Studio を使用して、SQL 仮想マシン (VM) を作成できます。

## <a name="pre-requisites"></a>前提条件

- [Azure Data Studio](download-azure-data-studio.md) がインストールされていること
- アクティブな Azure アカウントとサブスクリプション。 アカウントがない場合は、[無料アカウントを作成](https://azure.microsoft.com/free/)してください。

## <a name="use-the-deployment-wizard"></a>展開ウィザードを使用

次の手順に従って、展開ウィザードを使用します。これにより、簡単な UI エクスペリエンスで必要な設定を行うことができます。

まず、展開ウィザードで Azure SQL VM を見つけて選択します。

1. Azure Data Studio で、左側のナビゲーションにある [接続] ビューレットを選択します。

2. [接続] パネルの上部にある **[...]** ボタンを選択し、 **[新しい展開]** を選択します。

3. 展開ウィザードで、 **[Azure SQL VM]** タイルを選択し、使用条件に同意するチェックボックスをオンにします。

4. 求められたら、必要なツールをインストールし、下部にある **[選択]** ボタンを選択します。

次に、Azure SQL VM ウィザードで必要なすべてのパラメーターを入力します。

1. Azure アカウントにまだサインインしていない場合は、サインインします。 ウィザードのこのページで問題が発生した場合は、接続を更新できます。

2. 目的のサブスクリプション、リソース グループ、リージョンを選択します。 **[次へ]** を選択します。

3. 一意の仮想マシン名と、ユーザー名とパスワード資格情報を入力します。

4. 任意のイメージ、SKU、バージョンを選択し、任意の VM サイズを選択します。 [使用可能な VM サイズ](https://docs.microsoft.com/azure/virtual-machines/sizes)の詳細を確認すると、選択に役立ちます。 **[次へ]** を選択します。

5. ドロップダウン リストから既存の仮想ネットワークを選択するか、 **[新しい仮想ネットワーク]** チェックボックスをオンにして新しい仮想ネットワークの名前を入力します。

6. サブネットとパブリック IP アドレスを選択または作成する場合も、同じ操作を行います。

7. リモート デスクトップ (RDP) 経由で VM に接続する場合は、 **[Enable RDP inbound port]\(RDP 受信ポートを有効にする\)** チェックボックスをオンにします。 **[次へ]** を選択します。

8. 任意の SQL Server 設定を入力します。 このエクスペリエンスをテストするには、SQL 接続を **[パブリック (インターネット)]** に設定し、ポート 1433 を入力し、任意のユーザー名とパスワードを使用して SQL 認証を有効にすることをお勧めします。 **[次へ]** を選択します。

9. 入力したパラメーターを確認し、 **[ノートブックへのスクリプト]** を選択します。

Notebook が開いたら、コンテンツとコードを確認し、必要に応じて変更を加えることができます。 ただし、検証エラーが発生する可能性があるため、変更を行うことはお勧めしません。

最後の手順で、 **[すべて実行]** を選択して、Notebook 内のすべてのセルを実行します。 これが完了すると、以下が完全に作成され、実行されます。

- Azure 仮想マシン
- SQL 仮想マシン
- 仮想ネットワーク、サブネット、パブリック IP アドレス
- ネットワーク セキュリティ グループとネットワーク インターフェイス
- VM への RDP へのアクセス
- さまざまな SQL Server 管理機能にアクセスして、バックアップ スケジュール、修正プログラムの適用スケジュール、SQL Server のエディションとライセンス、ストレージパフォーマンス構成などを簡単に制御できます。

## <a name="next-steps"></a>次のステップ

新しい SQL VM にデータを移行する方法の詳細については、次の記事を参照してください。

> [!div class="nextstepaction"]
> [SQL VM にデータベースを移行する](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/migrate-to-vm-from-sql-server)

Azure での SQL Server の使用に関するその他の情報については、[Azure 仮想マシンにおける SQL Server](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/sql-server-on-azure-vm-iaas-what-is-overview) に関する記事と[よく寄せられる質問](https://docs.microsoft.com/azure/azure-sql/virtual-machines/windows/frequently-asked-questions-faq)に関するページを参照してください。
