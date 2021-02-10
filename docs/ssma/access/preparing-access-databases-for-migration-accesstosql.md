---
title: Access データベースの移行の準備 (アクセス可能な Sql) |Microsoft Docs
description: SQL Server または Azure SQL Database に移行するアクセスデータベースを特定し、それらのデータベースを移行する準備ができていることを確認する方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, versions
- Access databases, when to migrate
- Access databases, workgroup security
- backing up databases
- documenting databases
- files, preparing
- migrating databases, versions
- migrating databases, when to migrate
- versions of Access
- workgroup security
ms.assetid: 9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 7c52b13a2a71afc005f19d1733e8dff435d2a582
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100066587"
---
# <a name="preparing-access-databases-for-migration-accesstosql"></a>移行のための Access データベースの準備 (アクセス可能な Sql)
Access データベースをに移行する前に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、移行するデータベースを決定し、それらのデータベースの移行準備ができていることを確認する必要があります。  
  
## <a name="determining-when-to-migrate-to-sql-server"></a>SQL Server に移行する場合の判断  
Access のデータベースエンジンとして使用される Jet データベースエンジンは、データ管理のための柔軟で使いやすいソリューションです。 ただし、データベースが大きくなり、ミッションクリティカルになるにつれて、多くのユーザーは、パフォーマンス、セキュリティ、または可用性の向上を必要としていることがわかります。 より堅牢なデータプラットフォームを必要とするアプリケーションでは、これらのアプリケーションの基になるデータベースをに移動することを検討してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 移行のタイミングを決定する方法の詳細については、Web サイトの「 [移行情報」ページ](https://go.microsoft.com/fwlink/?LinkId=68571) を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
データベースをに移行した後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] も、リンクテーブルを使用して引き続きアクセスでき [!INCLUDE[msCoName](../../includes/msconame_md.md)] ます。また、と直接やり取りする .NET Framework ベースのコードにアプリケーションを手動で移行することもでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="determining-which-databases-to-migrate"></a>移行するデータベースの決定  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Access の Migration Assistant (SSMA) は、Access データベースを見つけることができます。 その後、これらのデータベースに関するメタデータをにエクスポートでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 メタデータをエクスポートおよび照会する方法の詳細については、「 [アクセスインベントリのエクスポート](exporting-an-access-inventory-accesstosql.md)」を参照してください。  

   > [!NOTE]
   > すべてのアクセス機能と設定がでサポートされているわけではありません。また、に簡単に変換することもでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 データベースの移行を開始する前に、「互換性のない [アクセス機能](incompatible-access-features-accesstosql.md)」を参照してください。
  
## <a name="preparing-for-migration"></a>移行の準備  
への移行のために Access データベースを準備するには、次のガイドラインに従い [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
### <a name="upgrading-older-access-databases"></a>古い Access データベースのアップグレード  
SSMA for Access は、97以降のバージョンへのアクセスをサポートしています。 以前のバージョンの Access のデータベースを使用している場合は、Access 97 以降のバージョンでデータベースを開いて保存します。  
  
### <a name="removing-workgroup-protection"></a>ワークグループの保護の削除  
SSMA では、ワークグループ保護を使用するデータベースを移行することはできません。 Access データベースからワークグループ保護を削除するには、次の手順を実行します。  
  
1.  Access データベースファイルを別の場所にコピーします。  
  
2.  コピーしたデータベースを開きます。  
  
3.  [ **ツール** ] メニューの [ **セキュリティ**] をポイントし、[ **ユーザーとグループのアクセス許可**] を選択します。  
  
4.  [Users] \ ( **ユーザー** \) オプションを選択し、 **管理者** ユーザーを選択して、[ **管理** ] アクセス許可が選択されていることを確認します。  
  
5.  [ **グループ** ] オプションを選択し、[ **Users** ] グループを選択して、[ **管理** ] アクセス許可が選択されていることを確認します。  
  
6.  [ **OK**] をクリックし、[ **ファイル** ] メニューの [ **終了**] をクリックします。  
  
これで、SSMA を使用して、コピーしたデータベースを移行できるようになりました。 スキーマをに読み込んだ後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、でデータベースを手動でセキュリティで保護することができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
### <a name="backing-up-databases"></a>データベースのバックアップ  
Access データベースをに移行する前に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、移行する access データベースと、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アクセスオブジェクトとデータを移行するデータベースの両方をバックアップする必要があります。  
  
Access データベースをバックアップするには、[ **ツール** ] メニューの [ **データベースユーティリティ**] をポイントし、[ **データベースのバックアップ**] を選択します。  
  
データベースをバックアップする方法の詳細については [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンラインブックの「データベースのバックアップと復元」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
### <a name="documenting-databases"></a>データベースのドキュメント化  
また、Access データベースのデータベースオブジェクト、ファイルサイズ、アクセス許可の一覧などのプロパティを文書化することもできます。 Access でこのドキュメントを生成するには、[ **ツール** ] メニューの [ **分析**] をポイントし、[ **文書化**] をクリックします。  
  
## <a name="see-also"></a>関連項目  
[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Access アプリケーションの SQL Server へのリンク](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)
