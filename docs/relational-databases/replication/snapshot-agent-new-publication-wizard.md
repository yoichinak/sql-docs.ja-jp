---
description: '[スナップショット エージェント] (パブリケーションの新規作成ウィザード)'
title: '[スナップショット エージェント](パブリケーションの新規作成ウィザード) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.configuresnapshotagent.f1
ms.assetid: 0257d4ee-1f7b-49fd-b4ef-65bfc1ef6951
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 09ba1d7b01a7b162d68dfb55c03fe1fead25f941
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420396"
---
# <a name="snapshot-agent-new-publication-wizard"></a>[スナップショット エージェント] (パブリケーションの新規作成ウィザード)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  [スナップショット エージェント] では、新しいサブスクリプションの初期化に使用されるパブリケーション スキーマおよびデータを含んでいるファイルを作成します。 既定では、スナップショット エージェントは、パブリケーションの新規作成ウィザードでパブリケーションが作成されるとすぐに実行されます。 続いて、エージェントが指定したスケジュールに従って実行されます。 エージェントが実行されるたびに新しいスナップショット ファイルが作成されるかどうかは、選択したレプリケーションおよびオプションの種類によって異なります。 詳細については、「[スナップショットの作成および適用](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)」を参照してください。  
  
 パラメーター化されたフィルターを使用するマージ パブリケーションでは、パブリケーション スナップショットの完了後、データの各パーティションのスナップショットを作成する必要があります。 詳しくは、「 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」をご覧ください。  
  
## <a name="options"></a>Options  
 **[スナップショットをすぐに作成する]** (マージ レプリケーション) または **[スナップショットをすぐに作成し、サブスクリプションを初期化できるようにそのスナップショットを保持する]** (トランザクション レプリケーション)  
 パブリケーションの新規作成ウィザードが完了した後、すぐにスナップショットを作成する場合は、このチェック ボックスを選択します。 スナップショットが生成される前に **[パブリケーションのプロパティ]** ダイアログ ボックスでスナップショットのプロパティを変更する場合、またはスナップショットを使用せずにサブスクライバーを初期化する場合は、このチェック ボックスをオフにします。 詳細については、「 [スナップショットを使用しないトランザクション サブスクリプションの初期化](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)を使用して、サブスクリプションを手動で初期化する方法について説明します。  
  
> [!NOTE]  
>  ディストリビューション エージェントまたはマージ エージェントの適切なジョブを開始するために、ウィザードによりディストリビューターへの接続が要求される場合があります。  
  
 **[以下のスケジュールでスナップショット エージェントを実行する]**  
 スナップショット エージェントを実行する既定のスケジュールを受け入れるか、 **[変更]** をクリックしてスケジュールを指定します。  
  
## <a name="see-also"></a>参照  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [初期スナップショットの作成および適用](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [パブリケーション プロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Initialize a Subscription with a Snapshot (スナップショットを使用したサブスクリプションの初期化)](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)   
 [データとデータベース オブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [レプリケーション エージェントの概要](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
