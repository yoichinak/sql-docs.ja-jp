---
description: サブスクリプションの再初期化
title: サブスクリプションの再初期化 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- initializing subscriptions [SQL Server replication], reinitializing
- subscriptions [SQL Server replication], reinitializing
- reinitializing subscriptions
ms.assetid: fb13712b-e7ad-4f1f-b605-4554bad0cb60
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 7f1992be76777862078f029df44a73f7b3579dc2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88405418"
---
# <a name="reinitialize-subscriptions"></a>サブスクリプションの再初期化
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  サブスクリプションの再初期化では、1 つ以上のサブスクライバーに 1 つ以上のアーティクルの新しいスナップショットが適用されます。トランザクション レプリケーションとスナップショット レプリケーションでは個々のアーティクルを再初期化できますが、マージ レプリケーションではすべてのアーティクルを再初期化する必要があります。 ピア ツー ピア トランザクション レプリケーション トポロジのノードは再初期化できません。 ノードが新しいデータのコピーを確実に保持する必要がある場合は、そのノードでバックアップを復元してください。 再初期化は、以下の 2 つの場合に行われます。  
  
-   サブスクリプションを再初期化するように明示的にマークした場合。  
  
-   プロパティの変更など、再初期化を必要とする操作を実行した場合。 再初期化が必要な操作の詳細については、「[Change Publication and Article Properties](../../relational-databases/replication/publish/change-publication-and-article-properties.md)」 (パブリケーションおよびアーティクルのプロパティの変更) を参照してください。  
  
 いずれの場合も、ディストリビューション エージェントまたはマージ エージェントが次に実行されたときに、最新のスナップショットがサブスクライバーに適用されます。 スナップショット レプリケーションとトランザクション レプリケーションの場合は、再初期化が行われると、サブスクライバーで行われた変更 (まだパブリッシャーと同期されていない変更) は新しいスナップショットの適用によって上書きされます。  
  
 マージ レプリケーションの場合は、スナップショットを適用する前にすべてのデータ変更をサブスクライバーからアップロードするように選択することができます。 スナップショットが再適用される前に、パブリッシャーの保留中のスキーマ変更がサブスクライバーに適用され、前回の同期以降にサブスクライバーで行われた更新がパブリッシャーに反映されます。 この動作は、 **upload_first** プロパティと **automatic_reinitialization_policy** プロパティによって制御されます。詳細については、「 [Reinitialize a Subscription](../../relational-databases/replication/reinitialize-a-subscription.md)」を参照してください。 SQL Server Management Studio またはレプリケーション モニターを使用してサブスクリプションを再初期化するようにマークする場合は、 **[サブスクリプションの再初期化]** ダイアログ ボックスのオプションで、先に変更をアップロードするかどうかを指定できます。  
  
> [!IMPORTANT]  
>  マージ パブリケーションのパラメーター化されたフィルターを追加、削除、変更する場合は、再初期化の際にサブスクライバーで保留中の変更をパブリッシャーにアップロードできません。 保留中の変更をアップロードしたい場合は、フィルターを変更する前にすべてのサブスクリプションを同期してください。  
  
 サブスクリプションを作成するとき、初期スナップショットをサブスクライバーに適用しないように指定した場合、作成されたサブスクリプションを再初期化するようにマークしても、スナップショットは適用されません。 詳細については、「 [スナップショットを使用しないトランザクション サブスクリプションの初期化](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)を使用して、サブスクリプションを手動で初期化する方法について説明します。  
  
 **サブスクリプションを再初期化するには**  
  
 サブスクリプションのすべてのアーティクルを再初期化するには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、ストアド プロシージャ、またはレプリケーション管理オブジェクト (RMO) を使用します。 スナップショット パブリケーションおよびトランザクション パブリケーションの個々のアーティクルを再初期化するには、ストアド プロシージャを使用する必要があります。 詳細については、「 [Reinitialize a Subscription](../../relational-databases/replication/reinitialize-a-subscription.md)」をご覧ください。  
  
## <a name="see-also"></a>関連項目  
 [サブスクリプションの初期化](../../relational-databases/replication/initialize-a-subscription.md)   
 [サブスクリプションの有効期限と非アクティブ化](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
