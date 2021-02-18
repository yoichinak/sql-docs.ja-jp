---
title: フィルターを変更する
titleSuffix: SQL Server Profiler
description: SQL Server Profiler でトレース フィルターを変更して、必要な情報を収集できるようにする方法について説明します。 トレース フィルターがデータベースのパフォーマンスに与える影響について説明します。
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 8b317813-4918-4485-b930-77b1951aa00c
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: dc2171ea2aaf418eae0fa277a8f4144dc4e7ca9d
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100345044"
---
# <a name="modify-a-filter-sql-server-profiler"></a>フィルターの変更 (SQL Server Profiler)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

トレース定義を保持するトレース テンプレートにフィルターを追加して、トレースで収集するイベントの数を制限します。 収集するイベントの数を制限すると、トレースによるパフォーマンスの影響を軽減できます。 トレース テンプレートにフィルターを設定していても、そのトレースで必要な種類の情報が収集されていないことが判明した場合は、そのフィルターを編集できます。  
  
### <a name="to-modify-a-filter"></a>フィルターを変更するには  
  
1.  [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]で、変更するトレース フィルターのテンプレートを開きます。 **[ファイル]** メニューの **[テンプレート]** をポイントし、 **[テンプレートの編集]** をクリックします。  
  
2.  **[トレース テンプレートのプロパティ]** ダイアログ ボックスの **[全般]** タブで、 **[テンプレート名の選択]** ボックスの一覧からテンプレートを選択します。  
  
3.  **[イベントの選択]** タブをクリックします。  
  
     **[イベントの選択]** タブにはグリッド コントロールがあります。 グリッド コントロールは、トレース可能な各イベント クラスを含んでいるテーブルです。 このテーブルには、各イベント クラスが 1 行で表示されます。 イベント クラスは、接続先のサーバーの種類やバージョンによって多少異なる場合があります。 イベント クラスは、グリッドの **[イベント]** 列で識別され、イベント カテゴリ別に分類されています。 残りの列には、各イベント クラスに対応するデータ列が表示されます。  
  
4.  **[列フィルター]** をクリックします。  
  
5.  **[フィルターの編集]** ダイアログ ボックスで、編集する比較演算子に対応した値をクリックし、新しい値を入力するか、既存の値を削除します。 また、新しいフィルターを追加することもできます。  
  
6.  **[OK]** をクリックしてテンプレートを保存します。  
  
## <a name="see-also"></a>参照  
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
