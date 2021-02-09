---
title: 証明書の管理 (SQL Server 構成マネージャー)
description: さまざまな SQL Server 構成で証明書をインストールする方法について説明します。 例として、単一インスタンス、フェールオーバー クラスター、Always On 可用性グループがあります。
ms.prod: sql
ms.prod_service: high-availability
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], encrypted
- SSL [SQL Server]
- Secure Sockets Layer (SSL)
- encryption [SQL Server], connections
- cryptography [SQL Server], connections
- certificates [SQL Server], installing
- requesting encrypted connections
- installing certificates
- security [SQL Server], encryption
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: ''
ms.date: 01/12/2021
ms.openlocfilehash: d4ad86b8ce46e39f0143f72badca4926bc0d50b2
ms.sourcegitcommit: 0b400bb99033f4b836549cb11124a1f1630850a1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/09/2021
ms.locfileid: "99978670"
---
# <a name="certificate-management-sql-server-configuration-manager"></a>証明書の管理 (SQL Server 構成マネージャー)

[!INCLUDE [sql-windows-only](../../includes/applies-to-version/sql-windows-only.md)]

このトピックでは、SQL Server Always On フェールオーバー クラスターまたは可用性グループ トポロジにわたって証明書を展開および管理する方法について説明します。

SSL/TLS 証明書は、SQL Server へのアクセスをセキュリティで保護するために広く使われています。 以前のバージョンの SQL Server では、大規模な SQL Server の資産を持つ組織は、その SQL Server 証明書インフラストラクチャを維持するために、多くの場合スクリプトを開発したりコマンドを手動で実行したりして、かなりの労力を費やす必要がありました。 SQL Server 2019 では、証明書の管理が SQL Server 構成マネージャーに統合されており、次のような一般的なタスクが簡単になりました。 

* SQL Server インスタンスにインストールされている証明書の表示と検証。 
* 期限切れに近づいている可能性のある証明書の特定。 
* Always On 可用性グループ マシンへの証明書の展開 (プライマリ レプリカを保持するノードから)。 
* Always On フェールオーバー クラスター インスタンスに参加しているマシンへの証明書の展開 (アクティブなノードから)。

> [!NOTE]
> SQL Server 構成マネージャーの証明書の管理は、SQL Server 2008 以降の古いバージョンの SQL Server で使用できます。

##  <a name="to-install-a-certificate-for-a-single-sql-server-instance"></a><a name="provision-single-server-cert"></a> 1 つの SQL Server インスタンス用の証明書をインストールするには  

::: moniker range=">=sql-server-ver15"
1. SQL Server 構成マネージャーのコンソール ペインで、 **[SQL Server ネットワークの構成]** を展開します。  

2. [ *&lt;インスタンス名&gt;* **のプロトコル**] を右クリックし、 **[プロパティ]** を選択します。  

3. **[証明書]** タブを選択し、 **[インポート]** を選択します。  

4. **[参照]** を選択し、証明書ファイルを選択します。  

5. **[次へ]** を選択して、証明書を検証します。 エラーがない場合は、 **[次へ]** を選択して、ローカル インスタンスに証明書をインポートします。  
::: moniker-end

::: moniker range="<= sql-server-2017"
1. SQL Server 構成マネージャーのコンソール ペインで、 **[SQL Server ネットワークの構成]** を展開します。  

2. [ *&lt;インスタンス名&gt;* **のプロトコル**] を右クリックし、 **[プロパティ]** を選択します。  

3. **[証明書]** ドロップダウン メニューから証明書を選んでから、 **[適用]** を選択します。  

4. **[OK]** を選択します。 
::: moniker-end

##  <a name="to-install-a-certificate-in-a-failover-cluster-instance-configuration"></a><a name="provision-failover-cluster-cert"></a> フェールオーバー クラスター インスタンス構成で証明書をインストールするには  
  
1. SQL Server 構成マネージャーのコンソール ペインで、 **[SQL Server ネットワークの構成]** を展開します。
  
2. [ *&lt;インスタンス名&gt;* **のプロトコル**] を右クリックし、 **[プロパティ]** を選択します。 

3. **[証明書]** タブを選択し、 **[インポート]** を選択します。

4. 証明書の種類を選択し、現在のノードに対してのみインポートするか、または個々のクラスター ノードごとにインポートするかを選択します。

5. 1 つのノードに対してインストールする場合は、 **[参照]** を選択し、証明書ファイルを選択します。 その後、手順 8. に進みます。

6. ノードごとに証明書をインストールする場合は、 **[次へ]** を選択して、所有者ノード候補を一覧表示します。 現在のフェールオーバー クラスター インスタンスの所有者候補が、あらかじめ選択されています。

7. **[次へ]** を選択して、インポートする証明書を選択します。

8. パスワードの入力を求められたら、入力します。 検証後に、警告やエラーを探します。

9. **[次へ]** を選択して、選択した証明書をインポートします。

> [!NOTE]
> これらの手順は、Always On フェールオーバー クラスター インスタンスのアクティブ ノードで実行します。 ユーザーには、すべてのクラスター ノードでの管理者権限が必要です。

##  <a name="to-install-a-certificate-in-an-always-on-availability-group-configuration"></a><a name="provision-availability-group-cert"></a>Always On 可用性グループ構成で証明書をインストールするには  
  
1. SQL Server 構成マネージャーのコンソール ペインで、 **[SQL Server ネットワークの構成]** を展開します。
  
2. [ *&lt;インスタンス名&gt;* **のプロトコル**] を右クリックし、 **[プロパティ]** を選択します。  
  
3. **[証明書]** タブを選択し、 **[インポート]** を選択します。  
  
4. 証明書の種類を選択し、 **[次へ]** を選択して、既知の可用性グループの一覧から選択します。  

5. **[次へ]** を選択して、各レプリカ ノード用の証明書を選択します。 証明書のファイル名は、ノードの NetBios 名と一致する必要があります。

6. **[次へ]** を選択して、各ノードに選択した証明書をインポートします。


> [!NOTE]
> これらの手順は、可用性グループのプライマリ レプリカを保持しているノードから実行します。 ユーザーには、すべてのクラスター ノードでの管理者権限が必要です。

