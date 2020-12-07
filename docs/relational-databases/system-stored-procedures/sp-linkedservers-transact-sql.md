---
description: sp_linkedservers (Transact-sql)
title: sp_linkedservers (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_linkedservers
- sp_linkedservers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_linkedservers
ms.assetid: d8f82f78-8a1f-4831-bcee-7c36c6e7dfbb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a998aa0bb5deab2b29b2133de95e0b3169602bb7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546035"
---
# <a name="sp_linkedservers-transact-sql"></a>sp_linkedservers (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ローカル サーバーに定義されているリンク サーバーの一覧を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_linkedservers  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または0以外の数値 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**SRV_NAME**|**sysname**|リンク サーバーの名前|  
|**SRV_PROVIDERNAME**|**nvarchar (** 128 **)**|指定されたリンクサーバーへのアクセスを管理している OLE DB プロバイダーのフレンドリ名。|  
|**SRV_PRODUCT**|**nvarchar (** 128 **)**|リンクサーバーの製品名。|  
|**SRV_DATASOURCE**|**nvarchar (** 4000 **)**|指定されたリンクサーバーに対応するデータソースプロパティを OLE DB します。|  
|**SRV_PROVIDERSTRING**|**nvarchar (** 4000 **)**|リンクサーバーに対応する OLE DB プロバイダー文字列プロパティです。|  
|**SRV_LOCATION**|**nvarchar (** 4000 **)**|指定されたリンクサーバーに対応する OLE DB location プロパティ。|  
|**SRV_CAT**|**sysname**|指定されたリンクサーバーに対応するカタログプロパティを OLE DB します。|  
  
## <a name="permissions"></a>アクセス許可  
 スキーマに対する SELECT 権限が必要です。  
  
## <a name="see-also"></a>参照  
 [sp_catalogs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_columns_ex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-columns-ex-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_primarykeys &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-primarykeys-transact-sql.md)   
 [sp_table_privileges &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [sp_tables_ex &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [分散クエリストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)  
  
  
