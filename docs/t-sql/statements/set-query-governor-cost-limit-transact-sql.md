---
description: SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL)
title: SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET QUERY_GOVERNOR_COST_LIMIT
- SET_QUERY_GOVERNOR_COST_LIMIT_TSQL
- QUERY_GOVERNOR_COST_LIMIT
- QUERY_GOVERNOR_COST_LIMIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET QUERY_GOVERNOR_COST_LIMIT statement
- connections [SQL Server], overriding
- QUERY_GOVERNOR_COST_LIMIT option
- overriding connection values
ms.assetid: 3424bb44-6915-462d-a8d7-fe834af81387
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bb7b16a18832bbdea950843409b0a17153c7a05b
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "89547474"
---
# <a name="set-query_governor_cost_limit-transact-sql"></a>SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在の接続に対して、現在の構成値 **query governor cost limit** をオーバーライドします。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
  
SET QUERY_GOVERNOR_COST_LIMIT value  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *value*  
 クエリの最大実行時間を表す数値または整数値です。 値は、最も近い整数に切り捨てられます。 負の値は 0 に切り上げられます。 クエリ ガバナーは、見積コストがこの値を超えるクエリの実行を許可しません。 このオプションに 0 (既定値) を指定すると、クエリ ガバナーが無効になり、すべてのクエリを永続的に実行できるようになります。  
  
 "クエリ コスト" とは、特定のハードウェア構成でクエリを完了するために必要とされる予測所要時間を秒単位で表したものです。  
  
## <a name="remarks"></a>解説  
 SET QUERY_GOVERNOR_COST_LIMIT の設定は現在の接続にだけ適用され、現在の接続が終了するまで有効です。 サーバー全体のクエリ制御コストの上限値を変更するには、[sp_configure](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md) の **query governor cost limit サーバー構成オプション** を構成します。 このオプションを構成する方法の詳細については、「[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)」および「[サーバー構成オプション &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)」を参照してください。  
  
 SET QUERY_GOVERNOR_COST_LIMIT は、解析時ではなく実行時に設定されます。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
