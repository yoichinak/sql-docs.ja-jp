---
title: SQL Server レプリケーションのインストール | Microsoft Docs
description: SQL Server インストール ウィザードまたはコマンド プロンプト ウィンドウを使用してレプリケーション コンポーネントをインストールします。
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server replication]
- command line installations [SQL Server replication]
- installing replication
- replication [SQL Server], installing
- command prompt [SQL Server replication]
ms.assetid: c50ad078-060b-4a8d-ad45-9e31a8d85729
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 55a8a744c384df0536cef1073e05b2fc61a7a1ac
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125928"
---
# <a name="install-sql-server-replication"></a>SQL Server レプリケーションのインストール

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

レプリケーション コンポーネントのインストールは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インストール ウィザードまたはコマンド プロンプトを使用して行うことができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]をインストールする場合、または既存のインスタンスを変更する場合はレプリケーションをインストールします。  
  
レプリケーション コンポーネントのインストール後、レプリケーションを使用する前にサーバーを構成する必要があります。 詳細については、 [オンライン ブックの「](../../relational-databases/replication/configure-distribution.md) ディストリビューションの構成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 」を参照してください。  
  
>[!IMPORTANT]  
>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の既存のインスタンスを変更するときにレプリケーション コンポーネントをインストールする場合は、インストール完了後に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントを停止して再起動する必要があります。 この操作により、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがレプリケーション エージェント サブシステムを認識し、ジョブ ステップからレプリケーション エージェントを呼び出すことができるようになります。  
  
## <a name="installing-replication-by-using-setup"></a>セットアップ プログラムによるレプリケーションのインストール  
**の新しいインスタンスをインストールするときにレプリケーションをインストールするには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
- レプリケーション管理オブジェクト (RMO) を含めてレプリケーション コンポーネントをインストールするには、インストール ウィザードの **[機能の選択]** ページで **[SQL Server レプリケーション]** を選択します。  
  
## <a name="installing-replication-from-the-command-prompt"></a>コマンド プロンプトによるレプリケーションのインストール  
 **の新しいインスタンスをインストールするときにレプリケーションをインストールするには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
- 「[コマンド プロンプトからの SQL Server のインストール](./install-sql-server-from-the-command-prompt.md)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server のインストール](../../database-engine/install-windows/install-sql-server.md)   
 [コマンド プロンプトからの SQL Server のインストール](./install-sql-server-from-the-command-prompt.md)   
 [SQL Server の各エディションでサポートされる機能](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
