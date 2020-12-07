---
description: トランザクション分離レベル
title: トランザクション分離レベル | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], hints
- isolation levels [SQL Server], metadata access
- hints [SQL Server], locking
ms.assetid: 02bb71fa-1e92-4782-a9cf-6e256cc1f3ea
author: rothja
ms.author: jroth
ms.openlocfilehash: f9c3d400f67f42f206c9b6924f3d2ea90445d023
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88467561"
---
# <a name="transaction-isolation-levels"></a>トランザクション分離レベル
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、カタログ ビュー、互換性ビュー、情報スキーマ ビュー、またはメタデータ生成組み込み関数を使用してメタデータにアクセスするようなクエリでのロック ヒントの使用は保証されていません。  
  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]内部では、READ COMMITTED 分離レベルのみがメタデータ アクセスに使用されます。 たとえば、分離レベルが SERIALIZABLE のトランザクションで、カタログ ビューまたはメタデータ生成組み込み関数を使用したメタデータへのアクセスが試行されたとします。この場合、これらのクエリは、READ COMMITTED として完了するまで実行されます。 ただし、スナップショット分離では、同時実行の DDL 操作により、メタデータへのアクセスが失敗する場合があります。 これは、メタデータのバージョンが管理されないためです。 したがって、スナップショット分離で次のものにアクセスすると、失敗することがあります。  
  
-   カタログ ビュー  
  
-   互換性ビュー  
  
-   情報スキーマ ビュー  
  
-   メタデータ生成組み込み関数  
  
-   **sp_help** グループのストアド プロシージャ  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client カタログ プロシージャ  
  
-   動的管理ビューと動的管理関数  
  
 分離レベルについての詳細については、「[SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)」を参照してください。  
  
 次の表は、各種の分離レベルでのメタデータ アクセスをまとめたものです。  
  
|分離レベル|サポートされています|使用|  
|---------------------|---------------|-------------|  
|READ UNCOMMITTED|いいえ|保証なし|  
|READ COMMITTED|はい|はい|  
|REPEATABLE READ|いいえ|いいえ|  
|SNAPSHOT ISOLATION|いいえ|いいえ|  
|SERIALIZABLE|いいえ|いいえ|  
  
  
