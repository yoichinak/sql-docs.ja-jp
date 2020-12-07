---
description: プロジェクトの作成と管理 (管理用 Sql)
title: プロジェクトの作成と管理 (管理用 Sql) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- creating projects
- new projects
- opening projects
- projects
- projects, creating and managing
- saving metadata
- saving projects
ms.assetid: f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: ee6cf3bea905b169503851efe375fd614c4589e9
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988198"
---
# <a name="creating-and-managing-projects-accesstosql"></a>プロジェクトの作成と管理 (管理用 Sql)
Access データベースをまたは SQL Azure に移行するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、まず SSMA プロジェクトを作成する必要があります。 このプロジェクトは、移行先または SQL Azure のアクセスデータベースに関するメタデータ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移行されたオブジェクトとデータ、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 接続情報、およびプロジェクト設定を受け取る SQL Azure の対象インスタンスに関するメタデータを含むファイルです。  
  
## <a name="reviewing-default-project-settings"></a>既定のプロジェクト設定の確認  
SSMA には、データベースオブジェクトを変換および同期したり、データを変換したりするためのオプションがいくつか用意されています。 これらのオプションの既定の設定は、多くのユーザーに適しています。 ただし、新しい SSMA プロジェクトを作成する前に、オプションを確認し、必要に応じて、すべての新しいプロジェクトで使用される既定の設定を変更する必要があります。  
  
**既定のプロジェクト設定を確認するには**  
  
1.  [ **ツール** ] メニューの [ **既定のプロジェクト設定**] をクリックします。  
  
2.  設定を表示または変更する [ **移行ターゲットバージョン** ] ドロップダウンでプロジェクトの種類を選択し、[ **全般** ] タブをクリックします。  
  
3.  左側のウィンドウで、[ **変換**] をクリックします。  
  
4.  右ペインで、オプションを確認します。 これらのオプションの詳細については、「 [プロジェクトの設定 (変換)](./project-settings-conversion-accesstosql.md)」を参照してください。  
  
5.  必要に応じてオプションを変更します。  
  
6.  **移行**、 **GUI**、および**種類のマッピング**ページに対して、前の手順を繰り返します。  
  
    -   移行オプションの詳細については、「 [プロジェクトの設定 (移行)](./project-settings-migration-accesstosql.md)」を参照してください。  
  
    -   ユーザーインターフェイスオプションの詳細については、「 [プロジェクトの設定 (GUI)](../sybase/project-settings-gui-sybasetosql.md)」を参照してください。  
  
    -   データ型マッピングの設定の詳細については、「 [プロジェクトの設定 (型のマッピング)](./project-settings-type-mapping-accesstosql.md)」を参照してください。  
  
    -   SQL Azure 設定の詳細については、「 [プロジェクトの設定 (SQL Azure)](./project-settings-azure-sql-db-accesstosql.md)」を参照してください。  
  
**メモ** SQL Azure 設定は、プロジェクトの作成中に [SQL Azure に移行] を選択した場合にのみ使用できます。  
  
## <a name="creating-new-projects"></a>新しいプロジェクトの作成  
SSMA は、既定のプロジェクトを読み込まずに起動します。 Access データベースからまたは SQL Azure にデータを移行するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、プロジェクトを作成する必要があります。  
  
**新しいプロジェクトを作成するには**  
  
1.  **[ファイル]** メニューの **[新しいプロジェクト]** を選択します。  
  
    **[新しいプロジェクト]** ダイアログ ボックスが表示されます。  
  
2.  [ **名前** ] ボックスに、プロジェクトの名前を入力します。  
  
3.  [ **場所** ] ボックスで、プロジェクトのフォルダーを入力または選択します。  
  
4.  [移行先] ドロップダウンで、SQL Server 2005/SQL Server 2008/SQL Server 2012/SQL Server 2014/SQL Server 2016/Azure SQL Database のいずれかを選択し、[ **OK**] をクリックします。  
  
SSMA により、プロジェクトファイルが作成されます。 これで、 [1 つ以上の Access データベースを追加](adding-and-removing-access-database-files-accesstosql.md)する次の手順を実行できます。  
  
## <a name="customizing-project-settings"></a>プロジェクト設定のカスタマイズ  
すべての新しい SSMA プロジェクトに適用される既定のプロジェクト設定を定義するだけでなく、各プロジェクトの設定をカスタマイズすることもできます。 詳細については、「 [変換オプションと移行オプションの設定](setting-conversion-and-migration-options-accesstosql.md)」を参照してください。  
  
ソースデータベースとターゲットデータベース間のデータ型マッピングをカスタマイズする場合は、プロジェクト、データベース、またはオブジェクトレベルでマッピングを定義できます。 型マッピングの詳細については、「 [ソースとターゲットのデータ型のマッピング](mapping-source-and-target-data-types-accesstosql.md)」を参照してください。  
  
## <a name="saving-projects"></a>プロジェクトの保存  
プロジェクトを保存すると、SSMA によってプロジェクトの設定が保持され、必要に応じてデータベースのメタデータをプロジェクトファイルに保存できます。  
  
**プロジェクトを保存するには**  
  
-   [ **ファイル** ] メニューの [ **プロジェクトの保存**] をクリックします。  
  
    プロジェクト内のデータベースが変更された場合、または変換されていない場合は、SSMA によってメタデータをプロジェクトに保存するように求められます。 メタデータを保存すると、オフラインで作業できるようになります。 また、テクニカルサポート担当者を含む、他のユーザーに完全なプロジェクトファイルを送信することもできます。 メタデータを保存するかどうかを確認するメッセージが表示されたら、次の手順を実行します。  
  
    1.  [ **メタデータが存在しません**] の状態を示すデータベースごとに、データベース名の横にあるチェックボックスをオンにします。  
  
        メタデータの保存には数分かかる場合があります。 この時点でメタデータを保存しない場合は、チェックボックスをオンにしないでください。  
  
    2.  **[保存]** をクリックします。  
  
        SSMA は、アクセススキーマを解析し、メタデータをプロジェクトファイルに保存します。  
  
## <a name="opening-projects"></a>プロジェクトを開く  
プロジェクトを開くと、そのプロジェクトはまたは SQL Azure から切断され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 これにより、オフラインで作業できるようになります。 メタデータを更新するには、データベースオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure に読み込みます。 データを移行するには、または SQL Azure に再接続する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
**プロジェクトを開くには**  
  
1.  次の手順のいずれかを使用します。  
  
    -   [ **ファイル** ] メニューの [ **最近使ったプロジェクト**] をポイントし、開くプロジェクトを選択します。  
  
    -   [ **ファイル** ] メニューの [ **プロジェクトを開く**] を選択し、a2ssproj プロジェクトファイルを見つけて、ファイルを選択し、[ **開く**] をクリックします。  
  
2.  に再接続するには、[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **ファイル** ] メニューの [ **SQL Server に再接続**] を選択します。  
  
3.  SQL Azure に再接続するには、[**ファイル**] メニューの [ **SQL Azure に再接続**] を選択します。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順では、 [Access データベースを1つ以上追加](adding-and-removing-access-database-files-accesstosql.md)します。  
  
## <a name="see-also"></a>参照  
[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Access データベースファイルの追加と削除](adding-and-removing-access-database-files-accesstosql.md)  
