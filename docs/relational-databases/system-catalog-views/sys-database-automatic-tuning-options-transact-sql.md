---
title: sys.database_automatic_tuning_options (Transact-sql) |Microsoft Docs
description: SQL Database で自動チューニングオプションを表示する方法について説明します。 必要なアクセス許可を確認し、使用可能なその他のリソースを表示します。
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- database_automatic_tuning_options_tsql
- database_automatic_tuning_options
- sys.database_automatic_tuning_options_tsql
- sys.database_automatic_tuning_options
dev_langs:
- TSQL
helpviewer_keywords:
- database_automatic_tuning_options catalog view
- sys.database_automatic_tuning_options catalog view
ms.assetid: 16b47d55-8019-41ff-ad34-1e0112178067
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0dbedd65c5f98016e4e001fd863845079da68578
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99210378"
---
# <a name="sysdatabase_automatic_tuning_options-transact-sql"></a>データベースの \_ 自動 \_ Tuning_options (transact-sql)
[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

  このデータベースの自動チューニングオプションを返します。  

|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|自動チューニングオプションの名前。 使用可能なオプションについては、 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) を参照してください。|  
|**desired_state**|**smallint**|自動チューニングオプションの目的の操作モードを示します。ユーザーによって明示的に設定されます。<br />0 = OFF<br />1 = ON|  
|**desired_state_desc**|**nvarchar(60)**|自動チューニングオプションの目的の操作モードの説明テキスト。<br />OFF<br />ON|  
|**actual_state**|**smallint**|自動チューニングオプションの操作モードを示します。<br />0 = OFF<br />1 = ON|  
|**actual_state_desc**|**nvarchar(60)**|自動チューニングオプションの実際の操作モードの説明テキストです。<br />OFF<br />ON|  
|**reason**|**smallint**|実際の状態と目的の状態が異なる理由を示します。<br />2 = 無効<br />11 = QUERY_STORE_OFF<br />12 = QUERY_STORE_READ_ONLY<br />13 = NOT_SUPPORTED|   
|**reason_desc**|**nvarchar(60)**|実際の状態と目的の状態が異なる理由の説明テキスト。<br />DISABLED = オプションはシステムによって無効にされています<br />QUERY_STORE_OFF = クエリストアがオフになっています<br />QUERY_STORE_READ_ONLY = クエリストアが読み取り専用モードです。<br />NOT_SUPPORTED = Enterprise edition でのみ使用可能 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]| 
  
## <a name="permissions"></a>アクセス許可  
 `VIEW DATABASE STATE` アクセス許可が必要です。  
  
## <a name="see-also"></a>参照  
 [自動チューニング](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [sys.dm_db_tuning_recommendations &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 
