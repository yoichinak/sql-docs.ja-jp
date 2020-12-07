---
description: ミラー テーブルおよび CDC キャプチャ インスタンスの生成
title: ミラー テーブルおよび CDC キャプチャ インスタンスの生成 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- mirTab
ms.assetid: 260c1617-eecc-4007-a84d-3c5778ce46b6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9f8340ef153f815d3073edaf4f9a13e99e1e9f67
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88394808"
---
# <a name="generate-mirror-tables-and-cdc-capture-instances"></a>ミラー テーブルおよび CDC キャプチャ インスタンスの生成

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  [ミラー テーブルの生成] ページを使用すると、CDC インスタンスに含めたテーブルのミラー テーブルを生成できます。  
  
 **[実行]** をクリックするとミラー テーブルが作成されます。 テーブルごとに作成の進行状況が表示され、各ミラー テーブルの作成が正常に終了したか、エラーが発生したかを通知するメッセージが表示されます。 エラーが発生した場合は、 **[詳細]** をクリックしてエラーについて説明するダイアログ ボックスを表示します。  
  
 テーブルの作成に失敗した場合は、そのまま続行するか、または失敗したテーブルを削除してから続行するかを選択できます。 ウィザードの実行が終了したら、Oracle ソース データベースでテーブルを修正するか、CDC インスタンスでそのテーブルを使用しないようにするかを選択できます。 テーブルを修正する場合は、 [Edit Tables](../../integration-services/change-data-capture/edit-tables.md)を行うときにそのテーブルを追加できます。  
  
 **[次へ]** をクリックして [Finish](../../integration-services/change-data-capture/finish.md) ページを開きます。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server 変更データベース インスタンスを作成する方法](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)  
  
  
