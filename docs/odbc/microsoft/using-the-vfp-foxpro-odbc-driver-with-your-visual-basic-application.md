---
description: Visual Basic アプリケーションでの VFP FoxPro ODBC ドライバーの使用
title: Visual Basic アプリケーションで VFP FoxPro ODBC ドライバーを使用する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], visual basic applications
- Visual Basic applications [ODBC]
- FoxPro ODBC driver [ODBC], visual basic applications
- Visual FoxPro data [ODBC], visual basic applications
ms.assetid: 5223ca23-5df6-4ebc-aa3b-70682ff27a8c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07ec83ccab43890bccbf5e12582628fdb98d29c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500055"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Visual Basic アプリケーションでの VFP FoxPro ODBC ドライバーの使用
Microsoft® Visual Basic®アプリケーションは、Visual FoxPro データソースに接続するデータコントロールを作成することによって、Visual FoxPro データと通信できます。  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>Visual Basic のデータコントロールを使用して Visual FoxPro データに接続するには  
  
1.  Visual FoxPro に含まれている TasTrade サンプルデータベースに接続する "test" という名前のデータソースを作成します。 既定の Visual FoxPro のインストールでは、次の場所に TasTrade サンプルデータベースが配置されます。  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  Visual Basic で、新しいフォームを作成し、テキストボックスとデータコントロールを配置します。  
  
3.  データコントロールの Connect プロパティを次のように変更します。  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  RecordsetType プロパティを次のように変更します。  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  "RecordSource" プロパティを次のように変更します。  
  
    ```  
    customer  
    ```  
  
6.  テキストボックスの DataSource プロパティを、データコントロールの既定の名前に変更します。  
  
    ```  
    data1  
    ```  
  
7.  テキストボックスの DataField プロパティを次のように変更します。  
  
    ```  
    customer_id  
    ```  
  
8.  フォームを実行し、データコントロールを使用して、Visual FoxPro TasTrade サンプルデータベースの customer id フィールドをスキップします。
