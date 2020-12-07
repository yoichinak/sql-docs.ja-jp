---
description: マージ レプリケーションのアーティクルのオプション
title: マージ レプリケーションのアーティクルのオプション | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], article options
- articles [SQL Server replication], merge replication options
ms.assetid: 670abd41-d204-4cd7-a371-7664e603a0ce
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: eb832433ad5274bf63467327fc6ad8273ff4cc35
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465231"
---
# <a name="article-options-for-merge-replication"></a>マージ レプリケーションのアーティクルのオプション
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  アプリケーションのニーズに合わせてレプリケーション動作をカスタマイズするためのマージ テーブル アーティクルには多くのオプションがあります。 マージ レプリケーションを使用すると、以下のようなことが可能です。  
  
-   行フィルター、結合フィルター、および列フィルターを使用します。 テーブル アーティクルをフィルター選択すると、パブリッシュされるデータのパーティションを作成できます。 詳細については、「[パブリッシュされたデータのフィルター選択](../../../relational-databases/replication/publish/filter-published-data.md)」を参照してください。  
  
-   サブスクライバーでの変更をパブリッシャーにアップロードするかどうかを指定します。 サブスクライバーでデータの一部またはすべてが読み取り専用であるアプリケーションでは、アーティクルをダウンロード専用にすることにより、パフォーマンスが向上します。 詳細については、「[ダウンロード専用アーティクルを使用したマージ レプリケーションのパフォーマンス最適化](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)」を参照してください。  
  
-   1 つまたは複数のアーティクルに対する削除をレプリケーション トリガーおよびシステム テーブルによって追跡しないように指定します。 このオプションは多くのアプリケーション シナリオで役に立ちます。 レプリケートする必要のないバッチ削除を使用するシナリオなどがあります。 詳細については、「[Optimize Merge Replication Performance with Conditional Delete Tracking](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)」 (条件付き削除の追跡によるマージ レプリケーションのパフォーマンスの最適化) を参照してください。  
  
-   アーティクルの処理順序を指定し、アプリケーションが要求する順序でアーティクルが処理されるようにします。 詳細については、[マージ レプリケーションのオプションの指定](../../../relational-databases/replication/merge/specify-merge-replication-properties.md)に関するページを参照してください。  
  
-   関連するレコードのセットを 1 つの単位として処理するように指定します (既定では、マージ レプリケーションはテーブルへの変更を行単位で処理します)。 詳細については、「[Group Changes to Related Rows with Logical Records](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)」 (論理レコードによる関連行への変更のグループ化) を参照してください。  
  
-   トポロジの複数のノードで同じデータが変更される可能性がある場合に、競合の検出と解決を使用します。 詳細については、「 [マージ レプリケーションの競合の検出および解決](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)」を参照してください。  
  
-   制約やトリガーをサブスクライバーにコピーするかどうかなど、スキーマ オプションを指定します。 詳細については、「[スキーマ オプションの指定](../../../relational-databases/replication/publish/specify-schema-options.md)」を参照してください。  
  
-   ビジネス ロジック ハンドラーを使用して、同期中に発生するさまざまな状況に対処します。 たとえば、データの変更、競合、エラーに対処します。 詳細については、「[Execute Business Logic During Merge Synchronization](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)」(マージ同期中のビジネス ロジックの実行) をご覧ください。  
  
## <a name="see-also"></a>参照  
 [データとデータベース オブジェクトのパブリッシュ](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
