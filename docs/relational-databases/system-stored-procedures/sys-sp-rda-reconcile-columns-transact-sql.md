---
title: sys.sp_rda_reconcile_columns (Transact-sql) |Microsoft Docs
description: Sys.sp_rda_reconcile_columns について説明します。 このストアドプロシージャを使用して、リモート Azure テーブルの列と Stretch が有効な SQL Server テーブルの列を調整します。
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
f1_keywords:
- sys.sp_rda_reconcile_columns
- sys.sp_rda_reconcile_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reconcile_columns stored procedure
ms.assetid: 60d9cc4e-1828-450b-9d88-5b8485800d73
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8eb33cbb1fd2975d96a727f6a7fde457c9827cc8
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99211777"
---
# <a name="syssp_rda_reconcile_columns-transact-sql"></a>sys.sp_rda_reconcile_columns (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  リモート Azure テーブルの列を、Stretch が有効な SQL Server テーブルの列に調整します。  
    
  **sp_rda_reconcile_columns** では、リモートテーブルではなく、Stretch が有効な SQL Server テーブルに存在するリモートテーブルに列が追加されます。 これらの列は、リモートテーブルから誤って削除した列である場合があります。 ただし、リモートテーブルには存在するが SQL Server テーブルには存在しない列は、リモートテーブルからは削除されません **sp_rda_reconcile_columns** 。
  
  > [!IMPORTANT]
  > **sp_rda_reconcile_columns** がリモート テーブルから誤って削除した列を再作成する場合、削除された列に属していたデータは復元されません。
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
   
## <a name="syntax"></a>構文  
  
```  
  
sp_rda_reconcile_columns @objname = '@objname'  
  
```  
  
## <a name="arguments"></a>引数  
 \@objname = '*\@ objname*'  
 Stretch が有効な SQL Server テーブルの名前。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または >0 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 db_owner のアクセス許可が必要です。  
   
## <a name="remarks"></a>コメント  
 Stretch 対応の SQL Server テーブルに存在しなくなったリモートの Azure テーブルに列が存在している場合、これらの余分な列が Stretch Database の正常な動作を妨げることはありません。 必要に応じて余分の列を手動で削除できます。  
  
## <a name="example"></a>例  
 リモート Azure テーブルの列を調整するには、次のステートメントを実行します。  
  
```sql  
EXEC sp_rda_reconcile_columns @objname = N'StretchEnabledTableName';  
```  
  
  
