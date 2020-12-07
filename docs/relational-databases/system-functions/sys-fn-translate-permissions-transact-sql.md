---
description: sys.fn_translate_permissions (Transact-SQL)
title: fn_translate_permissions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_translate_permissions
- sys.fn_translate_permissions_TSQL
- fn_translate_permissions
- fn_translate_permissions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- permissions bitmask [SQL Server]
- sys.fn_translate_permissions function
- fn_translate_permissions function
ms.assetid: ac97121f-2bd0-4f71-8e45-42c8584edbc5
author: rothja
ms.author: jroth
ms.openlocfilehash: 1069d5b76d6ee404ddd2e671eb6a7b63396424ee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481765"
---
# <a name="sysfn_translate_permissions-transact-sql"></a>sys.fn_translate_permissions (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SQL トレースによって返されるアクセス許可のビットマスクを権限名のテーブルに変換します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.fn_translate_permissions ( level , perms )  
```  
  
## <a name="arguments"></a>引数  
 *level*  
 権限が適用されるセキュリティ保護可能なリソースの種類を指定します。 *レベル* は **nvarchar (60)** です。  
  
 *perms*  
 権限列に返されるビットマスクを指定します。 *perms* は **varbinary (16)** です。  
  
## <a name="returns"></a>戻り値  
 **テーブル**  
  
## <a name="remarks"></a>解説  
 SQL トレースの **permissions** 列に返される値は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 有効な権限を計算するためにによって使用されるビットマスクを整数で表したものです。 25種類の securables にはそれぞれ、対応する数値を持つ独自のアクセス許可セットがあります。 **fn_translate_permissions** は、このビットマスクを権限名のテーブルに変換します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="example"></a>例  
 次のクエリでは、を使用して、 `sys.fn_builtin_permissions` 証明書に適用されるアクセス許可を表示し、を使用して `sys.fn_translate_permissions` アクセス許可のビットマスクの結果を返します。  
  
```  
SELECT * FROM sys.fn_builtin_permissions('CERTIFICATE');  
SELECT '0001' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0001);  
SELECT '0010' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0010);  
SELECT '0011' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0011);  
```  
  
## <a name="see-also"></a>参照  
 [アクセス許可 &#40;データベース エンジン&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)  
  
  
