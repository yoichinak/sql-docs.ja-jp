---
description: sp_dropmergealternatepublisher (Transact-sql)
title: sp_dropmergealternatepublisher (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_dropmergealternatepublisher
- sp_dropmergealternatepublisher_TSQL
helpviewer_keywords:
- sp_dropmergealternatepublisher
ms.assetid: a7dee4e2-2a60-41da-9d1d-6f991d7e2c5e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5d787648f197c54623ba305503ddd878a3a7061d
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99208279"
---
# <a name="sp_dropmergealternatepublisher-transact-sql"></a>sp_dropmergealternatepublisher (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マージパブリケーションから代替パブリッシャーを削除します。 このストアドプロシージャは、サブスクライバー側のサブスクリプションデータベースで実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dropmergealaternatepublisher [ @publisher = ] 'publisher'    , [ @publisher_db = ] 'publisher_db'    , [ @publication = ] 'publication'    , [ @alternate_publisher = ] 'alternate_publisher'    , [ @alternate_publisher_db = ] 'alternate_publisher_db'    , [ @alternate_publication = ] 'alternate_publication'  
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` 現在のパブリッシャーの名前を指定します。 *publisher* は **sysname** で、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'` 現在のパブリケーションデータベースの名前を指定します。 *publisher_db* は **sysname** であり、既定値はありません。  
  
`[ @publication = ] 'publication'` 現在のパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @alternate_publisher = ] 'alternate_publisher'` 代替同期パートナーとして削除する代替パブリッシャーの名前を指定します。 *alternate_publisher* は **sysname** であり、既定値はありません。  
  
`[ @alternate_publisher_db = ] 'alternate_publisher_db'` 代替同期パートナーパブリケーションデータベースとして削除するパブリケーションデータベースの名前を指定します。 *alternate_publisher_db* は **sysname** であり、既定値はありません。  
  
`[ @alternate_publication = ] 'alternate_publication'` 代替同期パートナーパブリケーションとして削除するパブリケーションの名前を指定します。 *alternate_publication* は **sysname** であり、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_dropmergealternatepublisher** は、マージレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_dropmergelternatepublisher** を実行できるのは、固定サーバーロール **sysadmin** または固定データベースロール **db_owner** のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [sp_addmergealternatepublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergealternatepublisher-transact-sql.md)  
  
  
