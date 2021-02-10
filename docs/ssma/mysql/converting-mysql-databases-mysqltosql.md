---
title: MySQL データベースの変換 (MySQLToSQL) |Microsoft Docs
description: 接続してプロジェクトおよびデータマッピングオプションを設定した後に、MySQL データベースオブジェクトを SSMA で SQL Server または Azure SQL Database オブジェクトに変換する方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ac21850b-fb32-4704-9985-5759b7c688c7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 61298bb7e2c65e85959b52ab3750dc49a5105504
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100069015"
---
# <a name="converting-mysql-databases-mysqltosql"></a>MySQL データベースの変換 (MySQLToSQL)
MySQL への接続、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure への接続、およびプロジェクトおよびデータマッピングのオプションの設定が完了したら、mysql データベースオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または Azure SQL Database オブジェクトに変換できます。  
  
## <a name="the-conversion-process"></a>変換処理  
データベースオブジェクトを変換すると、MySQL からオブジェクトの定義が取得され、それらのオブジェクトが類似または SQL Azure のオブジェクトに変換され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、この情報が SSMA メタデータに読み込まれます。 のインスタンスに情報は読み込まれません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 または SQL Azure メタデータエクスプローラーを使用して、オブジェクトとそのプロパティを表示でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
変換中に SSMA は出力メッセージを出力ウィンドウに出力し、エラーメッセージをエラー一覧ウィンドウに出力します。 出力とエラーの情報を使用して、MySQL データベースまたは変換プロセスを変更して目的の変換結果を取得する必要があるかどうかを判断します。  
  
