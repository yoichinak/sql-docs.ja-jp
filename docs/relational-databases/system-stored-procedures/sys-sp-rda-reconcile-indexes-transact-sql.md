---
title: sp_rda_reconcile_indexes (Transact-sql) |Microsoft Docs
description: 詳細については、「sp_rda_reconcile_indexes」を参照してください。 リモートテーブルのインデックスを調整するために、この Transact-sql ストアドプロシージャを使用してスキーマタスクをキューに格納する方法について説明します。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sp_rda_reconcile_indexes
- sp_rda_reconcile_indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_indexes stored procedure
ms.assetid: 96b31ab9-bf84-46d6-9990-81f5c51f885a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2d224f5ea2b20f684fdd9e484304639114fd2d2e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544675"
---
# <a name="syssp_rda_reconcile_indexes-transact-sql"></a>sp_rda_reconcile_indexes (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  リモートテーブルのインデックスを調整するために、スキーマタスクをキューに入れます。 このタスクが正常に完了した後、リモートテーブルには、Stretch が有効なローカルテーブルに存在するのと同じインデックスがあります。  
  
 **Sp_rda_reconcile_indexes**を呼び出すときに、インデックスを調整するためにキューに登録された別のタスクがある場合、このストアドプロシージャは重複するタスクをキューに入れません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_rda_reconcile_indexes [@objname = ] 'objname'  
  
```  
  
## <a name="arguments"></a>引数  
 [ @objname =] *' objname '*  
 インデックスを調整する Stretch が有効なテーブルの修飾名または修飾されていない名前を指定します。 引用符は、修飾されたオブジェクトを指定する場合にのみ必要です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または >0 (失敗)  
  
## <a name="see-also"></a>参照  
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
