---
description: sp_db_increased_partitions
title: sp_db_increased_partitions |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_increased_partitions_TSQL
- sp_db_increased_partitions
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_increased_partitions
ms.assetid: a8c043ec-b504-4929-ac0e-8babaa99d989
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0cac6cc79f06087b7ddd79dcd891ad370ad1338f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536616"
---
# <a name="sp_db_increased_partitions"></a>sp_db_increased_partitions
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定されたデータベースに対して最大15000のパーティションのサポートを有効または無効にします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dp_increased_partitions   
[ @dbname ] = 'database_name'   
[ , [ @increased_partitions = ] 'increased_partitions' ] [;]  
```  
  
## <a name="arguments"></a>引数  
 [ @dbname =] '*database_name*'  
 データベースの名前です。 *dbname* は **sysname** で、既定値は NULL です。 場合 *dbname* が指定されていない、現在のデータベースが使用されます。  
  
 [ @increased_partitions =] '*increased_partitions*'  
 指定したデータベースに対して 15, 000 個のパーティションのサポートを有効または無効にします。 *increased_partitions* は **varchar (6)** で、既定値は NULL です。 使用できる値は ' ON ' または ' TRUE ' で、サポートを有効にし、' OFF ' または ' FALSE ' を使用してサポートを無効にします。 *Increased_partitions*が指定されていない場合、指定されたデータベースに対してサポートが有効になっていることを示すために1を返し、サポートが無効になっていることを示す0を返します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 指定したデータベースに対する ALTER DATABASE 権限が必要です。  
  
  
