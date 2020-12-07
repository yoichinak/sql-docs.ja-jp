---
description: 変換のための SAP ASE データベースオブジェクトの評価 (SybaseToSQL)
title: 変換のための SAP ASE データベースオブジェクトの評価 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 12/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eb996b7c-1eef-4f73-b5e6-2fa6faf7336c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6e8bd25b8529f09896cbec2ec31578375a015f2a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88372629"
---
# <a name="assessing-sap-ase-database-objects-for-conversion-sybasetosql"></a>変換のための SAP ASE データベースオブジェクトの評価 (SybaseToSQL)
オブジェクトを読み込んで、または Azure SQL にデータを移行する前に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、移行の複雑さと所要時間を決定する必要があります。 SSMA では、に正常に変換されるオブジェクトとプロシージャの割合を示す評価レポートを作成でき [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。 SSMA では、変換エラーの原因となる可能性のある特定の問題を確認することもできます。  
  
## <a name="create-assessment-reports"></a>評価レポートの作成  
この評価レポートを作成すると、SSMA は、選択した SAP Adaptive Server Enterprise (ASE) データベースオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または AZURE SQL 構文に変換し、結果を表示します。  
  
**評価レポートを作成するには**  
  
1.  Sybase メタデータエクスプローラーで、評価するデータベースを選択します。  
  
2.  個々のオブジェクトを省略するには、評価しないオブジェクトの横にあるチェックボックスをオフにします。  
  
3.  [ **データベース**] を右クリックし、[ **レポートの作成**] を選択します。  
  
    オブジェクトを右クリックし、[ **レポートの作成**] を選択して、個々のオブジェクトを分析することもできます。  
  
    SSMA は、ウィンドウの下部にあるステータスバーに進行状況を表示します。 出力ウィンドウが表示されている場合は、関連するメッセージも表示されます。  
  
    評価が完了すると、[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Sybase: 評価レポートの Migration Assistant] ウィンドウが表示されます。  
  
## <a name="use-assessment-reports"></a>評価レポートの使用  
[評価レポート] ウィンドウには、次の3つのペインがあります。  
  
-   左側のウィンドウには、評価レポートに含まれるオブジェクトの階層が表示されます。 階層を参照してオブジェクトとオブジェクトカテゴリを選択すると、変換の統計情報とコードを表示できます。  
  
-   右側のウィンドウの内容は、左側のウィンドウで選択した項目によって異なります。  
  
    オブジェクトのグループ (スキーマなど) またはテーブルが選択されている場合、右側のペインには2つのペインが表示されます。 [ **変換統計** ] ペインには、選択したオブジェクトの変換統計が表示されます。 [ **カテゴリ別のオブジェクト** ] ペインには、オブジェクトまたはオブジェクトのカテゴリの変換統計が表示されます。  
  
    ストアドプロシージャ、ビュー、またはトリガーが選択されている場合、右側のペインには統計、ソースコード、およびターゲットコードが表示されます。  
  
    -   上の領域には、オブジェクトの全体的な統計が表示されます。 この情報を表示するには、 **統計** の展開が必要になる場合があります。 
    -   [ソース] 領域には、左ペインで選択したオブジェクトのソースコードが表示されます。 強調表示された領域には、問題のあるソースコードが表示されます。  
    -   ターゲット領域には、変換されたコードが表示されます。 赤いテキストは、問題のあるコードとエラーメッセージを示しています。  
  
-   下部のペインには、メッセージ番号でグループ化された変換メッセージが表示されます。 [ **エラー**]、[ **警告**]、または [ **情報** ] を選択して、メッセージのカテゴリを表示し、メッセージのグループを展開します。 個々のメッセージをクリックして左ペインでオブジェクトを選択し、右側のウィンドウに詳細を表示します。  
  
## <a name="analyze-conversion-problems-by-using-the-assessment-report"></a>評価レポートを使用して変換の問題を分析する  
変換統計 **ペイン** には、変換の統計情報が表示されます。 いずれかのカテゴリの割合が100% 未満の場合は、変換が成功しなかった理由を判断する必要があります。  
  
**変換の問題を表示するには**  
  
1.  前の手順の指示に従って、評価レポートを作成します。  
  
2.  左側のウィンドウで、[スキーマ] または赤色のエラーアイコンが表示されているフォルダーを展開します。 変換に失敗した個々の項目を選択するまで、項目を展開し続けます。  
  
3.  ソースペインの上部にある [次の **問題**] を選択します。  
    **ターゲットナビゲーション**ウィンドウの関連コードと同様に、問題のあるコードが強調表示されます。  
  
4.  エラーメッセージを確認し、変換の問題の原因となったオブジェクトで何を実行するかを決定します。  
  
    -   SSMA の ASE 構文を更新します。 構文は、ストアドプロシージャとトリガーに対してのみ更新できます。 構文を更新するには、Sybase メタデータエクスプローラーペインでオブジェクトを選択し、[ **sql** ] タブをクリックして、sql コードを編集します。 項目から移動すると、更新された構文を保存するように求められます。 [ **レポート** ] タブで、オブジェクトについて報告されたエラーを表示します。  
  
    -   ASE では、ASE オブジェクトを変更して、問題のあるコードを削除または修正できます。 更新されたコードを SSMA に読み込むには、メタデータを更新する必要があります。 詳細については、「 [SYBASE ASE &#40;SybaseToSQL&#41;への接続 ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)」を参照してください。  
  
    -   オブジェクトを移行から除外することができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]または AZURE Sql Metadata explorer と Sybase メタデータエクスプローラーで、オブジェクトをまたは AZURE sql に読み込む前に項目の横のチェックボックスをオフにし、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ASE からデータを移行します。
  
## <a name="next-steps"></a>次の手順  
[SAP ASE データベースオブジェクトの &#40;SybaseToSQL&#41;への変換 ](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md)  
  
## <a name="see-also"></a>参照  
[SAP ASE データベースの SQL Server Azure SQL Database &#40;SybaseToSQL&#41;への移行 ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
