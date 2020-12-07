---
description: '[クエリの定義が異なります] ダイアログ ボックス (Visual Database Tools)'
title: '[クエリの定義が異なります] ダイアログ ボックス'
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:69639
- vdtsql.chm:69640
- vdt.dlgbox.querydefinitionsdiffer
ms.assetid: 90383473-2922-40e5-9682-3850849aa856
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: a2517d930333f9a17e7746db29074456281ecf9d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88313858"
---
# <a name="query-definitions-differ-dialog-box-visual-database-tools"></a>[クエリの定義が異なります] ダイアログ ボックス (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
このダイアログ ボックスは、クエリがダイアグラム ペインおよび抽出条件ペインでグラフィカルに表示できず、SQL ペインでしか編集できないことを通知します。  
  
SQL ペインで SQL ステートメントを入力または編集してから、別のペインに移動するか、クエリを検査するか、またはクエリを実行しようとしたときに、次の条件のいずれかが当てはまる場合に表示されます。  
  
-   SQL ステートメントが不完全であるか、構文エラーがある。  
  
-   SQL ステートメントは有効だが、グラフィカル ペインでサポートされていない (Union クエリなど)。  
  
-   SQL ステートメントは有効だが、使用しているデータ接続に固有の構文が含まれている。  
  
> [!TIP]  
> **[クエリ]** ツール バーの **[SQL 構文の確認]** ボタンを使用すると、ステートメントが有効かどうかを確認できます。  
  
ダイアログ ボックスには、SQL ステートメントが表示できない理由を示すメッセージが表示され、どのように処理するかの決定が求められます。  
  
> [!NOTE]  
> ダイアグラム ペインおよび抽出条件ペインが非表示になっている場合、 **[クエリの定義が異なります]** ダイアログ ボックスは表示されません。  
  
## <a name="options"></a>オプション  
**[無視] ボタン**  
SQL ステートメントを受け入れてさらに編集するか実行する場合は、このボタンをクリックします。 ステートメントを受け入れると、ダイアグラム ペインと抽出条件ペインが淡色表示になり、SQL ペインのステートメントを反映しないことが示されます。  
  
**[元に戻す] ボタン**  
SQL ペインへの変更を破棄する場合は、このボタンを選択します。  
  
> [!NOTE]  
> ステートメントが正しいにもかかわらずクエリおよびビュー デザイナーによってグラフィカルにサポートされない場合は、ダイアグラム ペインと抽出条件ペインには表示されませんが、実行することはできます。 たとえば、Union クエリを入力した場合、ステートメントは実行できますが、他のペインには表示されません。  
  
## <a name="see-also"></a>参照  
[クエリおよびビュー デザイナー ツール (Visual Database Tools)](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)  
  
