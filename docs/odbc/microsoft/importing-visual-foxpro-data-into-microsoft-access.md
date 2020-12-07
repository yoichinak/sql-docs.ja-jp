---
description: Visual FoxPro データの Microsoft Access へのインポート
title: Visual FoxPro データを Microsoft Access にインポートする |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], importing
ms.assetid: a3591295-0a76-4e3c-b4fa-8bd4f1cde705
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 38440ca61b8af951f201978013d30529b75a452b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449534"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Visual FoxPro データの Microsoft Access へのインポート
[インポート] オプションを使用して、Visual FoxPro データベースに格納されているデータを Microsoft Access データベースにインポートできます。  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Visual FoxPro データを Microsoft Access データベースにインポートするには  
  
1.  Microsoft Access データベースを開きます。  
  
2.  [ファイル] メニューの [外部データの取り込み]、[インポート] の順に選択します。  
  
3.  [インポート] ダイアログボックスの [ファイルの種類] ボックスの一覧で、[ODBC データベース] を選択します。  
  
4.  [SQL データソース] ダイアログボックスで、クエリを実行する FoxPro データに接続する Visual FoxPro データソースを選択し、[OK] をクリックします。  
  
5.  [オブジェクトのインポート] ダイアログボックスで、インポートする1つ以上のテーブルを選択し、[OK] をクリックします。 インポートした Visual FoxPro テーブルの名前は、Microsoft Access データベースの [テーブル] タブに表示されます。  
  
 これで、Microsoft Access を使用して、インポートした Visual FoxPro テーブルのデータを操作できるようになりました。 インポートするデータは、Visual FoxPro に格納されているデータのスナップショットです。インポートされたデータに加えた変更は、Visual FoxPro データソースには返されません。  
  
 Visual FoxPro データソースのデータを変更するために Microsoft Access で行った変更が必要な場合は、「 [Microsoft access からの Visual Foxpro データのクエリと更新](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md)」を参照してください。
