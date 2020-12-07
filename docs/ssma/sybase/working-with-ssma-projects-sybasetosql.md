---
description: SSMA プロジェクトでの作業 (SybaseToSQL)
title: SSMA プロジェクトの使用 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 11091d95-c488-48c3-891a-743cac94ac93
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: a1a73e1dbc1c494080427ae5dfd686dd3c18abc1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497634"
---
# <a name="working-with-ssma-projects-sybasetosql"></a>SSMA プロジェクトでの作業 (SybaseToSQL)
Sybase Adaptive Server Enterprise (ASE) データベースをまたは SQL Azure に移行するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、まず SSMA プロジェクトを作成します。 このプロジェクトは、移行または SQL Azure する ASE データベースに関するメタデータ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移行されたオブジェクトとデータを受け取るまたは SQL Azure のターゲットインスタンスに関するメタデータ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure 接続情報、およびプロジェクト設定を含むファイルです。  
  
プロジェクトを開くと、そのプロジェクトはまたは SQL Azure から切断され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これにより、オフラインで作業できるようになります。 または SQL Azure に再接続でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については[ ](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)、「  /  [Azure SQL Database &#40;sybasetosql&#41;に接続](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)するための SQL Server &#40;sybasetosql&#41;への接続」を参照してください。  
  
## <a name="reviewing-default-project-settings"></a>既定のプロジェクト設定の確認  
SSMA には、データベースオブジェクトの変換と読み込み、データの移行、SSMA と ASE との同期、または SQL Azure を行うためのオプションがいくつか [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] あります。 これらのオプションの既定の設定は、多くのユーザーに適しています。 ただし、新しい SSMA プロジェクトを作成する前に、オプションを確認し、必要に応じて、すべての新しいプロジェクトで使用される既定値を変更する必要があります。  
  
**既定のプロジェクト設定を確認するには**  
  
1.  [ **ツール** ] メニューの [ **既定のプロジェクト設定**] をクリックします。  
  
2.  表示または変更が必要な設定について、[ **移行ターゲットバージョン** ] ドロップダウンでプロジェクトの種類を選択し、[ **全般** ] タブをクリックします。  
  
3.  左側のウィンドウで、[ **変換**] をクリックします。  
  
4.  右ペインでオプションを確認し、必要に応じてオプションを変更します。 これらのオプションの詳細については、「 [プロジェクトの設定 &#40;変換&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)」を参照してください。  
  
5.  移行、SQL Azure、オブジェクトの読み込み、GUI、種類のマッピングの各ページについて、手順1-3 を繰り返します。  
  
    -   移行オプションの詳細については、「 [プロジェクトの設定 &#40;migration&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-migration-sybasetosql.md)」を参照してください。  
  
    -   オブジェクトをに読み込むオプションの詳細について [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、「 [プロジェクト設定 &#40;同期&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-synchronization-sybasetosql.md)」を参照してください。  
  
    -   GUI オプションの詳細については、「 [プロジェクト設定 &#40;gui&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-gui-sybasetosql.md)」を参照してください。  
  
    -   データ型マッピングの設定の詳細については、[プロジェクトの設定] をクリックして [&#40;Type mapping&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)] をクリックします。  
  
    -   SQL Azure オプションの詳細については、「 [プロジェクトの設定 &#40;Azure SQL Database &#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-azure-sql-db-sybasetosql.md)」を参照してください。  
  
    > [!NOTE]  
    > SQL Azure 設定は、プロジェクトの作成中に [ **SQL Azure に移行** ] を選択した場合にのみ表示されます。  
  
## <a name="creating-new-projects"></a>新しいプロジェクトの作成  
ASE データベースからまたは SQL Azure にデータを移行するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、最初にプロジェクトを作成する必要があります。  
  
**プロジェクトを作成するには**  
  
1.  **[ファイル]** メニューの **[新しいプロジェクト]** を選択します。  
  
    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2.  [ **名前** ] ボックスに、プロジェクトの名前を入力します。  
  
3.  [ **場所** ] ボックスで、プロジェクトのフォルダーを入力または選択します。  
  
4.  [ **移行先** ] ドロップダウンで、移行に使用するターゲットのバージョンを選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 次の方法を使用できます。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL データベース  
  
[ **OK]** をクリックします。  
  
## <a name="customizing-project-settings"></a>プロジェクト設定のカスタマイズ  
すべての新しい SSMA プロジェクトに適用される既定のプロジェクト設定を定義するだけでなく、各プロジェクトの設定をカスタマイズすることもできます。 詳細については、「 [SybaseToSQL&#41;&#40;プロジェクトオプションの設定 ](../../ssma/sybase/setting-project-options-sybasetosql.md)」を参照してください。  
  
ソースデータベースとターゲットデータベース間のデータ型マッピングをカスタマイズする場合は、プロジェクト、データベース、またはオブジェクトレベルでマッピングを定義できます。 型マッピングの詳細については、「 [SQL&#41;の SYBASE ASE と SQL Server のデータ &#40;型のマッピング ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md)」を参照してください。  
  
## <a name="saving-projects"></a>プロジェクトの保存  
プロジェクトを保存すると、SSMA によってプロジェクトの設定が保持され、必要に応じてデータベースのメタデータをプロジェクトファイルに保存できます。  
  
**プロジェクトを保存するには**  
  
-   [ **ファイル** ] メニューの [ **プロジェクトの保存**] をクリックします。  
  
    プロジェクト内のデータベースが変更された場合、または変換されていない場合は、SSMA によってメタデータをプロジェクトに保存するように求められます。 メタデータを保存することで、オフラインで作業したり、テクニカルサポート担当者などのプロジェクトファイルを他のユーザーに送信したりすることができます。 メタデータを保存するかどうかを確認するメッセージが表示されたら、次の手順を実行します。  
  
    1.  [ **メタデータが存在しません**] の状態を示すデータベースごとに、データベース名の横にあるチェックボックスをオンにします。  
  
        メタデータの保存には数分かかる場合があります。 この時点でメタデータを保存しない場合は、チェックボックスをオンにしないでください。  
  
    2.  **[保存]** ボタンをクリックします。  
  
        SSMA は Sybase ASE スキーマを解析し、メタデータをプロジェクトファイルに保存します。  
  
## <a name="opening-projects"></a>プロジェクトを開く  
プロジェクトを開くと、そのプロジェクトは ASE から切断され、または SQL Azure から切断され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これにより、オフラインで作業できるようになります。 メタデータを更新するには、データベースオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure に読み込みます。 データを移行するには、ASE または SQL Azure に再接続する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
**プロジェクトを開くには**  
  
1.  次の手順のいずれかを使用します。  
  
    -   [ **ファイル** ] メニューの [ **最近使ったプロジェクト**] をポイントし、開くプロジェクトを選択します。  
  
    -   [ **ファイル** ] メニューの [ **プロジェクトを開く**] を選択し、s2ssproj プロジェクトファイルを見つけて、ファイルを選択し、[ **開く**] をクリックします。  
  
2.  ASE に再接続するには、[ **ファイル** ] メニューの [ **Sybase に再接続**] を選択します。  
  
3.  再接続 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure するには、[**ファイル**] メニューの [再接続] を選択して**Reconnect to SQL Server**  /  **SQL Azure に再接続**SQL Server ます。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順は、 [SYBASE ASE に接続](connecting-to-sybase-ase-sybasetosql.md)することです。  
  
## <a name="see-also"></a>参照  
[Sybase ASE データベースを SQL Server Azure SQL Database &#40;SybaseToSQL&#41;に移行する ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Sybase ASE &#40;SybaseToSQL&#41;に接続する ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)  
[SQL Server &#40;SybaseToSQL&#41;に接続しています ](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)  
[Azure SQL Database &#40;SybaseToSQL&#41;に接続しています ](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)  
  
