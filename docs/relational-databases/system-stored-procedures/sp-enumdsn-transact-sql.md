---
description: sp_enumdsn (Transact-sql)
title: sp_enumdsn (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_enumdsn
- sp_enumdsn_TSQL
helpviewer_keywords:
- sp_enumdsn
ms.assetid: 171cbc7d-7406-4cb0-8602-9405243bfd1d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 711957655b7bb918fa49834160fd63329eb80343
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99193605"
---
# <a name="sp_enumdsn-transact-sql"></a>sp_enumdsn (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  特定の [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows ユーザー アカウントで実行中のサーバーに定義されている、すべての ODBC および OLE DB のデータ ソース名の一覧を返します。 このストアドプロシージャは、パブリッシャー側で任意のデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_enumdsn  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**データ ソース名**|**sysname**|データソースの名前。|  
|**説明**|**varchar(255)**|データ ソースの説明です。|  
|**Type**|**int**|データ ソースの種類です。<br /><br /> **1** = ODBC DSN<br /><br /> **3** = データソースの OLE DB|  
|**プロバイダー名**|**varchar(255)**|OLE DB プロバイダーの名前です。 ODBC DSN の場合、値は NULL です。|  
  
## <a name="remarks"></a>コメント  
 すべての [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスにユーザーコンテキストがあります。 ユーザーコンテキストは、ユーザーの ODBC データソースの定義を含むレジストリエントリのセットです。 ユーザーコンテキストは、が実行されているユーザー名によって提供され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 たとえば、サーバーがシステムアカウントのユーザーコンテキストで実行されている場合、返されるデータソース名 (Dsn) はすべて、システムアカウントに関連付けられているシステム Dsn になります。 サーバーがプライベートユーザーアカウントで実行されている場合は、そのユーザーのそのプライベートアカウントに対して定義されている Dsn だけが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_enumdsn** を実行できるのは、 **sysadmin** 固定サーバーロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_dsninfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dsninfo-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
