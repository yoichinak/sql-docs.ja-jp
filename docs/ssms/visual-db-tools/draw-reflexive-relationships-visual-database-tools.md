---
description: 再帰リレーションシップの作成 (Visual Database Tools)
title: 再帰リレーションシップの作成
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- drawing reflexive relationships
- reflexive relationships
- database diagrams [SQL Server], relationships
ms.assetid: e218363f-faec-46d5-9904-a537fbcc994d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 2472266ae29470b19f93518676e75f8ff17d86ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480052"
---
# <a name="draw-reflexive-relationships-visual-database-tools"></a>再帰リレーションシップの作成 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
テーブルの 1 つ以上の列を同じテーブルの他の 1 つ以上の列にリンクするには、再帰リレーションシップを作成します。 たとえば、 `employee` テーブルに `emp_id` 列と `mgr_id` 列があるとします。 各管理者は従業員でもあるため、テーブル内のこれらの 2 つの列をリレーションシップの線で関連付けます。 このリレーションシップによって、テーブルに追加された各管理者 ID は、既存の従業員 ID と確実に一致します。  
  
リレーションシップを作成する前に、まずテーブルに主キー制約または UNIQUE 制約を定義する必要があります。 次に、主キー列を目的の列に関連付けます。 リレーションシップを作成すると、対応する列がテーブルの外部キーになります。  
  
### <a name="to-draw-a-reflexive-relationship"></a>再帰リレーションシップを作成するには  
  
1.  データベース ダイアグラムで、他の列と関連付けるデータベース列の行セレクターをクリックし、ポインターをテーブル外部にドラッグして線を表示させます。  
  
2.  選択したテーブルに線をドラッグします。  
  
3.  マウスのボタンを離します。 **[テーブルと列]** ダイアログ ボックスが表示されます。  
  
4.  リレーションシップを形成する外部キー列、および主キーのテーブルと列を選択します。  
  
5.  **[OK]** を 2 回クリックしてリレーションシップを作成します。  
  
テーブルに対してクエリを実行するとき、再帰リレーションシップを使用して自己結合を作成できます。 結合を含むテーブル クエリの実行の詳細については、「 [結合を使用したクエリ (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
[結合を使用したクエリ (Visual Database Tools)](../../ssms/visual-db-tools/query-with-joins-visual-database-tools.md)  
  
