---
title: レプリケーションのチュートリアル | Microsoft Docs
description: これらのチュートリアルを使用して、SQL Server でのレプリケーション用にサーバーを準備し、トランザクションとマージの両方のレプリケーションを構成する方法について説明します。
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- tutorials [SQL Server replication]
- walkthroughs [SQL Server replication]
- replication [SQL Server], tutorials
ms.assetid: 19fbd10e-5b59-4cd0-a988-52d5d9206242
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: ab482e4818d7d60b9876fbf300a39de0b2f9ee40
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868384"
---
# <a name="replication-tutorials"></a>レプリケーションのチュートリアル
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
レプリケーションは、サーバー間でデータまたはデータのサブセットを移動するための強力なソリューションです。 トランザクション レプリケーションを使用して完全に接続されたサーバー間でデータをレプリケートすることができます。 マージ レプリケーションを使用して断続的に接続されたサーバーとクライアントの間でデータをレプリケートすることもできます。 この記事では、レプリケーション用にサーバーを準備するために役立つチュートリアルを示し、トランザクション レプリケーションとマージ レプリケーションの両方を構成する方法を説明します。 
  
レプリケーションのチュートリアルでは、"パブリッシャー" はレプリケート元のデータが配置されているサーバーを指します。 "サブスクライバー" は、レプリケート先のサーバーを指します。 パブリッシャーとサブスクライバーが同じ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを共有することもできますが、これは必須条件ではありません。 詳細については、「[レプリケーションのパブリッシング モデルの概要](../../relational-databases/replication/publish/replication-publishing-model-overview.md)」をご覧ください。  

これらのチュートリアルでは、パブリッシャーとディストリビューターとして NODE1\SQL2016 を使います。 サブスクライバーとしては、NODE2\SQL2016 を使います。 
  
> [!NOTE]  
> このチュートリアルで示すタスクのほとんどは、プログラムによって実行できます。 詳細については、「[レプリケーション開発者のドキュメント](../../relational-databases/replication/concepts/replication-developer-documentation.md)」をご覧ください。  
  
## <a name="replication-tutorials"></a>レプリケーションのチュートリアル  
[チュートリアル:レプリケーション用の SQL Server の準備 (パブリッシャー、ディストリビューター、サブスクライバー)](../../relational-databases/replication/tutorial-preparing-the-server-for-replication.md) 
 
最小の権限でレプリケーションを実行できるようサーバーを準備する方法を学習します。 このチュートリアルは、レプリケーション関連のチュートリアルの中で最初に実行する必要があります。  
  
[チュートリアル:2 つの常時接続サーバー間のレプリケーション (トランザクション) を構成する](../../relational-databases/replication/tutorial-replicating-data-between-continuously-connected-servers.md)

常時接続のサーバー間でデータをレプリケートするようにトランザクション レプリケーションを構成する方法を学習します。 このチュートリアルには、いくつか基本的なエラーのトラブルシューティングの手法も含まれます。 

  
[チュートリアル:サーバーとモバイル クライアントの間のレプリケーション (マージ) を構成する](../../relational-databases/replication/tutorial-replicating-data-with-mobile-clients.md)

サーバーと、常時接続でない 1 つ以上のクライアントの間でデータを交換するようにマージ レプリケーションを構成する方法を学習します。  
  
## <a name="see-also"></a>関連項目  
[レプリケーションのセキュリティ設定の表示および変更](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md) 

[トランザクション レプリケーションの概要](./transactional/transactional-replication.md) 

[マージ レプリケーションの概要](./merge/merge-replication.md)

