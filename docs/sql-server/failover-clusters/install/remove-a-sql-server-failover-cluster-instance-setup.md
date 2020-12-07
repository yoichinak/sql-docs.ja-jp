---
title: フェールオーバー クラスター インスタンスを削除する
description: この手順を使用して、Always On のフェールオーバー クラスター インスタンスをアンインストールします。 この記事では、先に進む前に、重要な考慮事項について説明します。
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: how-to
helpviewer_keywords:
- clusters [SQL Server], removing failover cluster instance
- failover clustering [SQL Server], removing failover cluster instance
- uninstalling failover cluster instances
- removing failover cluster instances
ms.assetid: bf63353b-69cf-4c5c-98ea-7b151e36537f
author: cawrites
ms.author: chadam
ms.openlocfilehash: 3a5da3c50888975301c5d576c634381b5b2e5310
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96121216"
---
# <a name="remove-a-failover-cluster-instance-setup"></a>フェールオーバー クラスター インスタンスの削除 (セットアップ)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

この手順を使用して、Always On [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のフェールオーバー クラスター インスタンスをアンインストールします。  
  
> [!IMPORTANT]  
>  Windows Server フェールオーバー クラスターのすべてのノードにサービスとしてログインする権限を持つローカル管理者だけが、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターを更新または削除できます。  
  
 **Before you begin**  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスをアンインストールする前に、次の重要な点について検討します。  
  
-   誤って [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client をアンインストールすると、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] リソースを起動できなくなります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client を再インストールするには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップ プログラムを実行し、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に必要なコンポーネントをインストールします。  
  
-   複数の SQL IP クラスター リソースを持つフェールオーバー クラスターをアンインストールする場合は、フェールオーバー クラスター マネージャーまたは PowerShell を使用してすべての SQL IP リソースを削除する必要があります。  
  
 コマンド プロンプトの構文については、「 [コマンド プロンプトから SQL Server 2016 をインストール](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)」を参照してください。  
  
### <a name="to-uninstall-a-ssnoversion-failover-cluster-instance"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスター インスタンスをアンインストールには
  
1.  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] フェールオーバー クラスターをアンインストールするには、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] セットアップによって提供されるノードの削除機能を使用して、各ノードを個別に削除します。 詳細については、[Always On フェールオーバー クラスターでのノードの追加または削除 &#40;セットアップ&#41;](../../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)に関するページを参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server セットアップ ログ ファイルの表示と読み取り](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
