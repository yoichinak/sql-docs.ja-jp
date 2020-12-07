---
description: sp_resetstatus (Transact-SQL)
title: sp_resetstatus (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_resetstatus
- sp_resetstatus_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_resetstatus
ms.assetid: b892727f-ea3b-4b94-88d9-f2386ad4962c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f76738491704d04b033126f88750670eec230a38
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541551"
---
# <a name="sp_resetstatus-transact-sql"></a>sp_resetstatus (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  問題のあるデータベースの状態をリセットします。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [ALTER database](../../t-sql/statements/alter-database-transact-sql.md) を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_resetstatus [ @dbname = ] 'database'  
```  
  
## <a name="arguments"></a>引数  
 [ @dbname =] '*データベース*'  
 リセットするデータベースの名前を指定します。 *データベースのデータ* 型は **sysname**で、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 sp_resetstatus では、データベースの未確認フラグがオフにされます。 また、このプロシージャによって、sys.databases 内の指定のデータベースのモード列と状態列が更新されます。 このプロシージャを実行する前には、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログを検討し、すべての問題を解決しておいてください。 sp_resetstatus を実行した後は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを停止し再起動します。  
  
 データベースは、いくつかの理由で問題ありの状態になる可能性があります。 その原因としては、オペレーティング システムによるデータベース リソースへのアクセス拒否や、データベース ファイルが利用できな場合や損傷している場合が考えられます。  
  
## <a name="permissions"></a>アクセス許可  
 sysadmin 固定サーバー ロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、データベースの状態をリセットし `AdventureWorks2012` ます。  
  
```  
EXEC sp_resetstatus 'AdventureWorks2012';  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
