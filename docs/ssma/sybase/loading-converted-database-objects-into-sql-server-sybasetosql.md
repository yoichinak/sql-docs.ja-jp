---
description: SQL Server への変換されたデータベース オブジェクトの読み込み (SybaseToSQL)
title: 変換されたデータベースオブジェクトを SQL Server に読み込む (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Loading Converted Database Objects
ms.assetid: 4c59256f-99a8-4351-9559-a455813dbd06
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6b7f9a9a69fd1f5ac685550fb91ab93ad2220f49
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038263"
---
# <a name="loading-converted-database-objects-into-sql-server-sybasetosql"></a>SQL Server への変換されたデータベース オブジェクトの読み込み (SybaseToSQL)
Sybase Adaptive Server Enterprise (ASE) データベースオブジェクトをまたは SQL Azure に変換した後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、結果として得られるデータベースオブジェクトをまたは SQL Azure に読み込むことができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 SSMA を使用してオブジェクトを作成するか、オブジェクトのスクリプトを作成して自分でスクリプトを実行することができます。 また、SSMA では、または Azure SQL Database の実際の内容でターゲットメタデータを更新することもでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同期とスクリプトの選択  
変換されたデータベースオブジェクトを変更せずにまたは SQL Azure に読み込む場合は、SSMA を使用し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] てデータベースオブジェクトを直接作成または再作成することができます。 このメソッドは短時間で簡単ですが、 [!INCLUDE[tsql](../../includes/tsql-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアドプロシージャ以外のオブジェクトまたは SQL Azure オブジェクトを定義するコードをカスタマイズすることはできません。  
  
[!INCLUDE[tsql](../../includes/tsql-md.md)]または SQL Azure でオブジェクトの作成に使用されるを変更する場合、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure でオブジェクトを作成するタイミングと方法をより細かく制御する場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、ssma を使用してスクリプトを作成 [!INCLUDE[tsql](../../includes/tsql-md.md)] します。 これらのスクリプトを変更し、各オブジェクトを個別に作成して、または SQL Azure エージェントを使用して、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] それらのオブジェクトの作成をスケジュールすることもできます。  
  
## <a name="using-ssma-to-load-objects-into-sql-server-or-sql-azure"></a>SSMA を使用して SQL Server または SQL Azure にオブジェクトを読み込む  
SSMA を使用してオブジェクトを作成または Azure SQL Database するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、次の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 手順に示すように、または SQL Azure メタデータエクスプローラーでオブジェクトを選択し、オブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure と同期します。 既定では、オブジェクトが既にまたは SQL Azure に存在する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ssma メタデータの一部のローカルな変更や、それらのオブジェクトの定義に対する更新がある場合、SSMA はまたは SQL Azure のオブジェクト定義を変更し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 既定の動作を変更するには、 **プロジェクトの設定**を編集します。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ASE データベースから変換されなかった既存のオブジェクトまたは Azure SQL Database オブジェクトを選択できます。 ただし、これらのオブジェクトは SSMA によって再作成または変更されることはありません。  
  
**SQL Server または SQL Azure とオブジェクトを同期するには**  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータエクスプローラーで、上部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [SQL Azure] ノードを展開し、[**データベース**] を展開します。  
  
2.  処理するオブジェクトを選択してください:  
  
    -   データベース全体を同期するには、データベース名の横にあるチェックボックスをオンにします。  
  
    -   個々のオブジェクトまたはオブジェクトのカテゴリを同期または除外するには、オブジェクトまたはフォルダーの横にあるチェックボックスをオンまたはオフにします。  
  
3.  または SQL Azure メタデータエクスプローラーで処理するオブジェクトを選択したら、[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **データベース**] を右クリックし、[ **データベースとの同期**] をクリックします。  
  
    オブジェクトまたはオブジェクトのカテゴリを右クリックし、[  **データベースとの同期**] をクリックして、個々のオブジェクトまたはオブジェクトのカテゴリを同期させることもできます。  
  
    その後、SSMA の [ **データベースとの同期** ] ダイアログボックスが表示され、2つのアイテムのグループが表示されます。 左側の SSMA は、ツリーで表される選択されたデータベースオブジェクトを示しています。 右側には、SSMA メタデータ内の同じオブジェクトを表すツリーが表示されます。 ツリーを展開するには、右または左の [+] ボタンをクリックします。 同期の方向は、2つのツリーの間に配置されたアクション列に表示されます。  
  
    アクションの署名には、次の3つの状態があります。  
  
    -   左矢印は、メタデータの内容がデータベースに保存されることを意味します (既定値)。  
  
    -   右矢印は、データベースの内容が SSMA メタデータを上書きすることを意味します。  
  
    -   クロス署名は、何も実行されないことを意味します。  
  
操作の署名をクリックして、状態を変更します。 実際の同期は、[**データベースとの同期**] ダイアログの [ **OK** ] ボタンをクリックしたときに実行されます。  
  
## <a name="scripting-objects"></a>スクリプトオブジェクト  
変換された [!INCLUDE[tsql](../../includes/tsql-md.md)] データベースオブジェクトの定義を保存する場合、またはオブジェクトの定義を変更して自分でスクリプトを実行する場合は、変換されたデータベースオブジェクトの定義をスクリプトに保存でき [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。  
  
**オブジェクトをスクリプトとして保存するには**  
  
1.  スクリプトに保存するオブジェクトを選択したら、[ **データベース**] を右クリックし、[ **スクリプトとして保存**] を選択します。  
  
    オブジェクトまたはオブジェクトのカテゴリを右クリックし、[ **スクリプトの保存**] を選択して、個々のオブジェクトまたはオブジェクトのカテゴリをスクリプト化することもできます。  
  
2.  [名前を **付けて保存** ] ダイアログボックスで、スクリプトを保存するフォルダーに移動し、[ **ファイル名** ] ボックスにファイル名を入力して、[ **OK**] をクリックします。  
  
    SSMA により、.sql ファイル名拡張子が追加されます。  
  
### <a name="modifying-scripts"></a>スクリプトの変更  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクトまたは SQL Azure の定義を1つ以上のスクリプトとして保存した後、を使用して [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] スクリプトを表示および変更できます。  
  
**スクリプトを変更するには**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **[ファイル]** メニューの **[開く]** をポイントし、 **[ファイル]** をクリックします。  
  
2.  [ **開く** ] ダイアログボックスで、に移動してスクリプトファイルを選択し、[ **OK**] をクリックします。  
  
3.  クエリエディターを使用して、スクリプトファイルを編集します。  
  
    クエリエディターの詳細については、オンラインブックの「エディターの便利なコマンドと機能」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
4.  スクリプトを保存するには、[ファイル] メニューの [ **保存**] をクリックします。  
  
### <a name="running-scripts"></a>スクリプトの実行  
では、スクリプトまたは個別のステートメントを実行でき [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ます。  
  
**スクリプトを実行するには**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **[ファイル]** メニューの **[開く]** をポイントし、 **[ファイル]** をクリックします。  
  
2.  [ **開く** ] ダイアログボックスで、に移動してスクリプトファイルを選択し、[ **OK**] をクリックします。  
  
3.  スクリプト全体を実行するには、 **F5** キーを押します。  
  
4.  一連のステートメントを実行するには、クエリエディターウィンドウでステートメントを選択し、 **F5** キーを押します。  
  
クエリエディターを使用してスクリプトを実行する方法の詳細については、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] オンラインブックの「クエリ」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
コマンドラインから **sqlcmd** ユーティリティおよびエージェントからスクリプトを実行することもでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 **Sqlcmd**の詳細については、オンラインブックの「sqlcmd ユーティリティ」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 エージェントの詳細について [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、オンラインブックの「管理タスク ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント) の自動化」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="securing-objects-in-sql-server"></a>SQL Server でのオブジェクトのセキュリティ保護  
変換されたデータベースオブジェクトをに読み込むと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、それらのオブジェクトに対する権限を許可および拒否できます。 これは、データをに移行する前に行うことをお勧めし [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 でオブジェクトをセキュリティで保護する方法の詳細について [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、オンラインブックの「データベースおよびデータベースアプリケーションのセキュリティに関する考慮事項」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順では、 [SYBASE ASE データを SQL Server/SQL Azure (SybaseToSQL) に移行](./migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md)します。  
  
## <a name="see-also"></a>参照  
[Sybase ASE データベースを SQL Server Azure SQL Database &#40;SybaseToSQL&#41;に移行する ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
