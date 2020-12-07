---
description: 変換されたデータベースオブジェクトを SQL Server に読み込んでいます (DB2ToSQL)
title: 変換されたデータベースオブジェクトを SQL Server に読み込んでいます (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: f4ea1ced-9f9f-4a9d-88ab-81dbab64adc3
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: e89edc66dee92fb74071de952e056d99c91cbf12
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91985028"
---
# <a name="loading-converted-database-objects-into-sql-server-db2tosql"></a>変換されたデータベースオブジェクトを SQL Server に読み込んでいます (DB2ToSQL)
DB2 スキーマをに変換した後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、結果として得られるデータベースオブジェクトをに読み込むことができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 SSMA を使用してオブジェクトを作成するか、オブジェクトのスクリプトを作成して自分でスクリプトを実行することができます。 また、SSMA では、ターゲットメタデータをデータベースの実際の内容で更新することもでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="choosing-between-synchronization-and-scripts"></a>同期とスクリプトの選択  
変換されたデータベースオブジェクトを変更せずにに読み込む場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、SSMA によってデータベースオブジェクトを直接作成または再作成することができます。 このメソッドは短時間で簡単ですが、 [!INCLUDE[tsql](../../includes/tsql-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアドプロシージャ以外のオブジェクトを定義するコードをカスタマイズすることはできません。  
  
オブジェクトの作成に使用されるを変更する場合 [!INCLUDE[tsql](../../includes/tsql-md.md)] 、またはオブジェクトの作成をより細かく制御する場合は、SSMA を使用してスクリプトを作成します。 その後、これらのスクリプトを変更し、各オブジェクトを個別に作成して、エージェントを使用してそれらのオブジェクトの作成をスケジュールすることもでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="using-ssma-to-synchronize-objects-with-sql-server"></a>SSMA を使用してオブジェクトを SQL Server と同期させる  
SSMA を使用してデータベースオブジェクトを作成するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 次の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 手順に示すように、メタデータエクスプローラーでオブジェクトを選択し、オブジェクトをと同期します。 既定では、オブジェクトが既にに存在して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] おり、ssma メタデータがのオブジェクトより新しい場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、ssma によってのオブジェクト定義が変更され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 既定の動作を変更するには、 **プロジェクトの設定**を編集します。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DB2 データベースから変換されなかった既存のデータベースオブジェクトを選択できます。 ただし、これらのオブジェクトは SSMA によって再作成または変更されることはありません。  
  
**オブジェクトを SQL Server と同期するには**  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メタデータエクスプローラーで、最上位 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ノードを展開し、[**データベース**] を展開します。  
  
2.  処理するオブジェクトを選択してください:  
  
    -   データベース全体を同期するには、データベース名の横にあるチェックボックスをオンにします。  
  
    -   個々のオブジェクトまたはオブジェクトのカテゴリを同期または除外するには、オブジェクトまたはフォルダーの横にあるチェックボックスをオンまたはオフにします。  
  
3.  メタデータエクスプローラーで処理するオブジェクトを選択したら [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、[ **データベース**] を右クリックし、[ **データベースとの同期**] をクリックします。  
  
    オブジェクトまたはオブジェクトのカテゴリを右クリックし、[  **データベースとの同期**] をクリックして、個々のオブジェクトまたはオブジェクトのカテゴリを同期させることもできます。  
  
    その後、SSMA の [ **データベースとの同期** ] ダイアログボックスが表示され、2つのアイテムのグループが表示されます。 左側の SSMA は、ツリーで表される選択されたデータベースオブジェクトを示しています。 右側には、SSMA メタデータ内の同じオブジェクトを表すツリーが表示されます。 ツリーを展開するには、右または左の [+] ボタンをクリックします。 同期の方向は、2つのツリーの間に配置されたアクション列に表示されます。  
  
    アクションの署名には、次の3つの状態があります。  
  
    -   左矢印は、メタデータの内容がデータベースに保存されることを意味します (既定値)。  
  
    -   右矢印は、データベースの内容が SSMA メタデータを上書きすることを意味します。  
  
    -   クロス署名は、何も実行されないことを意味します。  
  
操作の署名をクリックして、状態を変更します。 実際の同期は、[**データベースとの同期**] ダイアログの [ **OK** ] ボタンをクリックしたときに実行されます。  
  
## <a name="scripting-objects"></a>スクリプトオブジェクト  
変換された [!INCLUDE[tsql](../../includes/tsql-md.md)] データベースオブジェクトの定義を保存する、またはオブジェクトの定義を変更してスクリプトを実行するには、変換されたデータベースオブジェクトの定義をスクリプトに保存し [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。  
  
**オブジェクトをスクリプトとして保存するには**  
  
1.  スクリプトに保存するオブジェクトを選択したら、[ **データベース**] を右クリックし、[ **スクリプトとして保存**] をクリックします。  
  
    オブジェクトまたはその親フォルダーを右クリックし、[ **スクリプトとして保存**] をクリックして、個々のオブジェクトまたはオブジェクトのカテゴリをスクリプト化することもできます。  
  
2.  [名前を **付けて保存** ] ダイアログボックスで、スクリプトを保存するフォルダーに移動し、[ **ファイル名** ] ボックスにファイル名を入力して、をクリックし [!INCLUDE[clickOK](../../includes/clickok-md.md)] ます。 SSMA により、.sql ファイル名拡張子が追加されます。  
  
### <a name="modifying-scripts"></a>スクリプトの変更  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]オブジェクト定義を1つ以上のスクリプトとして保存した後、を使用して [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] スクリプトを表示および変更できます。  
  
**スクリプトを変更するには**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **[ファイル]** メニューの **[開く]** をポイントし、 **[ファイル]** をクリックします。  
  
2.  [ **開く** ] ダイアログボックスで、スクリプトファイルを選択し、[OK] をクリックします。
  
3.  クエリエディターを使用して、スクリプトファイルを編集します。  
  
    クエリエディターの詳細については、オンラインブックの「エディターの便利なコマンドと機能」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
4.  スクリプトを保存するには、[ファイル] メニューの [ **保存**] をクリックします。  
  
### <a name="running-scripts"></a>スクリプトの実行  
では、スクリプトまたは個別のステートメントを実行でき [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ます。  
  
**スクリプトを実行するには**  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **[ファイル]** メニューの **[開く]** をポイントし、 **[ファイル]** をクリックします。  
  
2.  [ **開く** ] ダイアログボックスで、スクリプトファイルを選択し、 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  スクリプト全体を実行するには、 **F5** キーを押します。  
  
4.  一連のステートメントを実行するには、クエリエディターウィンドウでステートメントを選択し、 **F5** キーを押します。  
  
クエリエディターを使用してスクリプトを実行する方法の詳細については、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] オンラインブックの「クエリ」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
また、 **sqlcmd** ユーティリティを使用してコマンドラインからスクリプトを実行したり、エージェントからスクリプトを実行したりすることもでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 **Sqlcmd**の詳細については、オンラインブックの「sqlcmd ユーティリティ」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 エージェントの詳細について [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、オンラインブックの「管理タスク ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント) の自動化」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="securing-objects-in-sql-server"></a>SQL Server でのオブジェクトのセキュリティ保護  
変換されたデータベースオブジェクトをに読み込むと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、それらのオブジェクトに対する権限を許可および拒否できます。 これは、データをに移行する前に行うことをお勧めし [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 でオブジェクトをセキュリティで保護する方法の詳細について [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、オンラインブックの「データベースおよびデータベースアプリケーションのセキュリティに関する考慮事項」を参照してください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順は、 [DB2 データを SQL Server に移行](./migrating-db2-data-into-sql-server-db2tosql.md)することです。  
  
## <a name="see-also"></a>参照  
[DB2 データの SQL Server &#40;DB2ToSQL&#41;への移行 ](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
