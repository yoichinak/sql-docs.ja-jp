---
description: 変換のための MySQL データベースの評価 (MySQLToSQL)
title: 変換のための MySQL データベースの評価 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Assessment reports
ms.assetid: 2a56a003-3b0f-453a-963c-00c9e40933ec
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 5512d7230b1b59add11e0d72efba232bb3770099
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88320798"
---
# <a name="assessing-mysql-databases-for-conversion-mysqltosql"></a>変換のための MySQL データベースの評価 (MySQLToSQL)
オブジェクトを読み込み、データをまたは SQL Azure に移行する前に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、移行の複雑さと移行にかかる時間を決定する必要があります。 SSMA は、正常に変換されるオブジェクトの割合を示す評価レポートを作成できます。 SSMA では、変換エラーの原因となる具体的な問題を確認することもできます。  
  
## <a name="creating-assessment-reports"></a>評価レポートの作成  
この評価レポートを作成すると、SSMA は、選択した MySQL データベースオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure 構文に変換し、結果を表示します。  
  
**評価レポートを作成するには**  
  
1.  MySQL メタデータエクスプローラーで、評価するスキーマを選択します。  
  
2.  個々のオブジェクトを省略するには、その横にあるチェックボックスをオフにします。  
  
3.  [ **スキーマ**] を右クリックし、[ **レポートの作成**] を選択します。  
  
    オブジェクトを右クリックして、個々のオブジェクトを分析します。 次に、[ **レポートの作成**] を選択します。  
  
    SSMA により、ウィンドウの下部にあるステータスバーに進行状況が表示されます。 出力ウィンドウが表示されている場合は、[出力] ウィンドウにメッセージも表示されます。  
  
    評価が完了すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant For MySQL の [評価レポート] ウィンドウが表示されます。  
  
## <a name="using-assessment-reports"></a>評価レポートの使用  
[評価レポート] ウィンドウには、次の3つのペインがあります。  
  
-   左側のウィンドウには、評価レポートに含まれるオブジェクトの階層が表示されます。 階層を参照し、オブジェクトのオブジェクトとカテゴリを選択して、変換の統計情報とコードを表示することができます。  
  
-   右側のウィンドウの内容は、左側のウィンドウで選択した項目によって異なります。  
  
    スキーマなど、オブジェクトのグループが選択されている場合、右側のペインには [変換統計] ペインと [カテゴリ別のオブジェクト] ウィンドウが表示されます。 [変換統計] ペインには、選択したオブジェクトの変換統計が表示されます。 [カテゴリ別のオブジェクト] ペインには、オブジェクトまたはオブジェクトのカテゴリの変換統計が表示されます。  
  
    関数、プロシージャ、テーブル、またはビューが選択されている場合、右側のペインには統計、ソースコード、およびターゲットコードが表示されます。  
  
    -   上の領域には、オブジェクトの全体的な統計が表示されます。 この情報を表示するには、 **統計** の展開が必要になる場合があります。  
  
    -   [ソース] 領域には、左ペインで選択したオブジェクトのソースコードが表示されます。 強調表示された領域には、問題のあるソースコードが表示されます。  
  
    -   ターゲット領域には、変換されたコードが表示されます。 赤いテキストは、問題のあるコードとエラーメッセージを示しています。  
  
-   下部のペインには、メッセージ番号でグループ化された変換メッセージが表示されます。 [ **エラー**]、[ **警告**]、または [ **情報** ] をクリックして、メッセージのカテゴリを表示し、メッセージのグループを展開することができます。 個々のメッセージをクリックして左ペインでオブジェクトを選択すると、右側のウィンドウに詳細が表示されます。  
  
## <a name="analyzing-conversion-problems-by-using-the-assessment-report"></a>評価レポートを使用した変換の問題の分析  
[変換統計] ペインに、変換の統計が表示されます。 いずれかのカテゴリの割合が100% 未満の場合は、変換が成功しなかった理由を判断する必要があります。  
  
**変換の問題を表示するには**  
  
1.  前の手順の指示に従って、評価レポートを作成します。  
  
2.  左側のウィンドウで、[スキーマ] または赤色のエラーアイコンが表示されているフォルダーを展開します。 変換に失敗した個々の項目を選択するまで、項目を展開し続けます。  
  
3.  ソースペインの上部にある [次の **問題**] をクリックします。  
  
    ターゲットナビゲーションウィンドウの関連コードと同様に、問題のあるコードが強調表示されます。  
  
4.  エラーメッセージを確認し、変換の問題の原因となったオブジェクトで何を実行するかを決定します。  
  
-   SSMA で MySQL 構文を更新します。 構文は、プロシージャと関数に対してのみ更新できます。 構文を更新するには、MySQL メタデータエクスプローラーペインでオブジェクトを選択し、[ **sql** ] タブをクリックして、sql コードを変更します。 項目から移動すると、更新された構文を保存するように求められます。 [ **レポート** ] タブでは、オブジェクトについて報告されたエラーを表示できます。  
  
-   MySQL では、問題のあるコードを削除または修正するために MySQL オブジェクトを変更できます。 更新されたコードを SSMA に読み込むには、メタデータを更新する必要があります。 詳細については、「 [MySQL への接続 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)」を参照してください。  
  
-   オブジェクトを移行から除外することができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または SQL Azure メタデータエクスプローラーおよび Mysql メタデータエクスプローラーで、項目の横のチェックボックスをオフにして、mysql からのオブジェクトの読み込み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure と移行を実行します。  
  
## <a name="next-step"></a>次の手順  
[MySQL データベース &#40;MySQLToSQL&#41;に変換しています ](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
## <a name="see-also"></a>参照  
[MySQL データベースを SQL Server Azure SQL Database &#40;MySQLToSql&#41;に移行する ](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
