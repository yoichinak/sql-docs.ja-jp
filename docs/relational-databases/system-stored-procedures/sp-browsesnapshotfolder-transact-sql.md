---
description: sp_browsesnapshotfolder (Transact-sql)
title: sp_browsesnapshotfolder (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_browsesnapshotfolder
- sp_browsesnapshotfolder_TSQL
helpviewer_keywords:
- sp_browsesnapshotfolder
ms.assetid: 0872edf2-4038-4bc1-a68d-05ebfad434d2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 61ac8c7567247e87afa927348592a0f0dacbb382
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548255"
---
# <a name="sp_browsesnapshotfolder-transact-sql"></a>sp_browsesnapshotfolder (Transact-sql)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  パブリケーションに対して生成された最新のスナップショットの完全なパスを返します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_browsesnapshotfolder [@publication= ] 'publication'  
    { [ , [ @subscriber = ] 'subscriber' ]  
 [ , [ @subscriber_db = ] 'subscriber_db' ] }  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` アーティクルを含むパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @subscriber = ] 'subscriber'` サブスクライバーの名前を指定します。 *サブスクライバー* の **sysname**,、既定値は NULL です。  
  
`[ @subscriber_db = ] 'subscriber_db'` サブスクリプションデータベースの名前を指定します。 *subscriber_db* は **sysname**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**snapshot_folder**|**nvarchar(512)**|スナップショットディレクトリへの完全パスです。|  
  
## <a name="remarks"></a>解説  
 **sp_browsesnapshotfolder** は、スナップショットレプリケーションおよびトランザクションレプリケーションで使用します。  
  
 *サブスクライバー*と*subscriber_db*のフィールドが NULL のままになっている場合、ストアドプロシージャは、パブリケーションに対して検索できる最新のスナップショットのスナップショットフォルダーを返します。 *サブスクライバー*と*subscriber_db*のフィールドが指定されている場合、ストアドプロシージャは、指定されたサブスクリプションのスナップショットフォルダーを返します。 パブリケーションに対するスナップショットが生成されていない場合は、空の結果セットが返されます。  
  
 パブリッシャーの作業ディレクトリとパブリッシャーのスナップショットフォルダーの両方でスナップショットファイルを生成するようにパブリケーションが設定されている場合、結果セットには2つの行が含まれます。 第 1 の行にはパブリケーションのスナップショット フォルダーが含まれ、第 2 の行にはパブリッシャーの作業ディレクトリが含まれます。 **sp_browsesnapshotfolder** は、スナップショットファイルが生成されるディレクトリを特定するのに役立ちます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_browsesnapshotfolder**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
