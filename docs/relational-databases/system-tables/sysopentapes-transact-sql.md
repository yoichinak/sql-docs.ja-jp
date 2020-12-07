---
description: sysopentapes (Transact-sql)
title: sysopentapes (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysopentapes
- sysopentapes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- backup media [SQL Server], sysopentapes system table
- sysopentapes system table
ms.assetid: c066ca9b-9cfd-46b1-90a3-5c8dc9e7b6ae
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5a64ea925775daacdbd44a71a945e86fe0f2c9aa
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89537907"
---
# <a name="sysopentapes-transact-sql"></a>sysopentapes (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在開いているテープ デバイスごとに 1 行のデータを格納します。 このビューは、 **master** データベースに格納されます。  
  
> [!IMPORTANT]  
>  このシステムテーブルは、下位互換性のためのビューとして含まれています。 代わりに、 [dm_io_backup_tapes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-io-backup-tapes-transact-sql.md) 動的管理ビューを使用します。  
  
> [!NOTE]  
>  **Sysopentapes**ビューを削除することはできません。  

  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**openTape**|**nvarchar (64)**|開いているテープ デバイスの物理ファイル名。 テープデバイスを開いて解放する方法の詳細については、「 [transact-sql&#41;のバックアップ &#40;](../../t-sql/statements/backup-transact-sql.md) 」および「 [&#40;Transact-sql&#41;の復元 ](../../t-sql/statements/restore-statements-transact-sql.md)」を参照してください。|  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは、サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
  
