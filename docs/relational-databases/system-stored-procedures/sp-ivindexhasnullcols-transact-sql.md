---
description: sp_ivindexhasnullcols (Transact-sql)
title: sp_ivindexhasnullcols (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_ivindexhasnullcols
- sp_ivindexhasnullcols_TSQL
helpviewer_keywords:
- sp_ivindexhasnullcols
ms.assetid: ed2cde63-37e1-43cf-b6ba-3b6114a0f797
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fe91514a87999bb053f6011e74b3b96ec075fbf4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549620"
---
# <a name="sp_ivindexhasnullcols-transact-sql"></a>sp_ivindexhasnullcols (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  インデックス付きビューを使ってトランザクション パブリケーションを作成する場合に、インデックス付きビューのクラスター化インデックスが一意であることと、NULL 値が許容される列を含まないことを検証します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_ivindexhasnullcols [ @viewname = ] 'view_name'  
        , [ @fhasnullcols= ] field_has_null_columns OUTPUT  
```  
  
## <a name="arguments"></a>引数  
`[ @viewname = ] 'view_name'` 検証するビューの名前を指定します。 *view_name* は **sysname**であり、既定値はありません。  
  
`[ @fhasnullcols = ] field_has_null_columns OUTPUT` NULL を許容する列がビューインデックスにあるかどうかを示すフラグです。 *view_name* は **sysname**であり、既定値はありません。 NULL を許容する列がビューインデックスに含まれる場合は、値 **1** を返します。 NULL を許容する列がビューに含まれていない場合は、値 **0** が返されます。  
  
> [!NOTE]  
>  ストアドプロシージャ自体がリターンコード **1**を返した場合、ストアドプロシージャの実行でエラーが発生したことを意味します。この値は **0** であり、無視する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_ivindexhasnullcols** は、トランザクションレプリケーションで使用されます。  
  
 既定では、サブスクライバー側でパブリケーション内のインデックス付きビュー アーティクルはテーブルとして作成されます。 ただし、インデックス付きの列で NULL 値が許容される場合、インデックス付きビューはテーブルではなく、サブスクライバー側のインデックス付きビューとして作成されます。 このストアドプロシージャを実行すると、現在のインデックス付きビューにこの問題が存在するかどうかをユーザーに警告できます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_ivindexhasnullcols**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
