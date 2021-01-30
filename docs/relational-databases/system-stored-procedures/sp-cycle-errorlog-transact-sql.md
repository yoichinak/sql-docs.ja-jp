---
description: sp_cycle_errorlog (Transact-SQL)
title: sp_cycle_errorlog (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_cycle_errorlog_TSQL
- sp_cycle_errorlog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cycle_errorlog
ms.assetid: 61a12cbf-78a3-4052-8604-3b29d07573fd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b75b9e0c056a86a8ad67d1a739214a46f88533f3
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99203168"
---
# <a name="sp_cycle_errorlog-transact-sql"></a>sp_cycle_errorlog (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のエラーログファイルを閉じ、サーバーの再起動と同様にエラーログの拡張番号を循環します。 新しいエラー ログには、バージョンおよび著作権の情報と、新しいログが作成されたことを示す行が含まれます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cycle_errorlog  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]が開始されるたびに、現在のエラーログの名前が "エラーログ" に変更され **ます。 1**;**エラーログ 1** は **エラーログ** になります。2、**エラーログ** 2 は **エラーログ 3** になります。 **sp_cycle_errorlog** を使用すると、サーバーを停止して起動しなくてもエラーログファイルを循環することができます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_cycle_errorlog** の実行権限は、 **sysadmin** 固定サーバーロールのメンバーに制限されています。  
  
## <a name="examples"></a>例  
 次の例では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログを使い回します。  
  
```  
EXEC sp_cycle_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cycle_agent_errorlog &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cycle-agent-errorlog-transact-sql.md)  
  
  