## <a name="setting-conversion-options"></a>変換オプションの設定  
オブジェクトを変換する前に、[ **プロジェクトの設定** ] ダイアログボックスでプロジェクトの変換オプションを確認してください。 このダイアログボックスを使用すると、SSMA によるテーブルおよびインデックスの変換方法を設定できます。 詳細については、「[プロジェクトの設定 &#40;変換&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md) 」を参照してください。  
  
## <a name="conversion-results"></a>変換結果  
次の表は、変換される MySQL オブジェクトと、結果として得られるオブジェクトを示してい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
|MySQL オブジェクト|結果の SQL Server オブジェクト|  
|-|-|  
|インデックスなどの依存オブジェクトを含むテーブル|SSMA によって、依存オブジェクトを含むテーブルが作成されます。 テーブルは、すべてのインデックスと制約に変換されます。 インデックスは、個別のオブジェクトに変換され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。<br /><br />**空間データ型のマッピング** は、テーブルノードレベルでのみ実行できます。<br /><br />テーブル変換の設定の詳細については、「[変換の設定](conversion-settings-mysqltosql.md)」を参照してください。|  
|関数|関数を Transact-SQL に直接変換できる場合は、SSMA によって関数が作成されます。 場合によっては、関数をストアド プロシージャに変換する必要があります。 これは、プロジェクト設定の **関数変換** を使用して行うことができます。 この場合、SSMA によってストアド プロシージャが作成され、ストアド プロシージャを呼び出す関数が作成されます。<br /><br />**指定された選択肢:**<br /><br />プロジェクト設定に従って変換する<br /><br />関数に変換<br /><br />ストアドプロシージャへの変換<br /><br />関数の変換設定の詳細については、「[変換の設定](conversion-settings-mysqltosql.md)」を参照してください。|  
|手順|プロシージャを Transact-SQL に直接変換できる場合は、SSMA によってストアド プロシージャが作成されます。 場合によっては、独立したトランザクションでストアドプロシージャを呼び出す必要があります。 この場合は、SSMA によって 2 つのストアド プロシージャが作成されます。1 つはプロシージャを実装するストアド プロシージャで、もう 1 つは実装ストアド プロシージャを呼び出すために使用されるものです。|  
|データベースの変換|MySQL オブジェクトとしてのデータベースは、SSMA for MySQL によって直接変換されるわけではありません。 MySQL データベースはスキーマ名と同様に処理され、すべての物理パラメーターは変換時に失われます。 SSMA for MySQL は [、mysql データベースを SQL Server スキーマ &#40;MySQLToSQL&#41;にマッピング ](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md) して、mysql データベースから適切な SQL Server データベース/スキーマのペアにオブジェクトをマップします。|  
|トリガーの変換|**SSMA は、次の規則に基づいてトリガーを作成します。**<br /><br />T-sql トリガーではなくトリガーがに変換される前<br /><br />AFTER トリガーは、行ごとにイテレーションがあるか、または指定されていない場合に、に変換されます。|  
|変換の表示|SSMA により、依存オブジェクトを含むビューが作成されます。|  
|ステートメントの変換|-各 SQL ステートメントオブジェクトには、1つの MySQL ステートメント (DDL、DML、およびその他の種類のステートメントなど) を含めることも、開始...終了ブロック。<br />-   複数 **ステートメントの変換: BEGIN...END block conversion** SQL ステートメントには、BEGIN...プロシージャ、関数、またはトリガー定義でのようにブロックを終了します。 これらのブロックは、1つの MySQL ステートメントオブジェクトに対して変換するのと同じように変換する必要があります。|  
  
## <a name="converting-mysql-database-objects"></a>MySQL データベースオブジェクトの変換  
MySQL データベースオブジェクトを変換するには、まず変換するオブジェクトを選択し、SSMA によって変換が実行されるようにします。 変換中に出力メッセージを表示するには、[ **表示** ] メニューの [ **出力**] をクリックします。  
  
**MySQL オブジェクトを SQL Server または SQL Azure 構文に変換するには**  
  
1.  MySQL メタデータエクスプローラーで、MySQL サーバーを展開し、[ **データベース**] を展開します。  
  
2.  変換するオブジェクトの選択:  
  
    -   すべてのスキーマを変換するには、[ **データベース**] の横にあるチェックボックスをオンにします。  
  
    -   データベースを変換または省略するには、データベース名の横にあるチェックボックスをオンにします。  
  
    -   オブジェクトのカテゴリを変換または除外するには、スキーマを展開し、カテゴリの横にあるチェックボックスをオンまたはオフにします。  
  
    -   個々のオブジェクトを変換または除外するには、[カテゴリ] フォルダーを展開し、オブジェクトの横にあるチェックボックスをオンまたはオフにします。  
  
3.  選択したすべてのオブジェクトを変換するには、[ **データベース** ] を右クリックし、[ **スキーマの変換**] をクリックします。  
  
    また、オブジェクトまたはオブジェクトのカテゴリを右クリックし、[ **スキーマの変換**] を選択して、オブジェクトの個々のカテゴリを変換することもできます。  
  
## <a name="viewing-conversion-problems"></a>変換に関する問題の表示  
一部の MySQL オブジェクトが変換されない可能性があります。 変換の成功率を確認するには、概要変換レポートを表示します。  
  
**概要レポートを表示するには**  
  
1.  MySQL メタデータエクスプローラーで、[ **データベース**] を選択します。  
  
2.  右ペインで、[ **レポート** ] タブを選択します。  
  
    このレポートには、評価または変換されたすべてのデータベースオブジェクトの概要評価レポートが表示されます。 個々のオブジェクトの概要レポートを表示することもできます。  
  
    -   個々のスキーマのレポートを表示するには、MySQL メタデータエクスプローラーでデータベースを選択します。  
  
    -   個々のオブジェクトのレポートを表示するには、MySQL メタデータエクスプローラーでオブジェクトを選択します。 変換の問題が発生しているオブジェクトには、赤色のエラーアイコンが付いています。  
  
変換に失敗したオブジェクトの場合、変換に失敗した原因となった構文を確認できます。  
  
**個々の変換の問題を表示するには**  
  
1.  MySQL メタデータエクスプローラーで、[ **データベース**] を展開します。  
  
2.  赤いエラーアイコンが表示されているデータベースを展開します。  
  
3.  データベースの下に、赤色のエラーアイコンが表示されているフォルダーを展開します。  
  
4.  赤色のエラーアイコンが付いているオブジェクトを選択します。  
  
5.  右ペインで、[ **レポート** ] タブをクリックします。  
  
6.  [ **レポート** ] タブの上部にドロップダウンリストが表示されます。 一覧に **統計** が表示されている場合は、選択範囲を **Source** に変更します。  
  
    SSMA では、コードのすぐ上にソースコードといくつかのボタンが表示されます。  
  
7.  [ **次の問題** ] ボタンをクリックします。 これは、右を指し示す矢印の付いた赤いエラーアイコンです。  
  
    SSMA は、現在のオブジェクトで検出された最初の問題のソースコードを強調表示します。  
  
変換できなかった項目ごとに、そのオブジェクトをどのように処理するかを決定する必要があります。  
  
-   MySQL データベース内のオブジェクトを変更して、問題のあるコードを削除または修正することができます。 更新されたコードを SSMA に読み込むには、メタデータを更新する必要があります。 詳細については、「 [MySQL への接続 &#40;MySQLToSQL](../../ssma/mysql/connecting-to-mysql-mysqltosql.md) 」を参照してください&#41;  
  
-   オブジェクトを移行から除外することができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータエクスプローラーおよび Mysql メタデータエクスプローラーで、項目の横のチェックボックスをオフにしてから、mysql からのオブジェクトの読み込みや [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データの SQL Azure と移行を行います。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次のステップでは、変換された [データベースオブジェクトを SQL Server &#40;MySQLToSQL に読み込み&#41;](../../ssma/mysql/loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
## <a name="see-also"></a>参照  
[MySQL データベースを SQL Server Azure SQL Database &#40;MySQLToSql&#41;に移行する ](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
