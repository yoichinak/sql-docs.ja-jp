---
title: トレース テンプレートを作成する
titleSuffix: SQL Server Profiler
description: SQL Server Profiler で新しいトレース テンプレートを作成する方法について説明します。 テンプレートにフィルターを追加する方法と、イベントとデータ列を追加または削除する方法について説明します。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 025868b0-3790-4cda-8757-5a58327bfba0
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 453989e908808e0444807bcfb9dd817b3f79c436
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100349359"
---
# <a name="create-a-trace-template-sql-server-profiler"></a>トレース テンプレートの作成 (SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このトピックでは、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]を使用して新しいトレース テンプレートを作成する方法について説明します。  
  
### <a name="to-create-a-trace-template"></a>トレース テンプレートを作成するには  
  
1.  **[ファイル]** メニューの **[テンプレート]** をポイントし、 **[新しいテンプレート]** をクリックします。  
  
2.  **[トレース テンプレートのプロパティ]** ダイアログ ボックスで、 **[サーバーの種類の選択]** ボックスの一覧でサーバーの種類を選択します。  
  
3.  **[新しいテンプレート名]** ボックスにテンプレート名を入力します。  
  
4.  必要に応じて、 **[既存のテンプレートを基に新しいテンプレートを作成する]** をクリックし、一覧からテンプレートを選択します。  
  
     すべてのイベント、データ列、フィルターは、最初、選択したテンプレートで指定されたとおりに設定されています。  
  
5.  必要に応じて、 **[選択したサーバーの種類に対する既定のテンプレートとして使用する]** をクリックします。  
  
6.  **[イベントの選択]** タブで、イベント、データ列、またはフィルターの追加、削除、変更を行います。  
  
7.  **[イベントの選択]** タブで、グリッド コントロールを使用して、次のようにトレース ファイルに対するイベントとデータ列の追加または削除を行います。  
  
    -   イベントを追加するには、 **[イベント]** 列の適切なイベント カテゴリを展開し、イベント名を選択します。  
  
    -   イベントを追加すると、関連するすべてのデータ列が既定で含まれます。 トレースからイベントのデータ列を削除するには、そのイベントのデータ列のチェック ボックスをオフにします。  
  
    -   フィルターを追加するには、データ列名をクリックし、 **[フィルターの編集]** ダイアログ ボックスにフィルターの条件を指定します。 また、データ列名を右クリックし、 **[列フィルターの編集]** をクリックすることによっても **[フィルターの編集]** ダイアログ ボックスを起動できます。 **[OK]** をクリックしてフィルターを追加します。  
  
8.  **[保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [トレース ファイルに含めるイベントとデータ列の指定 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)   
 [実行中のトレースからのテンプレートの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-running-trace-sql-server-profiler.md)   
 [トレース ファイルまたはトレース テーブルからのテンプレートの作成 &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/derive-a-template-from-a-trace-file-or-trace-table-sql-server-profiler.md)   
 [SQL Server プロファイラーのテンプレートと権限](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
