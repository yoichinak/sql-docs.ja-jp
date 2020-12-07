---
description: Microsoft Excel から Visual FoxPro データ ソースへのアクセス
title: Microsoft Excel からの Visual FoxPro データソースへのアクセス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], accessing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 2c143020-0403-4592-80e0-84229f3d40be
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ce4e3bf96a41918fff392117a2fbbd1b9eb47f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487575"
---
# <a name="accessing-a-visual-foxpro-data-source-from-microsoft-excel"></a>Microsoft Excel から Visual FoxPro データ ソースへのアクセス
Microsoft Query がインストールされている場合は、Visual FoxPro データに接続するデータソースを Microsoft Excel で作成できます。  
  
### <a name="to-access-visual-foxpro-data-from-microsoft-excel"></a>Microsoft Excel から Visual FoxPro データにアクセスするには  
  
1.  Microsoft Excel スプレッドシートを開きます。  
  
2.  [データ] メニューの [外部データの取り込み] をクリックします。 Microsoft Query が開きます。  
  
3.  [データソースの選択] ダイアログボックスで、[その他] をクリックします。  
  
4.  [ODBC データソース] ダイアログボックスで、[新規作成] をクリックします。  
  
5.  [データソースの追加] ダイアログボックスで、[インストールされている ODBC ドライバー] ボックスの一覧から [Microsoft Visual FoxPro Driver] を選択し、[OK] をクリックします。  
  
6.  [ [ODBC Visual FoxPro セットアップ] ダイアログボックス](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)で、データソース名を入力し、データベースの種類を選択して、データベースまたはディレクトリへのパスを入力し、[OK] をクリックします。  
  
     新しいデータソース名は、[ODBC データソース] ダイアログボックスの [データソースの入力] ボックスに表示されます。  
  
7.  [OK] をクリックします。  
  
     [データソースの選択] ダイアログボックスの [使用できるデータソース] ボックスで、新しいデータソース名が選択されます。  
  
8.  [使用] をクリックします。  
  
 開いているクエリにテーブルを追加できるようになりました。 クエリの作成の詳細については、「 [Visual FoxPro データベースから Microsoft Excel にデータをインポートする](../../odbc/microsoft/importing-data-into-microsoft-excel-from-a-visual-foxpro-database.md)」を参照してください。
