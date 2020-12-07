---
description: SSMA プロジェクトでの作業 (MySQLToSQL)
title: SSMA プロジェクトの操作 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Working with SSMA projects, create new project
- Working with SSMA projects, customize settings
- Working with SSMA projects, Open project
- Working with SSMA projects, Save project
ms.assetid: 9e4394e9-f177-41d9-839e-5d53a9c9b840
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3da213467ad6513d4c25e6888bd095e80746cba7
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038275"
---
# <a name="working-with-ssma-projects-mysqltosql"></a>SSMA プロジェクトでの作業 (MySQLToSQL)
MySQL データベースを SQL Server または SQL Azure に移行するには、まず SSMA プロジェクトを作成する必要があります。 プロジェクトは、次の情報を含むファイルです。  
  
-   SQL Server または SQL Azure に移行する MySQL データベースに関するメタデータ。  
  
-   移行されたオブジェクトとデータを受信する SQL Server または SQL Azure の対象インスタンスに関するメタデータ。  
  
-   接続情報を SQL Server または SQL Azure します。  
  
-   プロジェクト設定。  
  
プロジェクトを開くと、MySQL および SQL Server または SQL Azure から切断されます。 これにより、オフラインで作業できるようになります。 SQL Server に再接続する方法の詳細については、「 [SQL Server &#40;MySQLToSQL への接続](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)」を参照してください&#41;  
  
## <a name="reviewing-default-project-settings"></a>既定のプロジェクト設定の確認  
SSMA には、データベースの変換と読み込み、データの移行、SSMA と MySQL および SQL Server または SQL Azure の同期を行うための設定がいくつか含まれています。 既定の設定は、多くのユーザーに適しています。 ただし、新しい SSMA プロジェクトを作成する前に、設定を確認する必要があります。 必要に応じて、すべての新しいプロジェクトで使用される既定の設定を変更できます。  
  
##### <a name="to-review-default-project-settings"></a>既定のプロジェクト設定を確認するには  
  
1.  [**ツール**] メニューの [**既定のプロジェクト設定**] をクリックします。  
  
2.  設定を表示または変更する [ **移行ターゲットバージョン** ] ドロップダウンでプロジェクトの種類を選択し、[ **全般** ] タブをクリックします。  
  
3.  左側のウィンドウで、[ **変換**] をクリックします。  
  
4.  右側のウィンドウで、必要に応じて設定を確認し、変更します。 これらの設定の詳細については、「 [プロジェクトの設定 &#40;変換&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md) 」を参照してください。  
  
5.  移行、同期、SQL Azure、GUI、および種類のマッピングページについて、手順1-3 を繰り返します。  
  
-   移行設定の詳細については、「 [プロジェクトの設定 &#40;migration&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-migration-mysqltosql.md)」を参照してください。  
  
-   SQL Server に同期するための設定の詳細については、「 [プロジェクト設定 &#40;同期&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md)」を参照してください。  
  
-   GUI 設定の詳細については、「 [プロジェクトの設定 (gui) (SSMA Common)](../sybase/project-settings-gui-sybasetosql.md)」を参照してください。  
  
-   データ型のマッピング設定の詳細については、「 [プロジェクトの設定 &#40;Type mapping&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)」を参照してください。  
  
-   SQL Azure 設定の詳細については、「 [プロジェクトの設定 &#40;Azure SQL Database&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-azure-sql-db-mysqltosql.md)」を参照してください。  
  
> [!NOTE]  
> SQL Azure 設定は、プロジェクトの作成中に [ **SQL Azure に移行** ] を選択した場合にのみ表示されます。  
  
## <a name="creating-new-projects"></a>新しいプロジェクトの作成  
MySQL データベースから SQL Server または SQL Azure にデータを移行するには、プロジェクトを作成する必要があります。  
  
##### <a name="to-create-a-new-project"></a>新しいプロジェクトを作成するには  
  
1.  [**ファイル**] メニューの [**新しいプロジェクト**] をクリックします。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。 **[ファイル]** メニューの **[新しいプロジェクト]** を選択します。 **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2.  [ **名前** ] ボックスに、プロジェクトの名前を入力します。  
  
3.  [ **場所** ] ボックスで、プロジェクトのフォルダーを入力または選択します。  
  
4.  [ **移行先** ] ドロップダウンで、移行に使用するターゲットのバージョンを選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 次の方法を使用できます。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   Azure SQL データベース  
  
[ **OK** ] をクリックします。  
  
SSMA により、プロジェクトファイルが作成されます。  
  
## <a name="customizing-project-settings"></a>プロジェクト設定のカスタマイズ  
すべての新しい SSMA プロジェクトに適用される既定のプロジェクト設定を定義するだけでなく、各プロジェクトの設定をカスタマイズすることもできます。 詳細については、「 [プロジェクトオプションの設定 &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)」を参照してください。  
  
ソースデータベースとターゲットデータベース間のデータ型マッピングをカスタマイズする場合は、プロジェクト、データベース、またはオブジェクトレベルでマッピングを定義できます。 詳細については、「 [MySQL と SQL Server のデータ型のマッピング &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)」を参照してください。  
  
## <a name="saving-projects"></a>プロジェクトの保存  
[プロジェクトの保存] 機能を使用すると、ユーザーは基本的にプロジェクトの設定と、必要に応じてデータベースのメタデータを SSMA プロジェクトファイルに保存できます。  
  
##### <a name="to-save-a-project"></a>プロジェクトを保存するには  
  
-   [ **ファイル** ] メニューの [プロジェクトの **保存** ] をクリックします。  
  
プロジェクト内のデータベースが変更された場合、または変換されていない場合は、SSMA によってメタデータの読み込みと保存を求めるメッセージが表示されます。 メタデータを読み込んで保存すると、オフラインで作業できるようになります。 また、テクニカルサポート担当者など、すべてのプロジェクトファイルを他のユーザーに送信することもできます。 メタデータを保存するかどうかを確認するメッセージが表示されたら、次の手順を実行します。  
  
1.  [ **メタデータが存在しません**] の状態を示すデータベースごとに、データベース名の横にあるチェックボックスをオンにします。 メタデータの保存には数分かかる場合があります。 この時点でメタデータを保存しない場合は、チェックボックスをオンにしないでください。  
  
2.  **[保存]** をクリックします。  
  
SSMA は MySQL スキーマを解析し、メタデータをプロジェクトファイルに保存します。  
  
## <a name="opening-projects"></a>プロジェクトを開く  
プロジェクトを開くと、そのプロジェクトは MySQL および SQL Server または SQL Azure から切断されます。 これにより、オフラインで作業できるようになります。 メタデータを更新するには、データベースオブジェクトを SQL Server または SQL Azure に読み込みます。 データを移行するには、SQL Server または SQL Azure に再接続する必要があります。  
  
##### <a name="to-open-a-project"></a>プロジェクトを開くには  
  
1.  次の手順のいずれかを使用します。  
  
    1.  [ **ファイル** ] メニューの [ **最近使ったプロジェクト**] をポイントします。  
  
    2.  開くプロジェクトを選択します。  
  
    3.  [ **ファイル** ] メニューの [ **プロジェクトを開く**] を選択し、m2ssproj プロジェクトファイルを見つけて、ファイルを選択し、[ **開く**] をクリックします。  
  
2.  MySQL に再接続するには、[ **ファイル** ] メニューの [ **Mysql に再接続**] を選択します。  
  
3.  SQL Server に再接続するには、[ **ファイル** ] メニューの [ **SQL Server に再接続**] を選択します。  
  
4.  SQL Azure に再接続するには、[**ファイル**] メニューの [ **SQL Azure に再接続**] を選択します。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次のステップは、 [MySQL &#40;MySQLToSQL への接続&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
## <a name="see-also"></a>参照  
[MySQL &#40;MySQLToSQL&#41;に接続しています ](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
[MySQL データベースを SQL Server Azure SQL Database &#40;MySQLToSql&#41;に移行する ](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[SQL Server &#40;MySQLToSQL&#41;に接続しています ](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
[Azure SQL Database &#40;MySQLToSQL&#41;に接続しています ](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
