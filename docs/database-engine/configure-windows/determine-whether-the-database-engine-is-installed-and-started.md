---
title: データベース エンジンがインストールされ開始されているかどうかの確認 | Microsoft Docs
description: データベース エンジンがインストールされ開始されているかどうかを確認する方法について説明します。 SQL Server 構成マネージャーを使用して、インストールされているコンポーネントを確認する方法について説明します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, determining if installed
- verifying Database Engine installation
- viewing Database Engine installation
- installed Database Engine verification [SQL Server]
ms.assetid: babb02e4-3521-4b75-b5df-e09205594375
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 03aa96f16ee200846dae726851c51a1dc1d04e80
ms.sourcegitcommit: 2f3f5920e0b7a84135c6553db6388faf8e0abe67
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98783006"
---
# <a name="determine-whether-the-database-engine-is-installed-and-started"></a>データベース エンジンがインストールされ開始されているかどうかの確認
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインストールが成功すると、ファイルがファイル システムにインストールされ、レジストリのエントリが作成されて、ツールがいくつかインストールされます。 このトピックでは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 構成マネージャーを使用して、 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がインストールされて起動されているかどうかを確認する方法について説明します。  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> SQL Server 構成マネージャーの使用  
  
#### <a name="how-to-view-and-start-the-database-engine-by-using-sql-server-configuration-manager"></a>SQL Server 構成マネージャーを使用してデータベース エンジンを表示および開始する方法  
  
1.  **[スタート]** ボタンをクリックし、 **[すべてのプログラム]** 、 **[Microsoft SQL Server]** 、 **[構成ツール]** の順にポイントし、 **[SQL Server 構成マネージャー]** をクリックします。  
  
     **[スタート]** メニューにこれらのエントリがない場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が正しくインストールされていません。 セットアップを実行して、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]をインストールします。  
  
2.  **[SQL Server 構成マネージャー]** の左側のペインで、 **[SQL Server のサービス]** をクリックします。 右側のペインには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に関連するサービスがいくつか表示されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] がインストールされている場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスは **[SQL Server (MSSQLSERVER)]** と表示されるか (これが既定のインスタンスの場合)、 **[SQL Server (** \<*instance_name*> **)]** と表示されます ([!INCLUDE[ssDE](../../includes/ssde-md.md)] が名前付きインスタンスとしてインストールされている場合)。 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] はインスタンス名が変更されない限り、 **SQLEXPRESS** という名前の名前付きインスタンスとしてインストールされます。 緑の三角形のアイコンは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が実行中であることを示します。 赤い四角形のアイコンは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] が停止していることを示します。  
  
3.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]を開始するには、右側のペインで、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]を右クリックして、 **[開始]** をクリックします。  
  
> [!NOTE]  
>  ユーザーは、セットアップ時に、プログラム ファイルとデータベース ファイルをインストールする場所を選択できます。 ユーザーが既定の場所をそのまま使用すると、ファイルは [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)] および C:\Program Files\Microsoft SQL Server\MSSQL.*x*( *x* は番号) にインストールされます。  
  
  
