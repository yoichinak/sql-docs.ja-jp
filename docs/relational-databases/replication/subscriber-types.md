---
description: サブスクライバーの種類
title: サブスクライバーの種類 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.subscribertypes.f1
ms.assetid: a70656cb-21c9-4489-be77-ccd396747e3b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016
ms.openlocfilehash: 26d32a2fcf2e516236cb0bfba91e240e956dab5f
ms.sourcegitcommit: 38e055eda82d293bf5fe9db14549666cf0d0f3c0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2021
ms.locfileid: "99250570"
---
# <a name="subscriber-types"></a>サブスクライバーの種類
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  マージ レプリケーションを使用すると、パブリケーションがサポートする必要があるサブスクライバーの種類を指定することができます。 サブスクライバーの種類を選択することで、パブリケーションが使用できる機能を決定する *パブリケーションの互換性レベル* が設定されます。  
  
 パブリケーション スナップショットが作成された後は、パブリケーションの互換性レベルは、 **[パブリケーションのプロパティ]** ダイアログ ボックスの **[全般]** ページ上で高く (より制限) することができますが、互換性レベルを低くすることはできません。  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>オプション  
 このパブリケーションでサポートする必要がある各サブスクライバーの種類を選択します。  
  
 [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]  
 パブリケーションはすべての機能を使用することができます。  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)]  
 パブリケーションは、スナップショット ファイルが文字形式 (これは、スナップショット エージェントによって自動的に処理されます) である必要があります。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] には、互換性レベルとは別の制限事項もあります。  
  
 このオプションが選択されている場合、Web 同期オプションはこのパブリケーションで有効です。 Web 同期の詳細については、「 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [データとデータベース オブジェクトのパブリッシュ](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [ディストリビューターとパブリッシャーのプロパティの表示および変更](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
  
  
