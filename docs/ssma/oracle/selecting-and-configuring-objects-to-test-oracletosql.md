---
description: テストするオブジェクトの選択と構成 (OracleToSQL)
title: テストするオブジェクトの選択と構成 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Selection of Objects to Test,Parameter Comparison Settings
ms.assetid: 29fb6542-5c1f-4b14-a822-87700beb7623
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: deb482c041dd290db3d2a7c911fb7d3663aa819a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418338"
---
# <a name="selecting-and-configuring-objects-to-test-oracletosql"></a>テストするオブジェクトの選択と構成 (OracleToSQL)
このステップでは、テスト対象のオブジェクトを選択し、プロシージャの出力パラメーターと関数の戻り値を比較するための設定を構成します。  
  
## <a name="selection-of-objects-to-test"></a>テストするオブジェクトの選択  
ウィンドウの左側にある Oracle オブジェクトツリーで、テストプロセス中に呼び出すオブジェクトを確認します。 「移行された [データベースオブジェクト &#40;OracleToSQL&#41;のテスト ](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md) 」トピックのテスト可能オブジェクトの完全な一覧については、「」を参照してください。  
  
SSMA Tester がテスト用に選択されたオブジェクトのいずれかをサポートしていない場合は、 **選択したオブジェクトの中** に [オブジェクト] ツリーの下にエラーが含まれているというリンクが表示されます。 このリンクをクリックすると、これらのオブジェクトをテストできない理由が表示され、間違ったオブジェクトの選択を解除できます。  
  
右側では、複数のページを表示できます。 **SQL** ページには、現在のオブジェクトの定義が表示されています。 オブジェクトがストアドプロシージャまたは関数の **場合、パラメーターページに** はパラメーターが一覧表示されます。 [ **プロパティ** ] ページには、オブジェクトのその他の特性が表示されます。 次の「 **パラメーター比較** 」と「 **呼び出し値** 」のページの説明を参照してください。  
  
## <a name="parameter-comparison-settings"></a>パラメーター比較の設定  
[ **パラメーター比較** ] ページで、出力パラメーターと戻り値の比較規則を設定します。 次の設定を行うことができます。  
  
### <a name="use-during-test-comparisons"></a>テストの比較中に使用  
テスト結果の比較で、選択したパラメーターの使用を有効にします。  
  
-   **True**を選択した場合、ssma は、Oracle でプロシージャを実行した後に、SQL Server に対応する値を使用して、このパラメーターの出力値を比較します。
  
-   **False**を選択した場合、パラメーターは結果の検証から除外されます。  
  
### <a name="use-custom-scale"></a>カスタムスケールを使用する  
数値データ型のパラメーターの場合は、比較のカスタムスケールを設定できます。  
  
-   **True**を選択すると、比較する前に、比較する**スケール**値に従って数値が丸められます。  
  
-   **False**を選択した場合は、数値比較が正確になります。  
  
### <a name="comparing-scale"></a>比較 (スケールを)  
[ **カスタムスケールを使用** する] オプションが **True**に設定されている場合にのみ使用できます。 これは、数値比較の有効桁数です。  
  
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
  
-   **False**を選択した場合、比較では大文字と小文字が区別されます。  
  
### <a name="ignore-trailing-spaces"></a>[末尾のスペースを無視する]  
比較中に末尾のスペースを処理する方法を制御します。  
  
-   [ **True**] を選択した場合、比較対象の文字列は、比較の前に右から右にトリミングされます。  
  
-   **False**を選択した場合、比較対象の文字列では末尾の空白が保持されます。  
  
## <a name="specify-input-values-for-procedures-and-functions-call-values"></a>プロシージャと関数の入力値を指定する (呼び出し値)  
[ **呼び出しの値** ] ページで入力パラメーターの値を指定できます。 [ **呼び出しの追加** ] ボタンをクリックすると、空のパラメーター値を持つ新しい呼び出しが追加されます。 [ **呼び出しの削除** ] ボタンをクリックすると、現在の呼び出しが削除されます。  
  
## <a name="next-step"></a>次の手順  
[影響を受けるオブジェクトの選択と構成 &#40;OracleToSQL&#41;](../../ssma/oracle/selecting-and-configuring-affected-objects-oracletosql.md)  
  
## <a name="see-also"></a>参照  
[移行されたデータベースオブジェクト &#40;OracleToSQL&#41;のテスト ](../../ssma/oracle/testing-migrated-database-objects-oracletosql.md)  
  
