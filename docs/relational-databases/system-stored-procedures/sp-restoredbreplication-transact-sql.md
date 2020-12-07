---
description: sp_restoredbreplication (Transact-SQL)
title: sp_restoredbreplication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_restoredbreplication
- sp_restoredbreplication_TSQL
helpviewer_keywords:
- sp_restoredbreplication
ms.assetid: a2c5ee32-e6d9-46e9-8031-8ff13c20acf7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b64a39661fdceefade15d605ccc8e1c083ede0e6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541555"
---
# <a name="sp_restoredbreplication-transact-sql"></a>sp_restoredbreplication (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  バックアップ元以外のサーバー、データベース、またはシステムにデータベースを復元するとき、レプリケーション プロセスを実行できない場合に、レプリケーションの設定を削除します。 レプリケートされたデータベースを、バックアップが作成されたサーバーやデータベースとは別のサーバーまたはデータベースに復元する場合、レプリケーションの設定は保持できません。 復元時に、サーバーは **sp_restoredbreplication** を直接呼び出して、復元されたデータベースからレプリケーションメタデータを自動的に削除します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_restoredbreplication [ @srv_orig = ] 'original_server_name'  
        , [ @db_orig = ] 'original_database_name'  
    [ , [ @keep_replication = ] keep_replication ]  
    [ , [ @perform_upgrade = ] perform_upgrade ]  
```  
  
## <a name="arguments"></a>引数  
`[ @srv_orig = ] 'original_server_name'`  
 バックアップが作成されたサーバーの名前を指定します。 *original_server_name* は **sysname**であり、既定値はありません。  
  
`[ @db_orig = ] 'original_database_name'`  
 バックアップされたデータベースの名前。 *original_database_name* は **sysname**であり、既定値はありません。  
  
`[ @keep_replication = ] keep_replication`  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @perform_upgrade = ] perform_upgrade`  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_restoredbreplication** は、すべての種類のレプリケーションで使用されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_restoredbreplication**を実行できるのは、 **sysadmin**または**dbcreator**固定サーバーロールまたは**dbo**データベーススキーマのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
