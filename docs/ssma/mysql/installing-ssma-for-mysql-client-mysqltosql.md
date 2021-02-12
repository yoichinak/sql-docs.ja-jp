---
title: SSMA for MySQL クライアントのインストール (MySQLToSQL) |Microsoft Docs
description: SQL Server Migration Assistant (SSMA) for MySQL クライアントのインストールの前提条件と、のインストール方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e2eaa9daf9128b43ac061cad66e7e993882e43d7
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100070147"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>SSMA for MySQL クライアントのインストール (MySQLToSQL)

SSMA for MySQL クライアントは、次のタスクを実行するプログラムファイルで構成されています。

- MySQL データベースに接続します。  
- またはのインスタンスに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] します。
- MySQL データベースオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトまたはオブジェクトに変換し [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。
- オブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはに読み込み [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。
- データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] またはに移行 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] します。

このトピックでは、SSMA for MySQL クライアントをインストールするための前提条件と手順について説明します。

## <a name="prerequisites"></a>前提条件

SSMA for MySQL は、MySQL 4.1 以降のバージョン、2012以降のすべてのエディション、およびを使用するように設計されてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ます。

SSMA をインストールする前に、コンピューターが次の要件を満たしていることを確認してください。

- Windows 7 以降のバージョン、または Windows Server 2008 以降のバージョン。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows インストーラー3.1 以降のバージョン。
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] バージョン4.7.2 以降のバージョン。 これは [.NET Framework デベロッパーセンター](https://go.microsoft.com/fwlink/?LinkId=48882)から入手できます。
- MySQL ODBC 5.1 ドライバーと、移行する MySQL データベースへの接続。 Mysql は、MySQL Web サイトからインストールできます。 接続の詳細については、「 [MySQL への接続 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)」を参照してください。
- にアクセスし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースオブジェクトとデータを移行するのターゲットインスタンスをホストするコンピューターに対して十分なアクセス許可を付与します。 詳細については、「 [SQL Server &#40;MySQLToSQL&#41;への接続 ](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)」を参照してください。
- プロジェクトの場合は [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 、 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] データベースオブジェクトとデータを移行するのインスタンスに対する十分なアクセス許可とアクセス許可が必要です。 詳細については、「 [Azure SQL Database &#40;MySQLToSQL&#41;への接続 ](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)」を参照してください。
- 4 GB の RAM を推奨します。

## <a name="installing-ssma-for-mysql-client"></a>MySQL クライアントへの SSMA のインストール

SSMA は Web からダウンロードできます。 最新バージョンをダウンロードするには、 [SQL Server Migration Assistant のダウンロードページ](https://aka.ms/ssmaformysql)を参照してください。

SSMA クライアントをインストールするには:

1. **SSMAforMySQL_ *n*.msi** をダブルクリックします。ここで、 *n* はビルド番号です。
2. **[ようこそ]** ページで **[次へ]** をクリックします。

   前提条件がインストールされていない場合は、必要なコンポーネントを最初にインストールする必要があることを示すメッセージが表示されます。 インストールプログラムを再実行する前に、すべての前提条件がインストールされていることを確認してください。

3. End-User 使用許諾契約書をお読みください。 同意する場合は、 **[同意する] を選択し**、[ **次へ**] をクリックします。
4. [ **セットアップの種類の選択** ] ページで、[ **標準**] をクリックします。
5. [ **インストールの準備完了** ] ページで、ツールが開始されるたびにテレメトリと自動更新のチェックを有効または無効にすることができます。 **[インストール]** をクリックしてインストールを開始します。

> [!IMPORTANT]
> 新しいバージョンをインストールする前に、SSMA for MySQL の以前のバージョンをすべてアンインストールしてください。

既定のインストール場所は `C:\Program Files\Microsoft SQL Server Migration Assistant for MySQL` です。

## <a name="see-also"></a>関連項目

- [MySQL データベースの SQL Server Azure SQL Database への移行](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
