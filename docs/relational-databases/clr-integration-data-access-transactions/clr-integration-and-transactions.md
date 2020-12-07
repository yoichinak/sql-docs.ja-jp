---
title: CLR 統合とトランザクション |Microsoft Docs
description: CLR 統合とトランザクションでは、ADO.NET とが連携して、マネージアプリケーションでのローカルトランザクションと分散トランザクションの使用を拡張および簡素化します。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- managed code [SQL Server], transactions
- common language runtime [SQL Server], transactions
- System.Transactions namespace
- transactions [CLR integration]
ms.assetid: 381d206e-06e2-48d0-8206-295fcf06ac98
author: rothja
ms.author: jroth
ms.openlocfilehash: bd65fce2f2a2bdf2ce25f4811063f7f9d56d2e15
ms.sourcegitcommit: 36fe62a3ccf34979bfde3e192cfa778505add465
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/11/2020
ms.locfileid: "94521137"
---
# <a name="clr-integration-and-transactions"></a>CLR 統合とトランザクション
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  System.string **名前空間は、** ADO.NET および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共通言語ランタイム (CLR) 統合と完全に統合されたトランザクションフレームワークを提供します。 ADO.NET とは連携して、マネージアプリケーションでのローカル **トランザクションと分散** トランザクションの使用を拡張し、簡素化します。  
  
> [!NOTE]  
>  CLR ユーザー定義プロシージャ (UDP) は、このプロシージャが実行されているサーバーへの接続 (ループバック接続) を確立して、同じトランザクションに参加することができません。 この操作を試みると、接続試行がブロックされ、制御は UDP に返されません。 これにより、UDP でタイムアウト エラー (メッセージ 1206) が発生します。  
  
 トランザクションと .NET Framework の詳細については、.NET Framework SDK の「トランザクションの実行」と「トランザクションの利用」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [トランザクションの昇格](../../relational-databases/clr-integration-data-access-transactions/transaction-promotion.md)  
 トランザクションを昇格する機能とこの機能の使用方法について説明します。  
  
 [現在のトランザクションへのアクセス](../../relational-databases/clr-integration-data-access-transactions/accessing-the-current-transaction.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインプロセスで現在実行中のトランザクションにアクセスする方法について説明します。  
  
 [System.Transactions の使用](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)  
 マネージアプリケーションでの system.string **アプリケーションプログラミング** インターフェイス (API) の使用方法について説明します。  
  
 [トランザクションの有効期間](../../relational-databases/clr-integration-data-access-transactions/transaction-lifetimes.md)  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャで開始されたトランザクションと、CLR アプリケーションで開始されたトランザクションの有効期間の違いについて説明します。  
  
## <a name="see-also"></a>参照  
 [CLR データベース オブジェクトからのデータ アクセス](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
