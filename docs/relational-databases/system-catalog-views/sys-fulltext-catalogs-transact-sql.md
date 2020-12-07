---
description: sys.fulltext_catalogs (Transact-SQL)
title: fulltext_catalogs (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_catalogs_TSQL
- sys.fulltext_catalogs
- fulltext_catalogs
- fulltext_catalogs_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_catalogs catalog view
ms.assetid: cf1489ff-4819-41fa-a62a-4ed797a16207
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: 886f8d99e286fd026e5e4435c8daa9192d22ce99
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498393"
---
# <a name="sysfulltext_catalogs-transact-sql"></a>sys.fulltext_catalogs (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  フルテキストカタログごとに1行の値を格納します。  
  
> [!NOTE]  
>  次の列は、の将来のリリースで削除される予定です [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] : **data_space_id**、 **file_id**、および **パス**。 新しい開発作業ではこれらの列を使用しないようにし、現在これらの列を使用しているアプリケーションはできるだけ早く修正してください。  
 
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|fulltext_catalog_id|**int**|フルテキストカタログの ID。 データベース内のフルテキストカタログ全体で一意です。|  
|name|**sysname**|カタログの名前。 データベース内で一意です。|  
|path|**nvarchar(260)**|ファイルシステム内のカタログディレクトリの名前。|  
|is_default|**bit**|既定のフルテキストカタログ。<br /><br /> True = が既定値です。<br /><br /> False = 既定値ではない|  
|is_accent_sensitivity_on|**bit**|カタログのアクセントの区別に関する設定。<br /><br /> True = アクセントを区別する。<br /><br /> False = アクセントを区別しない|  
|data_space_id|**int**|このカタログが作成されたファイルグループ。|  
|file_id|**int**|カタログに関連付けられているフルテキストファイルのファイル ID。|  
|principal_id|**int**|フルテキストカタログを所有するデータベースプリンシパルの ID。|  
|is_importing|**bit**|フルテキストカタログがインポートされているかどうかを示します。<br /><br /> 1 = カタログがインポートされています。<br /><br /> 2 = カタログがインポートされていません。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>関連項目  
 [カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [CREATE FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [Transact-sql&#41;&#40;のフルテキストカタログの変更 ](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)   
 [DROP FULLTEXT CATALOG &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md)  
  
  
