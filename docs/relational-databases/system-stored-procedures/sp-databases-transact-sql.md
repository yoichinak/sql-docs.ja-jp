---
description: sp_databases (Transact-sql)
title: sp_databases (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_databases_TSQL
- sp_databases
dev_langs:
- TSQL
helpviewer_keywords:
- sp_databases
ms.assetid: 2a83b92a-9ecc-43c4-8ff4-e91e3a940b5a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 90fbcbf710f1779ad011163641aa61b14b33c65b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549900"
---
# <a name="sp_databases-transact-sql"></a>sp_databases (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  のインスタンスに存在するか、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースゲートウェイを介してアクセスできるデータベースの一覧を表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_databases  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 なし  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**DATABASE_NAME**|**sysname**|データベースの名前です。 では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] この列は、データベース名を表し **ます。** この名前は、データベースカタログビューに格納されています。|  
|**DATABASE_SIZE**|**int**|データベースのサイズ (kb 単位)。|  
|**備考**|**varchar (254)**|では [!INCLUDE[ssDE](../../includes/ssde-md.md)] 、このフィールドは常に NULL を返します。|  
  
## <a name="remarks"></a>解説  
 返されるデータベース名は、現在のデータベース状況を変更するために USE ステートメントでパラメーターとして使えます。  
  
 **sp_databases** には OPEN DATABASE CONNECTIVITY (ODBC) に相当するものはありません。  
  
## <a name="permissions"></a>アクセス許可  
 CREATE DATABASE、ALTER ANY DATABASE、または VIEW ANY DEFINITION 権限が必要です。また、データベースへのアクセス権限が必要です。 VIEW ANY DEFINITION 権限を拒否することはできません。  
  
## <a name="examples"></a>例  
 次の例では、 `sp_databases` を実行しています。  
  
```sql  
USE master;  
GO  
EXEC sp_databases;  
```  
  
## <a name="see-also"></a>参照  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [HAS_DBACCESS &#40;Transact-sql&#41;](../../t-sql/functions/has-dbaccess-transact-sql.md)  
  
  
