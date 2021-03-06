---
title: データベース復旧モデル
description: ユーザー データベースのバックアップ復旧モデルを確認し、データ損失を減らすためのポリシーを有効にする方法について説明します。
ms.custom: seo-lt-2019
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 8c68b60243ec033fff3735901cc4e35134222704
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100345504"
---
# <a name="database-recovery-model"></a>データベース復旧モデル
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  SQL Server の Enterprise Edition および Standard Edition では、このルールは、単純復旧モデルに設定されている読み取り専用以外のユーザー データベースについて確認します。 実稼働データベースの場合は、単純復旧モデルではなく完全復旧モデルを使用することをお勧めします。 完全復旧モードを使用すると、特定の時点への復旧が可能になります。 これにより、ディザスター リカバリー時のデータ損失を軽減できます。
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスの推奨事項  
 実稼働データベースを完全復旧モードにし、トランザクション ログを頻繁にバックアップしてください。これにより、復旧時のデータ損失を最小限に抑えることができます。
  
## <a name="see-also"></a>関連項目 
  
 [復元と復旧の概要](../backup-restore/restore-and-recovery-overview-sql-server.md)   
  
 [データベースの全体復元 (完全復旧モデル)](../backup-restore/complete-database-restores-full-recovery-model.md)  

 [ トランザクション ログのバックアップ](../backup-restore/transaction-log-backups-sql-server.md)   
  
