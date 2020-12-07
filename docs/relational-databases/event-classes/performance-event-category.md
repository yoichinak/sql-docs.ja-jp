---
description: Performance イベント カテゴリ
title: Performance イベント カテゴリ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SQL Server event classes, Performance event category
- Performance event category [SQL Server]
- event classes [SQL Server], Performance event category
ms.assetid: 708f3585-d8be-4980-bbff-672d7c59397e
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b652324f42375bd1de7161ac596f13be13891475
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88499430"
---
# <a name="performance-event-category"></a>Performance イベント カテゴリ
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  **Performance** イベント カテゴリを使用すると、 **Showplan** イベント クラス、および SQL DML (データ操作言語) の操作を実行したときに作成されるイベント クラスを監視できます。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[Auto Stats イベント クラス](../../relational-databases/event-classes/auto-stats-event-class.md)|インデックス統計および列統計の自動更新が実行されたことを示します。|  
|[Degree of Parallelism &#40;7.0 Insert&#41; イベント クラス](../../relational-databases/event-classes/degree-of-parallelism-7-0-insert-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で、直列プランまたは並列プランのいずれかを使用して SELECT、INSERT、UPDATE、または DELETE ステートメントが実行されたことを示します。 操作の実行に使用された CPU の数もレポートされます。|  
|[Performance Statistics イベント クラス](../../relational-databases/event-classes/performance-statistics-event-class.md)|実行中のクエリのパフォーマンスを監視します。|  
|[Showplan All イベント クラス](../../relational-databases/event-classes/showplan-all-event-class.md)|SQL ステートメント内の **Showplan** 操作を識別します。|  
|[Showplan All for Query Compile イベント クラス](../../relational-databases/event-classes/showplan-all-for-query-compile-event-class.md)|**Showplan** 操作のコンパイル時間データを表示します。|  
|[Showplan Statistics Profile イベント クラス](../../relational-databases/event-classes/showplan-statistics-profile-event-class.md)|クエリの推定コストを表示します。|  
|[Showplan XML イベント クラス](../../relational-databases/event-classes/showplan-xml-event-class.md)|SQL ステートメント内の **Showplan** 操作を識別します。 このイベント クラスには、各イベントが整形式の XML ドキュメントとして格納されます。|  
|[Showplan XML for Query Compile イベント クラス](../../relational-databases/event-classes/showplan-xml-for-query-compile-event-class.md)|**Showplan** 操作のコンパイル時間データを XML 形式で表示します。|  
|[Showplan XML Statistics Profile イベント クラス](../../relational-databases/event-classes/showplan-xml-statistics-profile-event-class.md)|SQL ステートメントに関連付けられた **Showplan** 操作を識別します。 出力は XML ドキュメントです。|  
|[SQL:FullTextQuery イベント クラス](../../relational-databases/event-classes/sql-fulltextquery-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でフルテキスト クエリが実行されたことを示します。|  
|[Plan Guide Successful イベント クラス](../../relational-databases/event-classes/plan-guide-successful-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でプラン ガイドを含むクエリまたはバッチの実行プランが正常に生成されたことを示します。|  
|[Plan Guide Unsuccessful イベント クラス](../../relational-databases/event-classes/plan-guide-unsuccessful-event-class.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でプラン ガイドを含むクエリまたはバッチの実行プランを生成できなかったことを示します。|  
  
## <a name="see-also"></a>参照  
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)  
  
  
