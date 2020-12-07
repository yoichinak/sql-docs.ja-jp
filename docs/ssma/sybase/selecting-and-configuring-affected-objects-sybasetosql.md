---
description: 影響を受けるオブジェクトの選択と構成 (SybaseToSQL)
title: 影響を受けるオブジェクトの選択と構成 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Tester Component,Affected Objects
ms.assetid: a219df74-543a-4aec-aeeb-79f90ac3e2ee
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 793430d548053b8d4c1cbf8dd07dd4e7d691c6d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88468744"
---
# <a name="selecting-and-configuring-affected-objects-sybasetosql"></a>影響を受けるオブジェクトの選択と構成 (SybaseToSQL)
このページでは、前の手順で選択したオブジェクトの実行結果が SSMA によって検証されるときに、テーブルと外部キーを選択できます。また、これらの変更を比較する必要があります。 また、検証パラメーターをカスタマイズすることもできます。  
  
## <a name="selection-of-affected-objects"></a>影響を受けるオブジェクトの選択  
ウィンドウの左側にある Sybase オブジェクトツリーで、テーブルと外部キーを確認します。変更内容は、同一であるかどうかを比較する必要があります。  
  
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
  
## <a name="table-comparison-settings"></a>テーブルの比較の設定  
**テーブル比較**ページのテーブルの比較規則を設定します。 次の設定を行うことができます。  
  
### <a name="comparison-mode"></a>比較モード  
が比較を実行するテーブルの内容を定義します。  
  
-   [ **変更のみ**] を選択した場合は、テーブル行の完全な比較が実行されます。  
  
-   [ **完全**] を選択した場合は、変更された行のみの比較が実行されます。  
  
## <a name="column-comparison-settings"></a>列の比較の設定  
[ **列の比較** ] ページで、テーブルの列の比較規則を設定します。 次の設定を行うことができます。  
  
### <a name="use-during-test-comparisons"></a>テストの比較中に使用  
この列がテスト結果の検証に参加するかどうかを判断します。  
  
-   **True**を選択した場合、ssma は、Sybase でテストを実行した後に、SQL Server の列の内容を使用して、この列の内容を比較します。
  
-   [ **False**] を選択した場合、列は結果の検証から除外されます。  
  
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
SSMA Tester によって生成された SELECT ステートメントは、[ **SQL の比較** ] ページで確認できます。 テスト担当者は、これらのステートメントの結果セットを行ごとに比較します。 Sybase の結果セットの次の行は、で生成された結果セットの次の行と同じである必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
これらの SELECT ステートメントを編集して、カスタム検証を行うことができます。 Sybase およびステートメントで変更を保存するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ソースとターゲットの SQL の下にある [ **適用** ] ボタンを使用します。  
  
## <a name="next-step"></a>次の手順  
[呼び出し順序のカスタマイズ &#40;SybaseToSQL&#41;](../../ssma/sybase/customizing-calls-order-sybasetosql.md)  
  
## <a name="see-also"></a>参照  
[実行、テストケース &#40;SybaseToSQL&#41;](../../ssma/sybase/running-test-cases-sybasetosql.md)  
[&#40;SybaseToSQL&#41;の移行されたデータベースオブジェクトのテスト ](../../ssma/sybase/testing-migrated-database-objects-sybasetosql.md)  
  
