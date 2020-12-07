---
description: Visual FoxPro データ ソースの追加
title: Visual FoxPro データソースの追加 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro data source [ODBC], adding
- adding data sources [ODBC], Visual FoxPro ODBC driver
ms.assetid: 1487e188-52c8-4f48-b4fe-25a650dd9e97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22ac95b51d543ca223148b169b53acb9c334d9f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494805"
---
# <a name="adding-a-visual-foxpro-data-source"></a>Visual FoxPro データ ソースの追加
アプリケーションから Visual FoxPro データにアクセスするには、データソースが必要です。 データソースは次のように作成できます。  
  
-   Microsoft® Word、Microsoft Excel、Microsoft Access などのアプリケーションで ODBC ドライバーを使用している。  
  
-   アプリケーションの外部で、Microsoft Windows®95、Microsoft Windows 98、または Microsoft Windows NT®/windows 2000 コントロールパネルを使用します。  
  
 システムにデータソースが存在した後、Visual FoxPro データにアクセスするたびに同じデータソースを再利用できます。 複数の異なるデータベースまたはテーブルにアクセスする場合は、データベースまたはディレクトリごとに個別のデータソースを作成できます。  
  
 次の手順では、コントロールパネルを使用してデータソースを作成します。 アプリケーションからデータソースを作成する方法の詳細については、「 [Microsoft Office からの Visual FoxPro データへのアクセス](../../odbc/microsoft/accessing-visual-foxpro-data-from-microsoft-office.md)」を参照してください。  
  
### <a name="to-add-a-visual-foxpro-data-source"></a>Visual FoxPro データソースを追加するには  
  
1.  Windows 2000 を実行しているコンピューターで、Windows のコントロールパネルを開き、[管理ツール] をダブルクリックします。  
  
2.  [データソース (ODBC)] をダブルクリックして、[ODBC データソースアドミニストレーター] ダイアログボックスを開きます。 このアイコンは、Visual FoxPro ODBC ドライバーまたは任意の ODBC ドライバーソフトウェアをインストールした後に使用できます。  
  
    > [!NOTE]  
    >  以前のバージョンの Windows を実行している場合は、Windows のコントロールパネルを開き、32ビットの ODBC または ODBC をダブルクリックして、[ODBC データソースアドミニストレーター] ダイアログボックスを開きます。  
  
3.  [追加] をクリックします。  
  
4.  [新しいデータソースの作成] ダイアログボックスで、[Microsoft Visual FoxPro ドライバー] を選択し、[完了] をクリックします。  
  
5.  [ [ODBC Visual FoxPro セットアップ] ダイアログボックス](../../odbc/microsoft/odbc-visual-foxpro-setup-dialog-box.md)で、データソースの名前と説明を入力し、データベースの種類を選択して、データベースまたはディレクトリを選択し、[OK] をクリックします。  
  
     新しいデータソース名は、[ODBC データソースアドミニストレーター] ダイアログボックスの [ユーザー DSN] タブにある [ユーザーデータソース] ボックスの一覧に表示されます。  
  
6.  [OK] をクリックして新しいデータソースを保存し、[ODBC データソースアドミニストレーター] ダイアログボックスを閉じます。
