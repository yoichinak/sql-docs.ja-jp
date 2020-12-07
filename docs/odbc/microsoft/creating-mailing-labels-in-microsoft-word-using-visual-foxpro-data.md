---
description: Visual FoxPro データを使用した Microsoft Word での宛名ラベルの作成
title: Visual FoxPro データを使用して Microsoft Word で宛名ラベルを作成する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data [ODBC], mailing labels
- Visual FoxPro data [ODBC], Word
- mailing labels [ODBC]
- Visual FoxPro ODBC driver [ODBC], Word
- FoxPro ODBC driver [ODBC], word
ms.assetid: c901b60c-9f84-407a-b3d1-b4d301a71370
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b70bed514893ab719b1f982f0facde9669e137a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471613"
---
# <a name="creating-mailing-labels-in-microsoft-word-using-visual-foxpro-data"></a>Visual FoxPro データを使用した Microsoft Word での宛名ラベルの作成
Visual FoxPro データは、Microsoft Word for Windows 95 または Windows 98 ドキュメントで使用できます。 たとえば、Visual FoxPro テーブルに格納されている顧客情報から宛名ラベルを作成することができます。  
  
### <a name="to-create-mailing-labels"></a>宛名ラベルを作成するには  
  
1.  Microsoft Word で、新しい空のドキュメントを作成します。  
  
2.  [ツール] メニューの [メールのマージ] をクリックします。  
  
3.  メールマージヘルパーで、[作成] を選択し、[メーリングラベル] を選択します。  
  
4.  メインドキュメントで、[アクティブウィンドウ] を選択します。  
  
5.  [データソース] の [データの取得] をクリックし、[データソースを開く] を選択します。  
  
6.  [データソースを開く] ダイアログボックスで、[MS クエリ] を選択します。  
  
7.  [データソースの選択] ダイアログボックスで、Visual FoxPro データソースを選択し、[使用] をクリックします。  
  
8.  データソースによってアクセスされるデータベースにテーブルが含まれている場合は、[テーブルの追加] ダイアログボックスでテーブルを選択します。 Microsoft Query では、クエリデザイナーの上半分に追加したテーブルが表示されます。  
  
9. テーブルからデザイナーの下半分にクエリをドラッグして、クエリのフィールドを選択します。  
  
10. [ファイル] メニューの [Microsoft Word にデータを返す] を選択します。 Microsoft Query が終了します。選択したデータは、差し込み印刷ドキュメントで使用できます。  
  
11. メインドキュメントで、[セットアップ] を選択します。  
  
12. [ラベルのオプション] ダイアログボックスで、必要なプリンターとラベル情報を選択し、[OK] をクリックします。  
  
13. [ラベルの作成] ダイアログボックスで、宛名ラベルに印刷するフィールドを選択し、[OK] をクリックします。  
  
14. メールマージヘルパーの [ドキュメントとデータをマージ] の下にある [マージ] をクリックします。  
  
15. [マージ] ダイアログボックスで、必要なオプションを選択し、[マージ] をクリックします。
