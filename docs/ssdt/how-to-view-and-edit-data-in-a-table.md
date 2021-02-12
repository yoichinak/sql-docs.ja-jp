---
title: テーブル内のデータを表示および編集する
description: データ エディターを使用して既存のテーブルのデータを表示、編集、削除する方法について説明します。 変更をスクリプト フォームに表示してスクリプト ファイルに保存する方法を確認します。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.QUERYRESULTS.F1
- sql.data.tools.queryresults.executequerydeletingrow
ms.assetid: bb67ce83-a87a-4e14-84cd-9a5930fe74c8
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: ebe23b534590bfb45c4a0bffce78d2139ef8912c
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100017992"
---
# <a name="how-to-view-and-edit-data-in-a-table"></a>方法:テーブル内のデータを表示および編集する

ビジュアル データ エディターを使用すると、既存のテーブルのデータを表示、編集、および削除できます。  
  
> [!WARNING]  
> 以下に示す手順では、「[接続されているデータベース開発](../ssdt/connected-database-development.md)」に示されているこれまでの手順で作成したエンティティを使用します。  
  
### <a name="to-edit-data-in-a-table-visually-using-the-data-editor"></a>データ エディターを使用してテーブル内のデータを視覚的に編集するには  
  
1.  **SQL Server オブジェクト エクスプローラー** で **Products** テーブルを右クリックして、 **[データの表示]** をクリックします。  
  
2.  データ エディターが起動します。 これまでの手順でテーブルに追加した行を確認します。  
  
3.  SQL Server オブジェクト エクスプローラーで **Fruits** テーブルを右クリックして、 **[データの表示]** をクリックします。  
  
4.  データ エディターで、**Id** に「**1**」、**Perishable** に「**True**」と入力し、Enter キーまたは Tab キーでフォーカスを新しい行から移動して、データベースにコミットします。  
  
5.  前の手順を繰り返して、「**2**」と「**False**」および「**3**」と「**False**」をテーブルに入力します。  
  
    行を編集する際には、Esc キーを押すことで、セルに対する変更をいつでも元に戻すことができます。  
  
6.  ツール バーの **[スクリプト]** をクリックすると、編集内容をスクリプトとして表示できます。 または、 **[スクリプトをファイルに保存]** を使用して .sql スクリプト ファイルに保存し、後で実行することもできます。  
  
7.  **SQL Server オブジェクト エクスプローラー** で **Trade** データベースを右クリックし、 **[新しいクエリ]** をクリックします。 エディターで、「`select * from dbo.PerishableFruits`」と入力して **[クエリの実行]** をクリックすると、データが `PerishableFruits` ビューとして返されます。  
  
