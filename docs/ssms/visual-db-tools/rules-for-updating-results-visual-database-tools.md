---
description: 結果更新の規則 (Visual Database Tools)
title: 結果更新のルール
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- updating query results
- Query Designer [SQL Server], Results pane
- Results pane
ms.assetid: de131ef0-ccbd-446f-9400-b93c7b8fa537
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: bbf2a7a3ca1d25a6556a6f31667d3f406cf055dc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88397348"
---
# <a name="rules-for-updating-results-visual-database-tools"></a>結果更新の規則 (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
多くの場合、 [結果ペイン](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)に表示されている結果セットは更新できます。 ただし、更新できない場合もあります。  
  
結果を更新するには、通常、 [クエリおよびビュー デザイナー](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) がテーブル内の行を一意に識別するのに十分な情報が必要です。 たとえば、クエリの出力リストに主キーが含まれている場合などが該当します。 さらに、データベースを更新するためのアクセス許可も必要です。  
  
クエリがビューに基づいている場合は、更新できる可能性があります。 この場合も同じガイドラインが適用されますが、ビュー自体に対してだけでなく、ビューの基になるテーブルにも適用される点が異なります。  
  
> [!NOTE]  
> クエリおよびビュー デザイナーは、ビューに基づく結果セットを更新できるかどうかを事前に判断できません。 このため、更新できない場合でも、すべてのビューが表示されます。  
  
次の表は、結果ペインに表示されたクエリの結果を更新できる場合とできない場合の例をまとめたものです。 多くの場合、クエリの結果を更新できるかどうかは、使用しているデータベースによって決まります。  
  
|クエリ|結果更新の可/不可|  
|---------|---------------------------|  
|出力リストに主キーを持つ、単一のテーブルに基づくクエリ|可 (下のリストを除く)。|  
|一意のインデックスおよび主キーを持たないテーブルに基づくクエリ|クエリとデータベースによって異なります。 データベースによっては、レコードを一意に識別するのに十分な情報があれば、クエリの結果を更新できます。|  
|結合されていない複数のテーブルに基づくクエリ|いいえ。|  
|データベース内で読み取り専用に設定されているデータに基づくクエリ|いいえ。|  
|制約のない単一のテーブルを含むビューに基づくクエリ|可 (下のリストを除く)。|  
|一対一リレーションシップで結合されているテーブルに基づくクエリ|可 (下のリストを除く)。|  
|一対多リレーションシップで結合されているテーブルに基づくクエリ|通常は可。|  
|多対多リレーションシップを持つ 3 つ以上のテーブルに基づくクエリ|いいえ。|  
|更新権限を与えられていないテーブルに基づくクエリ|削除は可。更新は不可。|  
|削除権限を与えられていないテーブルに基づくクエリ|更新は可。削除は不可。|  
|集計クエリ|いいえ。|  
|合計または集約関数を含むサブクエリに基づくクエリ|いいえ。|  
|重複する行を排除する DISTINCT キーワードを含むクエリ|いいえ。|  
|テーブルを返すユーザー定義関数が FROM 句に含まれるクエリ、および複数の SELECT ステートメントを含むユーザー定義関数を FROM 句に含むクエリ|いいえ。|  
|インライン ユーザー定義関数を FROM 句に含むクエリ|はい。|  
  
また、クエリ結果で特定の列を更新できない場合もあります。 結果ペインで更新できない列の種類を次に示します。  
  
-   式に基づく列  
  
-   スカラー ユーザー定義関数に基づく列  
  
-   他のユーザーにより削除された行または列  
  
-   他のユーザーによりロックされている行または列 (ただし、ロックされている行は、通常、ロックが解除されたと同時に更新できるようになります。)  
  
-   タイムスタンプまたは BLOB 列  
  
## <a name="see-also"></a>参照  
[クエリおよびビューのデザインの操作方法に関するトピック (Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
