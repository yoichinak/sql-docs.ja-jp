---
description: '&#x40;&#x40;MAX_CONNECTIONS (Transact-SQL)'
title: '@@MAX_CONNECTIONS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- '@@MAX_CONNECTIONS'
- '@@MAX_CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- simultaneous connections [SQL Server]
- maximum number of simultaneous user connections
- '@@MAX_CONNECTIONS function'
- connections [SQL Server], simultaneous
- number of simultaneous user connections
ms.assetid: 57eb9f4b-548f-4212-9684-a11d831c4732
author: cawrites
ms.author: chadam
ms.openlocfilehash: 67e4a3868e852a7bd454347e8e1e4b9c5a7fade4
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99160245"
---
# <a name="x40x40max_connections-transact-sql"></a>&#x40;&#x40;MAX_CONNECTIONS (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで同時に確立できるユーザー接続の最大数を返します。 返される数値は必ずしも現在構成されている数値ではありません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql  
@@MAX_CONNECTIONS  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 **integer**  
  
## <a name="remarks"></a>注釈  
 実際に可能なユーザー接続数は、インストールされている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンと、アプリケーションおよびハードウェアの制限により異なります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で可能な接続数が少なくなるように再構成するには、**sp_configure** を使用します。  
  
## <a name="examples"></a>例  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにおけるユーザー接続の最大数を返します。 この例では、接続数が少なくなるよう [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再構成していないことを前提としています。  
  
```sql 
SELECT @@MAX_CONNECTIONS AS 'Max Connections';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Max Connections  
---------------  
32767            
```  
  
## <a name="see-also"></a>参照  
 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [構成関数](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [user connections サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
  
  
