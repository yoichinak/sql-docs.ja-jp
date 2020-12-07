---
description: sp_copymergesnapshot (Transact-SQL)
title: sp_copymergesnapshot (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_copymergesnapshot
- sp_copymergesnapshot_TSQL
helpviewer_keywords:
- sp_copymergesnapshot
ms.assetid: eaecd6e0-8486-4e5d-ace7-8ae75768c0a8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4f763c28087802df2dd3922b54829f6dee888545
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536665"
---
# <a name="sp_copymergesnapshot-transact-sql"></a>sp_copymergesnapshot (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  指定されたパブリケーションのスナップショットフォルダーを** \@ destination_folder**に一覧表示されているフォルダーにコピーします。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_copymergesnapshot [ @publication = ] 'publication', [ @destination_folder = ] 'destination_folder'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` スナップショットの内容をコピーするパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @destination_folder = ] 'destination_folder'` パブリケーションスナップショットの内容をコピーするフォルダーの名前を指定します。 *destination_folder*は **nvarchar (255)**,、既定値はありません。 *Destination_folder*は、別のサーバー、ネットワークドライブ、リムーバブルメディア (cd-rom やリムーバブルディスクなど) などの別の場所にすることができます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_copymergesnapshot** は、マージレプリケーションで使用します。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョン7.0 以前を実行しているサブスクライバーでは、代替スナップショットの場所を使用できません。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_copymergesnapshot**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [代替スナップショットフォルダーの場所](../../relational-databases/replication/snapshot-options.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
