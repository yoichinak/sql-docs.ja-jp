---
description: Sybase ASE データベース オブジェクトの変換 (SybaseToSQL)
title: Sybase ASE データベースオブジェクトの変換 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Converting Database Objects
ms.assetid: 509cb65d-2f54-427a-83d7-37919cc4e3e3
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 66384c27490bbc9d330f5f2d186bad1b4f4b97ee
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038864"
---
# <a name="converting-sap-ase-database-objects-sybasetosql"></a>SAP ASE データベースオブジェクトの変換 (SybaseToSQL)
SAP Adaptive Server Enterprise (ASE) に接続した後、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または AZURE sql に接続し、プロジェクトとデータのマッピングオプションを設定した後、Sap Adaptive Server enterprise (ase) データベースオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または azure sql database オブジェクトに変換できます。  
  
## <a name="the-conversion-process"></a>変換プロセス  
データベースオブジェクトを変換すると、ASE からオブジェクトの定義が取得され、類似 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトまたは SQL Azure オブジェクトに変換され、この情報が SSMA メタデータに読み込まれます。 この情報は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または AZURE SQL のインスタンスに読み込まれません。 その後、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または AZURE SQL メタデータエクスプローラーを使用して、オブジェクトとそのプロパティを表示できます。
  
変換中に SSMA は出力メッセージを出力ウィンドウに出力し、エラーメッセージを **エラー一覧** ウィンドウに出力します。 出力とエラーの情報を使用して、必要な変換結果を取得するために ASE データベースまたは変換プロセスを変更する必要があるかどうかを判断します。  
  
