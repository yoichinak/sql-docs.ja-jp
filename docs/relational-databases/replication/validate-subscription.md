---
description: '[サブスクリプションを検証する]'
title: サブスクリプションを検証する | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.validate.validateandresynch.f1
helpviewer_keywords:
- Validate Subscription dialog box
ms.assetid: 74bdf5e1-b886-4284-b5fb-332bf79ae083
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 2e80697f75a6234b913e0784b0110873b3c848ac
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "88470145"
---
# <a name="validate-subscription"></a>[サブスクリプションを検証する]
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  **[サブスクリプションを検証する]** ダイアログ ボックスを使用すると、サブスクリプションのマージ エージェントを次に実行するときに、マージ パブリケーションへのサブスクリプションを検証するように指定できます。 検証の結果はレプリケーション モニターに表示されます。 詳しくは、「 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)」をご覧ください。  
  
 また、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] でパブリケーションを右クリックし、**[すべてのサブスクリプションの検証]** をクリックすると、マージ パブリケーションへのすべてのサブスクリプションを検証できます。  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>オプション  
 **[最後に検証を行った日付]**  
 検証が成功したかどうかに関係なく、サブスクリプションの検証を含むマージ エージェント セッションを最後に実行した日付です。  
  
 **[最後に検証が正常終了した日付]**  
 検証が正常終了したマージ エージェント セッションを最後に実行した日付です。  
  
 **[このサブスクリプションを検証する]**  
 選択すると、サブスクリプションを検証できます。  
  
 **Options**  
 クリックすると、 **[サブスクリプションの検証オプション]** ダイアログ ボックスが開き、行数の検証とバイナリ チェックサムの検証のどちらを使用するかを指定できます。  
  
## <a name="see-also"></a>参照  
 [レプリケートされたデータの検証](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
