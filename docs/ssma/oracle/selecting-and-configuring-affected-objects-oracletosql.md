---
description: 影響を受けるオブジェクトの選択と構成 (OracleToSQL)
title: 影響を受けるオブジェクトの選択と構成 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Columns Comparison Settings
- Selection of Affected Objects
ms.assetid: 545eeda2-9829-4187-a858-619a96b4b71d
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 5cd9ca7c8789133fdbccc3367f3bda121d2499ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418348"
---
# <a name="selecting-and-configuring-affected-objects-oracletosql"></a>影響を受けるオブジェクトの選択と構成 (OracleToSQL)
このページでは、前の手順で選択したオブジェクトの実行結果が SSMA によって検証されるときに、テーブルと外部キーを選択できます。また、これらの変更を比較する必要があります。 また、検証パラメーターをカスタマイズすることもできます。  
  
## <a name="selection-of-affected-objects"></a>影響を受けるオブジェクトの選択  
ウィンドウの左側にある Oracle オブジェクトツリーで、テーブルと外部キーを確認します。変更内容は、同一であるかどうかを比較する必要があります。  
  
SSMA Tester がこれらのオブジェクトのいずれかを確認できない場合は、 **選択したオブジェクトの中** に [オブジェクト] ツリーの下にエラーが含まれているというリンクが表示されます。 このリンクをクリックすると、これらのオブジェクトを比較できない理由が表示され、間違ったオブジェクトの選択を解除できます。  
  
## <a name="table"></a>テーブル  
[テーブル] タブには、選択したテーブルのグリッドビューが表示されます。 グリッドには、選択したテーブルに関する次の情報が表示されます。  
  
-   列名  
  
-   データ型  
  
-   有効桁数  
  
-   スケール  
  
-   ルール  
  
-   Default  
  
-   ID  
  
-   Nullable  
  
## <a name="sql"></a>Sql  
[SQL] タブには、選択したテーブルの "Create table" SQL が含まれています。  
  
## <a name="data"></a>データ  
[データ] タブ選択したテーブルに存在するデータが表示されます。  
  
## <a name="properties"></a>プロパティ  
[プロパティ] タブ選択したテーブルのプロパティが表示されます。 [プロパティ] タブには、次のフィールドが表示されます。  
  
-   作成済みまたは最終変更日時  
  
-   オブジェクト名  
  
## <a name="columns-comparison-settings"></a>列の比較の設定  
**列比較**ページのテーブル列の比較規則を設定します。 次の設定を行うことができます。  
  
### <a name="use-during-test-comparisons"></a>テストの比較中に使用  
この列がテスト結果の検証に参加するかどうかを判断します。  
  
-   **True**を選択した場合、ssma は、SQL Server の列の内容を使用して、Oracle でテストを実行した後に、この列の内容を比較します。 
  
-   [**False**] を選択した場合、列は結果の検証から除外されます。  
  
### <a name="use-custom-scale"></a>カスタムスケールを使用する  
数値データ型の列の場合は、比較のカスタムスケールを設定できます。  
  
-   **True**を選択すると、比較する前に、比較する**スケール**値に従って数値が丸められます。  
  
-   **False**を選択した場合は、数値比較が正確になります。  
  
### <a name="comparing-scale"></a>比較 (スケールを)  
  
-   [ **カスタムスケールを使用** する] オプションが **True**に設定されている場合にのみ使用できます。 これは、数値比較の有効桁数です。  
  
### <a name="date-time-comparing"></a>日付と時刻の比較  
日付/時刻値の比較方法を定義します。  
  
-   [全体の **比較**] を選択すると、両方のプラットフォームの値の完全な比較が実行されます。  
  
-   [ **日付のみを比較**] を選択した場合、時刻部分は無視されます。  
  
-   [ **時間のみを比較**] を選択した場合、日付部分は無視されます。  
  
-   [ **ミリ秒を無視**する] を選択すると、結果は秒単位で比較されます。  
  
-   [ **日付とミリ秒を無視**する] を選択した場合、結果は時刻部分のみで比較され、秒の小数部は無視されます。  
  
### <a name="ignore-strings-case"></a>文字列を無視する大文字小文字を区別する  
比較の大文字と小文字の区別を制御します。  
  
-   **True**を選択した場合、比較では大文字と小文字が区別されません。  
  
-   **False**を選択した場合、比較では大文字と小文字の区別が考慮されます。  
  
## <a name="comparing-sql"></a>比較 (SQL を)  
SSMA Tester によって生成された SELECT ステートメントは、 **SQL の比較** ページで確認できます。 テスト担当者は、これらのステートメントの結果セットを行ごとに比較します。 Oracle の結果セットの次の行は、SQL Server で生成される結果セットの次の行と同じである必要があります。
  
これらの SELECT ステートメントを編集して、カスタム検証を行うことができます。 Oracle および SQL Server ステートメントで変更を保存するには、ソースとターゲットの SQL の下にある [ **適用** ] ボタンを使用します。  
  
## <a name="next-step"></a>次の手順  
[呼び出し順序のカスタマイズ &#40;OracleToSQL&#41;](../../ssma/oracle/customizing-calls-order-oracletosql.md)  
  
## <a name="see-also"></a>参照  
[テストケースの準備 &#40;OracleToSQL&#41;を終了しています ](../../ssma/oracle/finishing-test-case-preparation-oracletosql.md)  
[OracleToSQL&#41;&#40;のテストケースの実行 ](../../ssma/oracle/running-test-cases-oracletosql.md)  
[移行されたデータベースオブジェクト &#40;OracleToSQL&#41;のテスト ](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
