---
description: sp_syscollector_delete_collector_type (Transact-SQL)
title: sp_syscollector_delete_collector_type (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_delete_collector_type
- sp_syscollector_delete_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_delete_collector_type
ms.assetid: 3f32905e-0005-42cb-aef1-7bd04c51fbac
author: markingmyname
ms.author: maghan
ms.openlocfilehash: cc4cdc682ec2230b7d0f3136feb683789b38c06b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547352"
---
# <a name="sp_syscollector_delete_collector_type-transact-sql"></a>sp_syscollector_delete_collector_type (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  コレクター型の定義を削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_delete_collector_type [[ @collector_type_uid = ] 'collector_type_uid' ]  
          , [[ @name = ] 'name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @collector_type_uid = ] 'collector_type_uid'` コレクター型の GUID を示します。 *collector_type_uid* は **uniqueidentifier** で、 *name* が NULL の場合は値を持つ必要があります。  
  
`[ @name = ] 'name'` コレクター型の名前を指定します。 *名前* は **sysname** であり、 *collector_type_uid* が NULL の場合は値を持つ必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 *Collector_type_uid*または*名前*には値を指定する必要があります。どちらも NULL にすることはできません。  
  
 このコレクション型のコレクションアイテムが存在する場合、このプロシージャはエラーをスローします。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、 **dc_admin** (EXECUTE 権限を持つ) 固定データベースロールのメンバーシップが必要です。  
  
## <a name="example"></a>例  
 次の例では、ジェネリック T-SQL Query コレクター型を削除します。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_delete_collector_type @collector_type_uid = '302E93D1-3424-4be7-AA8E-84813ECF2419';  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)  
  
  
