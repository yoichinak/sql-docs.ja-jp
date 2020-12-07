---
title: sp_repldone (Transact-sql) |Microsoft Docs
description: サーバーで最後にディストリビュートされたトランザクションを識別するレコードを更新します。 このストアドプロシージャは、パブリッシャー側のパブリケーションデータベースで実行されます。
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repldone
- sp_repldone_TSQL
helpviewer_keywords:
- sp_repldone
ms.assetid: 045d3cd1-712b-44b7-a56a-c9438d4077b9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7a8e32127986fb67a28abfa2433caefc044ed1b2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538592"
---
# <a name="sp_repldone-transact-sql"></a>sp_repldone (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  サーバーで最後にディストリビュートされたトランザクションを識別するレコードを更新します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
> [!CAUTION]  
>  手作業で **sp_repldone** を実行すると、配布されたトランザクションの順序および一貫性を無効にする可能性があります。 **sp_repldone** は、経験豊富なレプリケーションサポート担当者が指示するように、レプリケーションのトラブルシューティングにのみ使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```
sp_repldone [ @xactid= ] xactid   
        , [ @xact_seqno= ] xact_seqno   
    [ , [ @numtrans= ] numtrans ]   
    [ , [ @time= ] time   
    [ , [ @reset= ] reset ]  
```  
  
## <a name="arguments"></a>引数  
`[ @xactid = ] xactid` サーバーの最後に分散されたトランザクションの最初のレコードのログシーケンス番号 (LSN) を指定します。 *xactid* は **binary (10)**,、既定値はありません。  
  
`[ @xact_seqno = ] xact_seqno` サーバーの最後に分散されたトランザクションの最後のレコードの LSN を示します。 *xact_seqno* は **binary (10)**,、既定値はありません。  
  
`[ @numtrans = ] numtrans` 分散されているトランザクションの数を指定します。 *numtrans* は **int**,、既定値はありません。  
  
`[ @time = ] time` トランザクションの最後のバッチを配布するために必要な時間 (ミリ秒単位) を指定します。 *time* は **int**,、既定値はありません。  
  
`[ @reset = ] reset` リセットの状態を示します。 *reset* は **int**,、既定値はありません。 **1**の場合、ログ内のすべてのレプリケートされたトランザクションは、分散としてマークされます。 **0**の場合、トランザクションログは最初のレプリケートされたトランザクションにリセットされ、レプリケートされたトランザクションは配信済みとしてマークされません。 *reset* は、 *xactid* と *xact_seqno* の両方が NULL の場合にのみ有効です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_repldone** は、トランザクションレプリケーションで使用します。  
  
 **sp_repldone** は、配布されたトランザクションを追跡するために、ログリーダープロセスによって使用されます。  
  
 **Sp_repldone**を使用すると、トランザクションがレプリケートされた (ディストリビューターに送信された) ことをサーバーに手動で通知できます。 また、レプリケーションを待機しているトランザクションを次のように変更することもできます。 レプリケートされたトランザクションの一覧で、前方または後方に移動できます。 このトランザクションおよびそれ以前のトランザクションはすべてディストリビュートされたことを示すマークが付きます。  
  
 必要なパラメーター *xactid* と *xact_seqno* は **sp_repltrans** または **sp_replcmds**を使用して取得できます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールまたは**db_owner**固定データベースロールのメンバーは、 **sp_repldone**を実行できます。  
  
## <a name="examples"></a>例  
 *Xactid*が null の場合、 *xact_seqno*が null で、 *reset*が**1**の場合、ログ内のすべてのレプリケートされたトランザクションが分散としてマークされます。 これは、トランザクションログに有効ではなく、ログを切り捨てる必要があるトランザクションがレプリケートされている場合に便利です。次に例を示します。  
  
```sql
EXEC sp_repldone @xactid = NULL, @xact_seqno = NULL, @numtrans = 0, @time = 0, @reset = 1  
```  
  
> [!CAUTION]  
>  このプロシージャは、レプリケーションを保留しているトランザクションが存在するときにトランザクション ログの切り詰めを許可する、緊急の場合に使用できます。  
  
## <a name="see-also"></a>参照  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_replflush &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [sp_repltrans &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
