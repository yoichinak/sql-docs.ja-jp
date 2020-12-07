---
title: Management Studio の [プロパティ] ウィンドウの使用
description: '[プロパティ] ウィンドウを使用して、接続などの SQL Server Management Studio の項目とデータベース オブジェクトに関する情報を表示する方法について説明します。'
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- viewing properties
- Properties window [SQL Server Management Studio]
- complex properties [SQL Server Management Studio]
ms.assetid: 903d4aca-f57c-43d9-a893-702eceaa7004
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bd4bcf579688bd00c845a9c51a724e623805daf7
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036095"
---
# <a name="use-the-properties-window-in-management-studio"></a>Management Studio の [プロパティ] ウィンドウの使用
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  [プロパティ] ウィンドウには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]内の項目 (接続、プラン表示操作など) の状態や、データベース オブジェクト (テーブル、ビュー、デザイナーなど) の情報が表示されます。  
  
 [プロパティ] ウィンドウを使用して、現在の接続のプロパティを表示できます。 [プロパティ] ウィンドウに表示される多くのプロパティは読み取り専用ですが、 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]内の別の場所で変更できます。 たとえば、[プロパティ] ウィンドウに表示されるクエリの [データベース] プロパティは読み取り専用ですが、ツール バーからの変更が可能です。  
  
### <a name="to-view-properties-using-the-properties-window"></a>[プロパティ] ウィンドウを使用してプロパティを表示するには  
  
1.  [プロパティ] ウィンドウが表示されていない場合は、 **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックするか、F4 キーを押します。  
  
2.  表示するオブジェクトにフォーカスを設定します。  
  
3.  [プロパティ] ウィンドウで特定のプロパティを探します。  
  
### <a name="to-view-connection-properties-of-a-query-window"></a>クエリ ウィンドウの接続プロパティを表示するには  
  
1.  [プロパティ] ウィンドウが表示されていない場合は、 **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックするか、F4 キーを押します。  
  
2.  [プロパティ] ウィンドウですべての接続プロパティを確認できます。  
  
### <a name="to-view-the-properties-of-a-showplan-operator"></a>プラン表示操作のプロパティを表示するには  
  
1.  **[クエリ]** メニューの **[実際の実行プランを含める]** をクリックします。  
  
2.  SQL クエリ エディターで、クエリを入力して実行します。  
  
3.  [プロパティ] ウィンドウが表示されていない場合は、 **[表示]** メニューの **[プロパティ ウィンドウ]** をクリックするか、F4 キーを押します。  
  
4.  SQL クエリ エディターの **[実行プラン]** タブでオペレーターのアイコンをクリックすると、[プロパティ] ウィンドウにそのオペレーターの情報が表示されます。  
  
## <a name="see-also"></a>参照  
 [[プロパティ] ウィンドウ &#40;Management Studio&#41;](../properties-window-management-studio.md)  
  
