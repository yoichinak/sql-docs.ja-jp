---
title: SSMA プロジェクトの操作 (OracleToSQL) |Microsoft Docs
description: 設定と接続情報と共に、移行および SQL Server する Oracle データベースのメタデータを含む SSMA プロジェクトを作成する方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Customizing Project Settings
ms.assetid: ee5d94c0-c7a6-4779-bd32-729bdaf61e1b
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 1e8b211dc0a73ac6fd84515ce0153faa5ed7ae73
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038876"
---
# <a name="working-with-ssma-projects-oracletosql"></a>SSMA プロジェクトの操作 (OracleToSQL)
Oracle データベースをに移行するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、最初に SSMA プロジェクトを作成します。 プロジェクトは、次の情報を含むファイルです。  
  
-   移行先の Oracle データベースに関するメタデータ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移行されたオブジェクトとデータを受信するの対象インスタンスに関するメタデータ。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続情報。  
  
-   プロジェクト設定。  
  
プロジェクトを開くと、Oracle とから切断され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これにより、オフラインで作業できるようになります。 への再接続の詳細について [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、「 [SQL Server &#40;OracleToSQL&#41;への接続 ](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)」を参照してください。  
  
## <a name="reviewing-default-project-settings"></a>既定のプロジェクト設定の確認  
SSMA には、データベースオブジェクトの変換と読み込み、データの移行、SSMA と Oracle およびの同期を行うための設定がいくつか含まれてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 既定の設定は、多くのユーザーに適しています。 ただし、新しい SSMA プロジェクトを作成する前に、設定を確認する必要があります。 必要に応じて、すべての新しいプロジェクトで使用される既定の設定を変更できます。  
  
**既定のプロジェクト設定を確認するには**  
  
1.  [ **ツール** ] メニューの [ **既定のプロジェクト設定**] をクリックします。  
  
2.  表示または変更が必要な設定について、[ **移行ターゲットバージョン** ] ドロップダウンでプロジェクトの種類を選択し、[ **全般** ] タブをクリックします。  
  
3.  左側のウィンドウで、[ **変換**] をクリックします。  
  
4.  右側のウィンドウで、必要に応じて設定を確認し、変更します。 これらの設定の詳細については、「 [プロジェクトの設定 &#40;変換&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-conversion-oracletosql.md)」を参照してください。  
  
5.  移行、同期、システムオブジェクトの読み込み、GUI、種類マッピングの各ページについて、手順1-3 を繰り返します。  
  
    -   移行設定の詳細については、「 [プロジェクトの設定 &#40;migration&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-migration-oracletosql.md)」を参照してください。  
  
    -   システムオブジェクトの設定の詳細については、「 [OracleToSQL&#41;&#41; &#40;のシステムオブジェクトの読み込み&#40;プロジェクトの設定 ](../../ssma/oracle/project-settings-loading-system-objects-oracletosql.md)」を参照してください。  
  
    -   との同期の設定の詳細について [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、「 [プロジェクト設定&#40;同期&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)」を参照してください。  
  
    -   GUI 設定の詳細については、「 [プロジェクト設定 &#40;gui&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-gui-oracletosql.md)」を参照してください。  
  
    -   データ型のマッピング設定の詳細については、「 [プロジェクトの設定 &#40;Type mapping&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)」を参照してください。  
  
## <a name="creating-new-projects"></a>新しいプロジェクトの作成  
Oracle データベースからにデータを移行するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、最初にプロジェクトを作成する必要があります。  
  
**プロジェクトを作成するには**  
  
1.  **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。  
  
    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2.  [ **名前** ] ボックスに、プロジェクトの名前を入力します。  
  
3.  [ **場所** ] ボックスで、プロジェクトのフォルダーを入力または選択し、[ **OK]** をクリックします。  
  
4.  [ **移行先** ] ドロップダウンで、移行に使用するターゲットのバージョンを選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 次の方法を使用できます。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL データベース  
  
## <a name="customizing-project-settings"></a>プロジェクト設定のカスタマイズ  
すべての新しい SSMA プロジェクトに適用される既定のプロジェクト設定を定義するだけでなく、各プロジェクトの設定をカスタマイズすることもできます。 詳細については、「 [プロジェクトオプションの設定 &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md)」を参照してください。  
  
ソースデータベースとターゲットデータベース間のデータ型マッピングをカスタマイズする場合は、プロジェクト、データベース、またはオブジェクトレベルでマッピングを定義できます。 詳細については、「 [OracleToSQL&#41;&#40;SQL Server Oracle データ型のマッピング ](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md)」を参照してください。  
  
## <a name="saving-projects"></a>プロジェクトの保存  
プロジェクトを保存すると、SSMA によってプロジェクトの設定が保持され、必要に応じてデータベースのメタデータをプロジェクトファイルに保存できます。  
  
**プロジェクトを保存するには**  
  
-   [ **ファイル** ] メニューの [ **プロジェクトの保存**] をクリックします。  
  
    プロジェクト内のスキーマが変更された場合、または変換されていない場合は、SSMA によってメタデータの読み込みと保存を求めるメッセージが表示されます。 メタデータを読み込んで保存すると、オフラインで作業できるようになります。 また、テクニカルサポート担当者など、すべてのプロジェクトファイルを他のユーザーに送信することもできます。 メタデータを保存するかどうかを確認するメッセージが表示されたら、次の手順を実行します。  
  
    1.  [ **メタデータが存在しません**] の状態を示す各スキーマについて、データベース名の横にあるチェックボックスをオンにします。  
  
        メタデータの保存には数分かかる場合があります。 メタデータをまだ保存しない場合は、チェックボックスをオンにしないでください。  
  
    2.  **[保存]** ボタンをクリックします。  
  
        SSMA は Oracle スキーマを解析し、メタデータをプロジェクトファイルに保存します。  
  
## <a name="opening-projects"></a>プロジェクトを開く  
プロジェクトを開くと、Oracle およびからの接続が解除され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これにより、オフラインで作業できるようになります。 メタデータを更新するには、データベースオブジェクトをに読み込み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 データを移行するには、Oracle とに再接続する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
**プロジェクトを開くには**  
  
1.  次の手順のいずれかを使用します。  
  
    -   [ **ファイル** ] メニューの [ **最近使ったプロジェクト**] をポイントし、開くプロジェクトをクリックします。  
  
    -   [ **ファイル** ] メニューの [ **プロジェクトを開く**] を選択し、o2ssproj プロジェクトファイルを見つけて、ファイルを選択し、[ **開く**] をクリックします。  
  
2.  Oracle に再接続するには、[ **ファイル** ] メニューの [ **Oracle に再接続**] をクリックします。  
  
3.  に再接続するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、[ **ファイル** ] メニューの [ **再接続**] をクリックして SQL Server します。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順では、 [Oracle Database (OracleToSQL) に接続](./connecting-to-oracle-database-oracletosql.md)します。  
  
## <a name="see-also"></a>参照  
[Oracle データベースの SQL Server &#40;OracleToSQL&#41;への移行 ](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
[Oracle Database &#40;OracleToSQL&#41;に接続しています ](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)  
[SQL Server &#40;OracleToSQL&#41;に接続しています ](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