## <a name="setting-conversion-options"></a>変換オプションの設定  
オブジェクトを変換する前に、[ **プロジェクトの設定** ] ダイアログボックスでプロジェクトの変換オプションを確認してください。 このダイアログボックスを使用すると、SSMA が関数とグローバル変数を変換する方法を設定できます。 詳細については、「 [プロジェクトの設定 &#40;変換&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-conversion-sybasetosql.md)」を参照してください。  
  
## <a name="converting-ase-database-objects"></a>ASE データベースオブジェクトの変換  
ASE データベースオブジェクトを変換するには、まず変換するオブジェクトを選択し、SSMA によって変換が実行されるようにします。 変換中に出力メッセージを表示するには、[ **表示** ] メニューの [ **出力**] をクリックします。  
  
**ASE オブジェクトを SQL Server または SQL Azure 構文に変換するには**  
  
1.  Sybase メタデータエクスプローラーで、ASE サーバーを展開し、[ **データベース**] を展開します。  
  
2.  変換するオブジェクトの選択:  
  
    -   すべてのデータベースを変換するには、[ **データベース**] の横にあるチェックボックスをオンにします。  
  
    -   データベースを変換または省略するには、データベース名の横にあるチェックボックスをオンまたはオフにします。  
  
    -   個々のスキーマを変換または省略するには、データベースを展開し、[ **スキーマ**] を展開して、スキーマの横にあるチェックボックスをオンまたはオフにします。  
  
    -   オブジェクトのカテゴリを変換または除外するには、スキーマを展開し、カテゴリの横にあるチェックボックスをオンまたはオフにします。  
  
    -   個々のオブジェクトを変換または除外するには、[カテゴリ] フォルダーを展開し、オブジェクトの横にあるチェックボックスをオンまたはオフにします。  
  
3.  選択したすべてのオブジェクトを変換するには、[ **データベース**] を右クリックし、[ **スキーマの変換**] を選択します。  
  
    また、オブジェクトまたはオブジェクトのカテゴリを右クリックし、[ **スキーマの変換**] をクリックして、個々のオブジェクトまたはオブジェクトのカテゴリを変換することもできます。  
  
> [!NOTE]  
> 一部の SAP ASE システム関数は、動作しているのと同等の SQL Server システム関数と完全には一致しません。 SAP ASE の動作をエミュレートするために、SSMA は、変換された SQL Server データベース内のユーザー定義関数を、"2ss" というスキーマの下に生成します。 プロジェクトの設定によっては、一部の SQL Server システム関数がこれらのエミュレートされた関数に置き換えられます。 SSMA では、次のユーザー定義関数が作成されます。  

:::row:::
    :::column:::
        **char_length_nvarchar**  
        **char_length_varchar**  
        **charindex_nvarchar**  
        **charindex_varchar**  
        **hextoint**  
        **index_colorder**  
    :::column-end:::
    :::column:::
        **inttohex**  
        **ssma_current_time**  
        **ssma_datediff**  
        **ssma_datepart**  
        **substring_nvarchar**  
        **substring_varbinary**  
    :::column-end:::
    :::column:::
        **substring_varchar**  
        **to_unichar**  
        **uhigh、r**  
        **ulow、r**  
    :::column-end:::
:::row-end:::

## <a name="objects-not-supported-in-azure-sql"></a>Azure SQL でサポートされていないオブジェクト  
SSMA for SAP ASE では、オンプレミス SQL Server への変換中に次の T-sql キーワードが使用されますが、これらのキーワードは SQL Azure T-sql 構文ではサポートされていません。  

:::row:::
    :::column:::
        CHECKPOINT  
        CREATE/ALTER/DROP DEFAULT  
        CREATE/DROP RULE  
        DBCC TRACEOFF  
        DBCC TRACEON  
    :::column-end:::
    :::column:::
        GRANT/REVOKE/DENY ALL  
        KILL  
        READTEXT  
        SELECT INTO  
        SET OFFSETS  
    :::column-end:::
    :::column:::
        SETUSER  
        SHUTDOWN  
        WRITETEXT  
    :::column-end:::
:::row-end:::

## <a name="viewing-conversion-problems"></a>変換に関する問題の表示  
一部の SAP ASE オブジェクトが変換されない可能性があります。 変換の成功率を確認するには、概要変換レポートを表示します。  
  
**概要レポートを表示するには**  
  
1.  Sybase メタデータエクスプローラーで、[ **データベース**] を選択します。  
  
2.  右ペインで、[ **レポート** ] タブを選択します。  
  
    このレポートには、評価または変換されたすべてのデータベースオブジェクトの概要評価レポートが表示されます。 個々のオブジェクトの概要レポートを表示することもできます。  
  
    -   個々のデータベースのレポートを表示するには、Sybase メタデータエクスプローラーでデータベースを選択します。  
  
    -   個々のデータベースオブジェクトのレポートを表示するには、Sybase メタデータエクスプローラーでオブジェクトを選択します。 変換の問題が発生しているオブジェクトには、赤色のエラーアイコンが付いています。  
  
変換に失敗したオブジェクトの場合、変換に失敗した原因となった構文を確認できます。  
  
**個々の変換の問題を表示するには**  
  
1.  Sybase メタデータエクスプローラーで、[ **データベース**] を展開します。  
  
2.  赤いエラーアイコンが表示されているデータベースを展開します。  
  
3.  [ **スキーマ** ] フォルダーを展開し、赤色のエラーアイコンが表示されているスキーマを展開します。  
  
4.  スキーマの下に、赤色のエラーアイコンが表示されているフォルダーを展開します。  
  
5.  赤色のエラーアイコンが付いているオブジェクトを選択します。  
  
6.  右ペインで、[ **レポート** ] タブを選択します。  
  
7.  [ **レポート** ] タブの上部にドロップダウンリストが表示されます。 一覧に **統計**が表示されている場合は、選択範囲を **Source**に変更します。  
  
    SSMA では、コードのすぐ上にソースコードといくつかのボタンが表示されます。  
  
8.  [ **次の問題**] を選択します。右を指している矢印が付いた赤いエラーアイコン。  
  
    SSMA for SAP ASE は、現在のオブジェクトで検出された最初の問題のソースコードを強調表示します。  
  
変換できなかった項目ごとに、そのオブジェクトをどのように処理するかを決定する必要があります。  
  
-   **SQL**タブでプロシージャおよびトリガーのソースコードを編集できます。  
  
-   問題のあるコードを削除または変更するには、SAP ASE オブジェクトを変更します。 更新されたコードを SSMA に読み込むには、メタデータを更新する必要があります。 詳細については、「 [SAP ASE &#40;SybaseToSQL&#41;への接続 ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)」を参照してください。  
  
-   オブジェクトを移行から除外することができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または AZURE Sql Metadata explorer と Sybase メタデータエクスプローラーで、オブジェクトをまたは AZURE sql に読み込む前に項目の横のチェックボックスをオフにし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SAP ASE からデータを移行します。  
  
## <a name="next-steps"></a>次の手順  
移行プロセスの次のステップでは、変換された [データベースオブジェクトを SQL Server/SQL Azure (SybaseToSQL) に読み込み](./loading-converted-database-objects-into-sql-server-sybasetosql.md)ます。  
  
## <a name="see-also"></a>関連項目  
[SAP ASE データベースの SQL Server Azure SQL Database &#40;SybaseToSQL&#41;への移行 ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
