---
description: SQL Server Azure SQL Database へのアクセスデータの移行 (アクセス許可 SQL)
title: SQL Server Azure SQL Database へのアクセスデータの移行 (アクセス可能な SQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- bulk loading data
- data, loading into SQL Azure
- data, loading into SQL Server
- migrating databases, loading data
- migrating databases, options
- options, migrating data
- SQL Azure, migrating data into
- SQL Server, migrating data into
ms.assetid: f3b18af7-1af0-499d-a00d-a0af94895625
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: cc1cdb31969eb94c29a6c58f974aef92c5cdfc62
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988658"
---
# <a name="migrating-access-data-into-sql-server---azure-sql-database-accesstosql"></a>SQL Server Azure SQL Database へのアクセスデータの移行 (アクセス許可 SQL)
データベースオブジェクトをに正常に作成した後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、アクセスからまたは SQL Azure にデータを移行でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="setting-migration-options"></a>移行オプションの設定  
データをまたは SQL Azure に移行する前に、[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **プロジェクトの設定** ] ダイアログボックスの [プロジェクトの移行] オプションを確認してください。 このダイアログボックスでは、移行バッチサイズ、テーブルロック、制約チェック、挿入トリガーの起動、id と null 値の処理、範囲外の日付の処理方法を設定でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「 [プロジェクトの設定 (移行)](./project-settings-migration-accesstosql.md)」を参照してください。  
  
## <a name="migrating-data"></a>データの移行  
データの移行は、データの行をトランザクションに移動または SQL Azure する一括読み込み操作です [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 各トランザクションで読み込まれる行または SQL Azure される行の数は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] プロジェクトの設定で構成されます。  
  
移行メッセージを表示するには、[出力] ウィンドウが表示されていることを確認します。 表示されていない場合は、[ **表示** ] メニューの [ **出力**] を選択します。  
  
**データを移行するには**  
  
1.  Access データベースオブジェクトをまたは SQL Azure に読み込んでいることを確認し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
2.  Access Metadata Explorer で、移行するデータを含むオブジェクトを選択します。  
  
    -   データベース全体のデータを移行するには、データベース名の横にあるチェックボックスをオンにします。  
  
    -   個々のテーブルからデータを移行するには、データベースを展開し、[ **テーブル**] を展開して、テーブルの横にあるチェックボックスをオンにします。 個々のテーブルからデータを除外するには、このチェックボックスをオフにします。  
  
3.  [ **データベース** ] を右クリックし、[ **データの移行**] を選択します。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Bcp**コマンドラインユーティリティまたはを使用して、ssma の外部でデータを移行することもでき [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ます。 これらのツールの詳細については、オンラインブックを参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="next-step"></a>次の手順  
移行後も引き続き使用するアクセスデータベースアプリケーションがある場合は、Access データベーステーブルを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure テーブルにリンクします。 詳細については、「 [SQL Server への Access アプリケーションのリンク](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[変換オプションと移行オプションの設定](setting-conversion-and-migration-options-accesstosql.md)  
