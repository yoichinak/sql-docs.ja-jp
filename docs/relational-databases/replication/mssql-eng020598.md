---
description: MSSQL_ENG020598
title: MSSQL_ENG020598 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020598 error
ms.assetid: 1c3032f2-23d1-4ead-94ee-16ac4d75cd0c
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 3f646b18a68d15d679031ffb8e3caf65b522c1df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465120"
---
# <a name="mssql_eng020598"></a>MSSQL_ENG020598
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>メッセージの詳細  
  
|属性|値|  
|-|-|  
|製品名|SQL Server|  
|イベント ID|20598|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|シンボル名||  
|メッセージ テキスト|レプリケートされたコマンドを適用しているときに、サブスクライバーで行が見つかりませんでした。|  
  
## <a name="explanation"></a>説明  
 このエラーは、トランザクション レプリケーションで、ディストリビューション エージェントがサブスクライバーの行を更新しようとしたときに、行が削除されていたり、行の主キーが変更されている場合に発生します。 既定では、変更はパブリッシャーには反映されないため、トランザクション パブリケーションに対するサブスクライバーは読み取り専用として処理されます。 トランザクション レプリケーションでは、更新可能なサブスクリプションまたはピア ツー ピア レプリケーションが使用されている場合にのみ、ユーザーの変更をサブスクライバーで行う必要があります。 これらのオプションの詳細については、「 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md) 」および「 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)」を参照してください。  
  
## <a name="user-action"></a>ユーザーの操作  
 **この問題を解決するには、次のようにします。**  
  
1.  エラーの原因を特定している間にレプリケーションを続行する必要がある場合は、ディストリビューション エージェントで **-SkipErrors 20598** パラメーターを指定します。 このパラメーターを指定すると、エージェントはエラー 20598 の原因となった変更をスキップし、他の変更をレプリケートできるようになります。  
  
2.  削除されている行、またはパブリッシャーの対応する行とは異なる主キーを持っているサブスクライバーの行を特定します。 パブリケーションとサブスクリプション データベースとの間で異なる行を確認するには、 [tablediff Utility](../../tools/tablediff-utility.md) を使用します。 レプリケートされたデータベースでのこのユーティリティの使用については、「[レプリケートされたテーブルを比較して相違があるかどうかを確認する &#40;レプリケーション プログラミング&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)」を参照してください。  
  
3.  **tablediff** ユーティリティまたは別の方法でサブスクライバーの行を修正します。  
  
4.  (省略可能) **-SkipErrors** パラメーターを削除します。  
  
## <a name="see-also"></a>参照  
 [エラーとイベントのリファレンス &#40;レプリケーション&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
