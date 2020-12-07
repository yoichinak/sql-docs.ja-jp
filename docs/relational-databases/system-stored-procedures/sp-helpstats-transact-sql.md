---
description: sp_helpstats (Transact-sql)
title: sp_helpstats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpstats
- sp_helpstats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpstats
ms.assetid: 00ab3cfd-2736-4fc0-b1b2-16dd49fb2fe5
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8c7779e96727eed170d8869af8c21fe68c9d1455
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535110"
---
# <a name="sp_helpstats-transact-sql"></a>sp_helpstats (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  指定したテーブルの列およびインデックスに関する統計を返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)] 統計に関する情報を取得するに [は、](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md) [stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md) カタログビューに対してクエリを実行します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpstats[ @objname = ] 'object_name'   
     [ , [ @results = ] 'value' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @objname = ] 'object_name'` 統計情報を提供するテーブルを指定します。 *object_name* は **nvarchar (520)** であり、null にすることはできません。 1 つまたは 2 つの部分で構成される名前を指定できます。  
  
`[ @results = ] 'value'` 提供する情報の範囲を指定します。 有効なエントリは **ALL** と **STATS**です。 **すべて** のインデックスの統計を一覧表示し、統計が作成された列も表示します。統計には、インデックスに関連付けられていない **統計のみが** 表示されます。 *値* は **nvarchar (5)** で、既定値は STATS です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次の表では、結果セットの列について説明します。  
  
|列名|説明|  
|-----------------|-----------------|  
|**statistics_name**|統計の名前。 **Sysname**を返します。 null にすることはできません。|  
|**statistics_keys**|統計の基になるキー。 **Nvarchar (2078)** を返します。 null にすることはできません。|  
  
## <a name="remarks"></a>解説  
 DBCC SHOW_STATISTICS を使用すると、特定のインデックスまたは統計に関する詳細な統計情報を表示できます。 詳細については、「 [DBCC SHOW_STATISTICS &#40;transact-sql&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md) 」と「 [transact-sql &#40;の sp_helpindex ](../../relational-databases/system-stored-procedures/sp-helpindex-transact-sql.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、`sp_createstats` を実行し、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内のすべてのユーザー テーブルを対象にして、条件を満たすすべての列に関する統計を 1 列ずつ作成します。 次に、を実行して、 `sp_helpstats` テーブルに作成された結果の統計情報を検索し `Customer` ます。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_createstats;  
GO  
EXEC sp_helpstats   
@objname = 'Sales.Customer',  
@results = 'ALL';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `statistics_name               statistics_keys`  
  
 `----------------------------  ----------------`  
  
 `_WA_Sys_00000003_22AA2996     AccountNumber`  
  
 `AK_Customer_AccountNumber     AccountNumber`  
  
 `AK_Customer_rowguid           rowguid`  
  
 `CustomerType                  CustomerType`  
  
 `IX_Customer_TerritoryID       TerritoryID`  
  
 `ModifiedDate                  ModifiedDate`  
  
 `PK_Customer_CustomerID        CustomerID`  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
