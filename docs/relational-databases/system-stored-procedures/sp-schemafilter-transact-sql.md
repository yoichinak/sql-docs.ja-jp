---
description: sp_schemafilter (Transact-sql)
title: sp_schemafilter (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_schemafilter_TSQL
- sp_schemafilter
helpviewer_keywords:
- sp_schemafilter
ms.assetid: 199e869b-2cd2-44ee-b2ee-69edb06a1bc4
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 51edefb63c7ec075e89e9239636207625c4ba1dc
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541523"
---
# <a name="sp_schemafilter-transact-sql"></a>sp_schemafilter (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  パブリッシュの対象となる Oracle テーブルを一覧表示するときに除外されるスキーマに関する情報を変更して表示します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_schemafilter [ @publisher = ] 'publisher'   
   [ , [ @schema = ] 'schema' ]   
   [ , [ @operation = ] 'operation' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @publisher = ] 'publisher'` 以外のパブリッシャーの名前を指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publisher* は **sysname**で、既定値はありません。  
  
`[ @schema = ] 'schema'` スキーマの名前を指定します。 *スキーマ* は **sysname**で、既定値は NULL です。  
  
`[ @operation = ] 'operation'` このスキーマに対して実行するアクションを指定します。 *操作* は **nvarchar (4)**,、値は次のいずれかを指定することができます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**add**|指定されたスキーマを、パブリケーションに適合しないスキーマの一覧に追加します。|  
|**」**|指定されたスキーマを、パブリケーションに適合しないスキーマの一覧から削除します。|  
|**help**|パブリケーションに適さないスキーマの一覧を返します。|  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**schemaname**|**sysname**|パブリケーションに適合しないスキーマの名前を指定します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_schemafilter** は異種パブリッシャーにのみ使用してください。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_schemafilter**を実行できるのは、ディストリビューター側の固定サーバーロール**sysadmin**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
