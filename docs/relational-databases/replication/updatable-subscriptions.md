---
description: '[更新可能なサブスクリプション]'
title: '[更新可能なサブスクリプション] | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.updatablesubscriptions.f1
ms.assetid: 8e9a13a0-6b24-47c6-9d83-3cbaf08f673d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 016414e9f6565c8c2593b478b295a3565f21266c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482257"
---
# <a name="updatable-subscriptions"></a>[更新可能なサブスクリプション]
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  トランザクション レプリケーションの場合、レプリケートされたデータは読み取り専用として扱う必要がありますが、更新可能なサブスクリプションを使用することにより、レプリケートされたデータを [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サブスクライバーで変更できます。 サブスクライバーでデータを変更する必要がある場合は、要件に応じて次のいずれかのオプションを選択してください。  
  
|更新可能なサブスクリプション タイプ|必要条件|  
|---------------------------------|------------------|  
|即時更新|サブスクライバーのデータを更新するために、パブリッシャーとサブスクライバーを接続します。|  
|キュー更新|サブスクライバーのデータを更新するために、パブリッシャーとサブスクライバーを接続する必要はありません。 更新をオフラインで実行し、後からパブリッシャーとサブスクライバーの間で同期させることができます。|  
  
## <a name="options"></a>オプション  
 **[以下のサブスクライバーの変更内容をレプリケートします]**  
 更新可能にする必要のある各サブスクライバーの **[レプリケート]** 列のチェック ボックスをオンにします。 これらの更新可能なサブスクライバーに対して、 **[パブリッシャーでのコミット]** 列のドロップダウン リスト ボックスから適切なオプションを選択します。  
  
-   即時更新サブスクリプションに対して **[変更を同時にコミットする]** を選択します。  
  
-   キュー更新サブスクリプションに対して **[変更をキューに登録し、可能な場合はコミット]** を選択します。  
  
## <a name="see-also"></a>参照  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [Subscribe to Publications](../../relational-databases/replication/subscribe-to-publications.md)   
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
