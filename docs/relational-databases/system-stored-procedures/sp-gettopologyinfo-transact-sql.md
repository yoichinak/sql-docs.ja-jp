---
description: sp_gettopologyinfo (Transact-sql)
title: sp_gettopologyinfo (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_gettopologyinfo_TSQL
- sp_gettopologyinfo
helpviewer_keywords:
- sp_gettopologyinfo
ms.assetid: 8bbe8a06-a4aa-4219-8402-12db6a4682c6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e6762b60612523b8150b791c3fcef19a82079968
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99197654"
---
# <a name="sp_gettopologyinfo-transact-sql"></a>sp_gettopologyinfo (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ピアツーピアトランザクションレプリケーショントポロジに関する情報を返します。 このプロシージャを実行する前に、 [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) を実行して情報を収集します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_gettopologyinfo [ @request_id = ] request_id  
```  
  
## <a name="arguments"></a>引数  
 [ @request_id =] *request_id*  
 トポロジ状態要求の ID を指定します。 *request_id* は **int**,、既定値は NULL です。 ID を取得するには、 @request_id [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) の出力パラメーターを使用するか、 [MSpeer_topologyrequest](../../relational-databases/system-tables/mspeer-topologyrequest-transact-sql.md) システムテーブルに対してクエリを実行します。  
  
## <a name="result-sets"></a>結果セット  
 sp_gettopologyinfo では、単一の XML 列で構成される結果セットが返されます。 XML 列のデータは、 [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) システムテーブルのデータと同じです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 sp_gettopologyinfo は、ピアツーピアトランザクションレプリケーションで使用されます。 Sp_gettopologyinfo を実行する前に [sp_requestpeertopologyinfo](../../relational-databases/system-stored-procedures/sp-requestpeertopologyinfo-transact-sql.md) を実行してください。 これらの手順は、ピアツーピアトポロジ構成ウィザードで使用されますが、XML 形式でトポロジ情報が必要な場合は、直接使用することもできます。 表形式の結果を優先する場合は、 [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) システムテーブルに対してクエリを実行します。  
  
## <a name="permissions"></a>アクセス許可  
 Sysadmin 固定サーバーロールまたは db_owner 固定データベースロールのメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
