---
description: SSMA プロジェクトの使用 (DB2ToSQL)
title: SSMA プロジェクトの操作 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 07abef8a-28e8-4a66-927c-c9a5b8c938ef
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: f56387f8081ce14c68d355327c2829bf6e33c8cc
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869480"
---
# <a name="working-with-ssma-projects-db2tosql"></a>SSMA プロジェクトの使用 (DB2ToSQL)
DB2 データベースをに移行するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、最初に SSMA プロジェクトを作成します。 プロジェクトは、次の情報を含むファイルです。  
  
-   移行先の DB2 データベースに関するメタデータ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移行されたオブジェクトとデータを受信するの対象インスタンスに関するメタデータ。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続情報。  
  
-   プロジェクト設定。  
  
プロジェクトを開くと、そのプロジェクトは DB2 およびから切断され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これにより、オフラインで作業できるようになります。 への再接続の詳細について [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、「 [SQL Server &#40;DB2ToSQL&#41;への接続 ](../../ssma/db2/connecting-to-sql-server-db2tosql.md)」を参照してください。  
  
## <a name="reviewing-default-project-settings"></a>既定のプロジェクト設定の確認  
SSMA には、データベースオブジェクトの変換と読み込み、データの移行、SSMA と DB2 およびの同期を行うための設定がいくつか含まれてい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 既定の設定は、多くのユーザーに適しています。 ただし、新しい SSMA プロジェクトを作成する前に、設定を確認する必要があります。 必要に応じて、すべての新しいプロジェクトで使用される既定の設定を変更できます。  
  
**既定のプロジェクト設定を確認するには**  
  
1.  [ **ツール** ] メニューの [ **既定のプロジェクト設定**] をクリックします。  
  
2.  表示または変更が必要な設定について、[ **移行ターゲットバージョン** ] ドロップダウンでプロジェクトの種類を選択し、[ **全般** ] タブをクリックします。  
  
3.  左側のウィンドウで、[ **変換**] をクリックします。  
  
4.  右側のウィンドウで、必要に応じて設定を確認し、変更します。 これらの設定の詳細については、「 [プロジェクトの設定 &#40;変換&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-conversion-db2tosql.md)」を参照してください。  
  
5.  移行、同期、システムオブジェクトの読み込み、GUI、種類マッピングの各ページについて、手順1-3 を繰り返します。  
  
    -   移行設定の詳細については、「 [プロジェクトの設定 &#40;migration&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-migration-db2tosql.md)」を参照してください。  
  
    -   システムオブジェクトの設定の詳細については、「 [DB2ToSQL&#41;&#41; &#40;のシステムオブジェクトの読み込み&#40;プロジェクトの設定 ](../../ssma/db2/project-settings-loading-system-objects-db2tosql.md)」を参照してください。  
  
    -   との同期の設定の詳細について [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、「 [プロジェクト設定&#40;同期&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-synchronization-db2tosql.md)」を参照してください。  
  
    -   GUI 設定の詳細については、「 [プロジェクト設定 &#40;gui&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-gui-db2tosql.md)」を参照してください。  
  
    -   データ型のマッピング設定の詳細については、「 [プロジェクトの設定 &#40;Type mapping&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)」を参照してください。  
  
## <a name="creating-new-projects"></a>新しいプロジェクトの作成  
DB2 データベースからにデータを移行するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、最初にプロジェクトを作成する必要があります。  
  
**プロジェクトを作成するには**  
  
1.  **[ファイル]** メニューの **[新しいプロジェクト]** をクリックします。  
  
    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2.  [ **名前** ] ボックスに、プロジェクトの名前を入力します。  
  
3.  [ **場所** ] ボックスで、プロジェクトのフォルダーを入力または選択し、[ **OK]** をクリックします。  
  
4.  [ **移行先** ] ドロップダウンで、移行に使用するターゲットのバージョンを選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 次の方法を使用できます。  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016  
  
    -   Azure SQL データベース  
  
## <a name="customizing-project-settings"></a>プロジェクト設定のカスタマイズ  
すべての新しい SSMA プロジェクトに適用される既定のプロジェクト設定を定義するだけでなく、各プロジェクトの設定をカスタマイズすることもできます。 詳細については、「 [プロジェクトオプション &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md) 」および関連するセクションを参照してください。  
  
ソースデータベースとターゲットデータベース間のデータ型マッピングをカスタマイズする場合は、プロジェクト、データベース、またはオブジェクトレベルでマッピングを定義できます。 詳細については、「 [MAPPING DB2 and SQL Server Data Types &#40;DB2ToSQL&#41;](../../ssma/db2/mapping-db2-and-sql-server-data-types-db2tosql.md)」を参照してください。  
  
## <a name="saving-projects"></a>プロジェクトの保存  
プロジェクトを保存すると、SSMA によってプロジェクトの設定が保持され、必要に応じてデータベースのメタデータをプロジェクトファイルに保存できます。  
  
**プロジェクトを保存するには**  
  
-   [ **ファイル** ] メニューの [ **プロジェクトの保存**] をクリックします。  
  
    プロジェクト内のスキーマが変更された場合、または変換されていない場合は、SSMA によってメタデータの読み込みと保存を求めるメッセージが表示されます。 メタデータを読み込んで保存すると、オフラインで作業できるようになります。 また、テクニカルサポート担当者など、すべてのプロジェクトファイルを他のユーザーに送信することもできます。 メタデータを保存するかどうかを確認するメッセージが表示されたら、次の手順を実行します。  
  
    1.  [ **メタデータが存在しません**] の状態を示す各スキーマについて、データベース名の横にあるチェックボックスをオンにします。  
  
        メタデータの保存には数分かかる場合があります。 メタデータをまだ保存しない場合は、チェックボックスをオンにしないでください。  
  
    2.  **[保存]** ボタンをクリックします。  
  
        SSMA は DB2 スキーマを解析し、メタデータをプロジェクトファイルに保存します。  
  
## <a name="opening-projects"></a>プロジェクトを開く  
プロジェクトを開くと、そのプロジェクトは DB2 およびから切断され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これにより、オフラインで作業できるようになります。 メタデータを更新するには、データベースオブジェクトをに読み込み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 データを移行するには、DB2 およびに再接続する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
**プロジェクトを開くには**  
  
1.  次の手順のいずれかを使用します。  
  
    -   [ **ファイル** ] メニューの [ **最近使ったプロジェクト**] をポイントし、開くプロジェクトをクリックします。  
  
    -   [ **ファイル** ] メニューの [ **プロジェクトを開く**] を選択し、o2ssproj プロジェクトファイルを見つけて、ファイルを選択し、[ **開く**] をクリックします。  
  
2.  DB2 に再接続するには、[ **ファイル** ] メニューの [ **Db2 への再接続**] をクリックします。  
  
3.  に再接続するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、[ **ファイル** ] メニューの [ **再接続**] をクリックして SQL Server します。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順は、 [DB2 データベースに接続](./connecting-to-db2-database-db2tosql.md)することです。  
  
## <a name="see-also"></a>参照  
[DB2 データベースを SQL Server &#40;DB2ToSQL&#41;に移行する ](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
[DB2 データベースへの接続 &#40;DB2ToSQL&#41;](../../ssma/db2/connecting-to-db2-database-db2tosql.md)  
[SQL Server &#40;DB2ToSQL&#41;に接続しています ](../../ssma/db2/connecting-to-sql-server-db2tosql.md)  
