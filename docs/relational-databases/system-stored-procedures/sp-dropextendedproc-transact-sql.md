---
description: sp_dropextendedproc (Transact-SQL)
title: sp_dropextendedproc (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropextendedproc
- sp_dropextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropextendedproc
ms.assetid: dd93af2c-1b7d-4e39-af23-2d21d270a381
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 02d4287b2825401acd0eca532b3fad100fa32639
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538972"
---
# <a name="sp_dropextendedproc-transact-sql"></a>sp_dropextendedproc (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  拡張ストアドプロシージャを削除します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [CLR 統合](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) を使用してください。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
sp_dropextendedproc [ @functname = ] 'procedure'   
```  
  
## <a name="arguments"></a>引数  
`[ @functname = ] 'procedure'` 削除する拡張ストアドプロシージャの名前を指定します。 *プロシージャ* は **nvarchar (517)**,、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 **Sp_dropextendedproc**を実行すると、ユーザー定義の拡張ストアドプロシージャ名[が、](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) extended_procedures カタログビューから削除され、そのエントリが削除されます[。](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) このストアドプロシージャは、 **master** データベースでのみ実行できます。  
  
**sp_dropextendedproc** では、システム拡張ストアドプロシージャは削除されません。 代わりに、システム管理者は、拡張ストアドプロシージャに対する EXECUTE 権限を **public** ロールに対して拒否する必要があります。  
  
 **sp_dropextendedproc** をトランザクション内で実行することはできません。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_dropextendedproc**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 次の例では、 `xp_hello` 拡張ストアドプロシージャを削除します。  
  
> [!NOTE]  
>  この拡張ストアドプロシージャは既に存在している必要があります。このような場合、この例ではエラーメッセージが返されます。  
  
```  
USE master;  
GO  
EXEC sp_dropextendedproc 'xp_hello';  
```  
  
## <a name="see-also"></a>参照  
 [sp_addextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
