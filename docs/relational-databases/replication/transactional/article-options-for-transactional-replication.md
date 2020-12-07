---
description: トランザクション レプリケーションのアーティクル オプション
title: トランザクション レプリケーションのアーティクル オプション | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], transactional replication options
- transactional replication, article options
ms.assetid: 3469b185-0ea5-4690-a71c-717230d886b6
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 085f991a1adc9a19c5d308ccf1e522ef1f73143e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482301"
---
# <a name="article-options-for-transactional-replication"></a>トランザクション レプリケーションのアーティクル オプション
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  トランザクション パブリケーションには、アーティクルのためのオプションがいくつかあります。 たとえば、トランザクション レプリケーションでは次のようなことが可能です。  
  
-   パブリッシャーからサブスクライバーに変更を反映する方法を指定できます。 詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
-   ストアド プロシージャの実行をレプリケートするように指定できます。 これは、大量のデータに影響を与えるメンテナンス用ストアド プロシージャの結果をレプリケートする場合に便利です。 詳細については、「[トランザクション レプリケーションにおけるパブリッシング ストアド プロシージャの実行](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)」をご覧ください。  
  
-   制約やトリガーをサブスクライバーにコピーするかどうかなど、スキーマ オプションを指定します。 詳細については、「[スキーマ オプションの指定](../../../relational-databases/replication/publish/specify-schema-options.md)」を参照してください。  
  
-   行フィルターや列フィルターを使用できます。 テーブル アーティクルをフィルター選択すると、パブリッシュされるデータのパーティションを作成できます。 詳細については、「[パブリッシュされたデータのフィルター選択](../../../relational-databases/replication/publish/filter-published-data.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データとデータベース オブジェクトのパブリッシュ](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
