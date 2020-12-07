---
description: '[データのプレビュー] ダイアログ ボックス (SQL Server インポートおよびエクスポート ウィザード)'
title: '[データのプレビュー] ダイアログ ボックス (SQL Server インポートおよびエクスポート ウィザード) | Microsoft Docs'
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.previewdata.f1
ms.assetid: 423ac26a-ba02-4fdf-88b4-07995fe4a97e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4608eed330a6ac8a64150197a591f68fcc832c65
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88347218"
---
# <a name="preview-data-dialog-box-sql-server-import-and-export-wizard"></a>[データのプレビュー] ダイアログ ボックス (SQL Server インポートおよびエクスポート ウィザード)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  コピーするデータを指定した後に、必要に応じて **[プレビュー]** をクリックして **[データのプレビュー]** ダイアログ ボックスを開くことができます。 このページでは、データ ソースから最大 200 行のサンプル データをプレビューできます。 プレビューで、コピーしたいデータがウィザードによってコピーされることを確認します。
  
## <a name="screen-shot-of-the-preview-data-page"></a>[データのプレビュー] ページのスクリーン ショット 
 次のスクリーン ショットは、ウィザードの **[データのプレビュー]** ダイアログ ボックスです。  
 
![インポートおよびエクスポート ウィザードの [データのプレビュー] ページ](../../integration-services/import-export-data/media/preview-data.png "インポートおよびエクスポート ウィザードの [データのプレビュー] ページ")  
  
## <a name="preview-sample-data"></a>サンプル データのプレビュー  
 **ソース**  
ウィザードがデータ ソースからデータを読み込むために使用しているクエリが表示されます。

コピーするテーブルを選択すると、**[ソース]** フィールドに、テーブル名の代わりに `SELECT * FROM <table>` クエリが表示されます。 
  
 **[サンプル データ グリッド]**  
 クエリから返されたデータ ソースのサンプル データが最大 200 行表示されます。  


## <a name="thats-not-right-i-want-to-change-something"></a>これは不正で、何かを変更したいです
データをプレビューした後で、ウィザードの前のページで選択したオプションを変更してもかまいません。 これらの変更を行うには、**[OK]** をクリックして **[コピー元のテーブルおよびビューを選択]** ページに戻り、**[戻る]** をクリックし、選択の変更が可能な前のページに戻ります。

## <a name="whats-next"></a>次の手順  
 コピーするデータをプレビューしたら、 **[OK]** をクリックします。 **[データのプレビュー]** ダイアログ ボックスから、 **[コピー元のテーブルおよびビューを選択]** ページまたは **[フラット ファイルの変換先の構成]** ページに戻ります。 詳細については、「 [[コピー元のテーブルおよびビューを選択]](../../integration-services/import-export-data/select-source-tables-and-views-sql-server-import-and-export-wizard.md) 」または「 [[フラット ファイルの変換先の構成]](../../integration-services/import-export-data/configure-flat-file-destination-sql-server-import-and-export-wizard.md)」を参照してください。  
 
 ## <a name="see-also"></a>関連項目
[簡単な例によるインポートおよびエクスポート ウィザードの概要](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)
