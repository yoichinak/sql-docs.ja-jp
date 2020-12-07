---
description: SQL Server への変換されたデータベースオブジェクトの読み込み (データへの変換)
title: SQL Server への変換されたデータベースオブジェクトの読み込み (データへの変換) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases, loading converted objects into SQL Azure
- Access databases, loading converted objects into SQL Server
- data, securing
- loading objects into SQL Azure
- loading objects into SQL Server
- migrating objects into SQL Azure
- migrating objects into SQL Server
- moving objects into SQL Azure
- moving objects into SQL Server
- schemas, loading into SQL Azure
- schemas, loading into SQL Server
- scripting converted objects
- securing data
- SQL Azure, loading objects into
- SQL Server, loading objects into
- synchronizing metadata with SQL Azure
- synchronizing metadata with SQL Server
- uploading objects into SQL Azure
- uploading objects into SQL Server
ms.assetid: 4e854eee-b10c-4f0b-9d9e-d92416e6f2ba
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 41a1613a879579e809c8fd6a85d5c9b58c7b2b9c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472579"
---
# <a name="loading-converted-database-objects-into-sql-server-accesstosql"></a>SQL Server への変換されたデータベースオブジェクトの読み込み (データへの変換)
Access データベースオブジェクトをまたは SQL Azure に変換した後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、結果として得られるデータベースオブジェクトをまたは SQL Azure に読み込むことができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 SSMA を使用してオブジェクトを作成するか、オブジェクトのスクリプトを作成して自分でスクリプトを実行することができます。 また、SSMA では、または Azure SQL Database の実際の内容でターゲットメタデータを更新することもでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同期とスクリプトの選択  
変換されたデータベースオブジェクトを変更せずにまたは SQL Azure に読み込む場合は、SSMA を使用し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] てデータベースオブジェクトを直接作成または再作成することができます。 このメソッドは短時間で簡単ですが、 [!INCLUDE[tsql](../../includes/tsql-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアドプロシージャ以外のオブジェクトまたは SQL Azure オブジェクトを定義するコードをカスタマイズすることはできません。  
  
オブジェクトの作成に使用されるを変更する場合 [!INCLUDE[tsql](../../includes/tsql-md.md)] 、またはオブジェクトの作成をより細かく制御する場合は、SSMA を使用してスクリプトを作成します。 その後、これらのスクリプトを変更し、各オブジェクトを個別に作成して、エージェントを使用してそれらのオブジェクトの作成をスケジュールすることもでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>SSMA を使用してオブジェクトを SQL Server と同期させる  
SSMA を使用してオブジェクトを作成または Azure SQL Database するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、次の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 手順に示すように、または SQL Azure メタデータエクスプローラーでオブジェクトを選択し、オブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure と同期します。 既定では、オブジェクトが既にまたは SQL Azure に存在する場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ssma メタデータの一部のローカルな変更や、それらのオブジェクトの定義に対する更新がある場合、SSMA はまたは SQL Azure のオブジェクト定義を変更し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 既定の動作を変更するには、 **プロジェクトの設定**を編集します。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Access データベースから変換されなかった既存のオブジェクトまたは Azure SQL Database オブジェクトを選択できます。 ただし、SSMA では、これらのオブジェクトを再作成したり変更したりすることはありません。  
  
**SQL Server または SQL Azure とオブジェクトを同期するには**  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータエクスプローラーで、上部 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または [SQL Azure] ノードを展開し、[**データベース**] を展開します。  
  
2.  処理するオブジェクトを選択してください:  
  
    -   データベース全体を同期するには、データベース名の横にあるチェックボックスをオンにします。  
  
    -   個々のオブジェクトまたはオブジェクトのカテゴリを同期または除外するには、オブジェクトまたはフォルダーの横にあるチェックボックスをオンまたはオフにします。  
  
3.  または SQL Azure メタデータエクスプローラーで処理するオブジェクトを選択したら、[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **データベース**] を右クリックし、[ **データベースとの同期**] をクリックします。  
  
    オブジェクトまたはオブジェクトのカテゴリを右クリックし、[ **データベースとの同期**] をクリックして、個々のオブジェクトまたはオブジェクトのカテゴリを同期させることもできます。  
  
    その後、SSMA の [ **データベースとの同期** ] ダイアログボックスが表示され、2つのアイテムのグループが表示されます。 左側の SSMA は、ツリーで表される選択されたデータベースオブジェクトを示しています。 右側には、SSMA メタデータ内の同じオブジェクトを表すツリーが表示されます。 ツリーを展開するには、右または左の [+] ボタンをクリックします。 同期の方向は、2つのツリーの間に配置されたアクション列に表示されます。  
  
    アクションの署名には、次の3つの状態があります。  
  
    -   左矢印は、メタデータの内容がデータベースに保存されることを意味します (既定値)。  
  
    -   右矢印は、データベースの内容が SSMA メタデータを上書きすることを意味します。  
  
    -   クロス署名は、何も実行されないことを意味します。  
  
    操作の署名をクリックして、状態を変更します。 実際の同期は、[**データベースとの同期**] ダイアログの [ **OK** ] ボタンをクリックしたときに実行されます。  
  
## <a name="scripting-objects"></a>スクリプトオブジェクト  
変換された [!INCLUDE[tsql](../../includes/tsql-md.md)] データベースオブジェクトの定義を保存する場合、またはオブジェクトの定義を変更して自分でスクリプトを実行する場合は、変換されたデータベースオブジェクトの定義をスクリプトに保存でき [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。  
  
**1つ以上のオブジェクトをスクリプトに保存するには**  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータエクスプローラーで、最上位ノード (サーバー名) を展開し、[**データベース**] を展開します。  
  
2.  次のうち1 つ以上を行います。  
  
    -   データベース全体のスクリプトを作成するには、データベース名の横にあるチェックボックスをオンにします。  
  
    -   個々のビューをスクリプト化または除外するには、データベースを展開し、[ **ビュー**] を展開して、ビューの横にあるチェックボックスをオンまたはオフにします。  
  
    -   個々のテーブルをスクリプト化または除外するには、データベースを展開し、[ **テーブル**] を展開して、テーブルの横にあるチェックボックスをオンまたはオフにします。  
  
    -   テーブルの個々のインデックスをスクリプト化または削除するには、テーブルを展開し、[ **インデックス**] を展開して、インデックスをオンまたはオフにします。  
  
3.  [ **データベース** ] を右クリックし、[ **スクリプトとして保存**] を選択します。  
  
    個々のオブジェクトのスクリプトを作成することもできます。 オブジェクトをスクリプト化するには、どのオブジェクトが選択されているかにかかわらず、オブジェクトを右クリックし、[ **スクリプトとして保存**] をクリックします。  
  
4.  [名前を **付けて保存** ] ダイアログボックスで、スクリプトを保存するフォルダーに移動し、[ **ファイル名** ] ボックスにファイル名を入力して、[ **OK**] をクリックします。  
  
    SSMA により、.sql ファイル名拡張子が追加されます。  
  
### <a name="modifying-scripts"></a>スクリプトの変更  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクトまたは SQL Azure の定義をスクリプトとして保存した後は、を使用して [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] スクリプトを変更できます。  
  
**スクリプトを変更するには**  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **[ファイル]** メニューの **[開く]** をポイントし、 **[ファイル]** をクリックします。  
  
2.  [ **開く** ] ダイアログボックスで、スクリプトファイルを探して選択し、[ **OK**] をクリックします。  
  
3.  クエリエディターを使用して、スクリプトファイルを編集します。  
  
    クエリエディターの詳細については、オンラインブックの「エディターの便利なコマンドと機能」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
4.  スクリプトを保存するには、[ファイル] メニューの [ **保存**] をクリックします。  
  
### <a name="running-scripts"></a>スクリプトの実行  
では、スクリプトまたは個別のステートメントを実行でき [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ます。  
  
**スクリプトを実行するには**  
  
1.  [ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **ファイル** ] メニューの [ **開く** ] をポイントし、[ **ファイル**] をクリックします。  
  
2.  [ **開く** ] ダイアログボックスで、スクリプトファイルを探して選択し、[ **OK**] をクリックします。  
  
3.  スクリプト全体を実行するには、 **F5** キーを押します。  
  
4.  一連のステートメントを実行するには、クエリエディターウィンドウでステートメントを選択し、 **F5** キーを押します。  
  
クエリエディターを使用してスクリプトを実行する方法の詳細については、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] オンラインブックの「クエリ」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
コマンドラインから **sqlcmd** ユーティリティおよびエージェントからスクリプトを実行することもでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 **Sqlcmd**の詳細については、オンラインブックの「sqlcmd ユーティリティ」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 エージェントの詳細について [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、オンラインブックの「管理タスク ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント) の自動化」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="securing-objects-in-sql-server"></a>SQL Server でのオブジェクトのセキュリティ保護  
変換されたデータベースオブジェクトをに読み込むと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、それらのオブジェクトに対する権限を許可および拒否できます。 これは、データをに移行する前に行うことをお勧めし [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 でオブジェクトをセキュリティで保護する方法の詳細について [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、オンラインブックの「データベースおよびデータベースアプリケーションのセキュリティに関する考慮事項」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順では、 [SQL Server にデータを移行](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md)します。  
  
## <a name="see-also"></a>参照  
[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
