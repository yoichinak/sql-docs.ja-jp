---
description: sp_who (Transact-sql)
title: sp_who (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_who_TSQL
- sp_who
dev_langs:
- TSQL
helpviewer_keywords:
- sp_who
ms.assetid: 132dfb08-fa79-422e-97d4-b2c4579c6ac5
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a3d3af35b9d886e41d43e0c480c49a7e593e00f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463982"
---
# <a name="sp_who-transact-sql"></a>sp_who (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  のインスタンス内の現在のユーザー、セッション、およびプロセスに関する情報を提供 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] します。 情報をフィルター処理して、アイドル状態ではないプロセス、特定のユーザーに属するプロセス、または特定のセッションに属するプロセスのみを返すことができます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_who [ [ @loginame = ] 'login' | session ID | 'ACTIVE' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @loginame = ] 'login' | session ID | 'ACTIVE'` は、結果セットをフィルター処理するために使用されます。  
  
 *login* は、特定のログインに属するプロセスを識別する **sysname** です。  
  
 *セッション id* は、インスタンスに属するセッション識別番号です [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *セッション ID* は **smallint**です。  
  
 **ACTIVE** は、ユーザーから次のコマンドを待機しているセッションを除外します。  
  
 値を指定しない場合は、インスタンスに属するすべてのセッションがレポートされます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 **sp_who** は、次の情報を含む結果セットを返します。  
  
|列|データ型|説明|  
|------------|---------------|-----------------|  
|**spid**|**smallint**|セッション ID。|  
|**ecid**|**smallint**|特定のセッション ID に関連付けられている、指定されたスレッドの実行コンテキスト ID。<br /><br /> 0、1、2、3、...*n*}。ここで、0は常にメインスレッドまたは親スレッドを表し、{1, 2, 3,...*n*} サブスレッドを表します。|  
|**status**|**nchar(30)**|プロセスの状態。 次の値を指定できます。<br /><br /> **休止**。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でセッションがリセットされています。<br /><br /> を**実行して**います。 セッションで1つ以上のバッチが実行されています。 複数のアクティブな結果セット (MARS) が有効になっている場合、1つのセッションで複数のバッチを実行できます。 詳細については、「[複数のアクティブな結果セット &#40;MARS&#41; の使用](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)」を参照してください。<br /><br /> **バックグラウンド**。 このセッションでは、デッドロック検出などのバックグラウンドタスクが実行されています。<br /><br /> **ロールバック**。 セッションでトランザクション ロールバックが実行中です。<br /><br /> **保留中**。 セッションは、ワーカー スレッドが使用可能になるのを待機しています。<br /><br /> **runnable**。 セッションのタスクは、時間クォンタムの取得を待機している間に、スケジューラの実行可能キューにあります。<br /><br /> **spinloop**。 セッションのタスクはスピンロックの空きを待機しています。<br /><br /> **中断**されました。 セッションは、i/o などのイベントが完了するのを待機しています。|  
|**loginame**|**nchar(128)**|特定のプロセスに関連付けられているログイン名。|  
|**hostname**|**nchar(128)**|各プロセスのホスト名またはコンピューター名。|  
|**blk**|**char (5)**|ブロック中のプロセスが存在する場合は、そのプロセスのセッション ID。 存在しない場合は、この列は 0 になります。<br /><br /> 指定したセッション ID に関連付けられているトランザクションが、孤立した分散トランザクションによってブロックされている場合、この列はブロックしている孤立トランザクションに対して '-2 ' を返します。|  
|**dbname**|**nchar(128)**|プロセスによって使用されるデータベース。|  
|**cmd**|**nchar(16)**|[!INCLUDE[ssDE](../../includes/ssde-md.md)][!INCLUDE[tsql](../../includes/tsql-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] プロセスに対して実行されるコマンド (ステートメント、内部プロセスなど)。 SQL Server 2019 では、データ型が **nchar (26)** に変更されました。|  
|**request_id**|**int**|特定のセッションで実行されている要求の ID。|  
  
 並列処理の場合は、特定のセッション ID に対してサブスレッドが作成されます。 メイン スレッドは `spid = <xxx>` および `ecid =0` のように示されます。 他のサブスレッドは同じです `spid = <xxx>` が、 **d** > 0 になります。  
  
## <a name="remarks"></a>解説  
 排他ロックが設定されている可能性のあるブロックプロセスは、別のプロセスが必要とするリソースを保持しているプロセスです。  
  
 孤立したすべての分散トランザクションにセッション ID 値 '-2' が割り当てられます。 孤立した分散トランザクションとは、どのセッション ID にも関連付けられていない分散トランザクションです。 詳細については、「 [マークされたトランザクションを使用して関連するデータベースを一貫した状態に復元する方法 &#40;完全復旧モデル&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)」を参照してください。  
  
 システムプロセスをユーザープロセスから分離するには、dm_exec_sessions の **is_user_process** 列に対してクエリを実行します。  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで実行されているすべてのセッションを確認するには、サーバーに対する VIEW SERVER STATE 権限が必要です。 権限がない場合、ユーザーは現在のセッションだけを確認できます。  
  
## <a name="examples"></a>例  
  
### <a name="a-listing-all-current-processes"></a>A. 現在のすべてのプロセスを一覧表示する  
 次の例では、 `sp_who` パラメーターを指定せずにを使用して、現在のすべてのユーザーを報告します。  
  
```  
USE master;  
GO  
EXEC sp_who;  
GO  
```  
  
### <a name="b-listing-a-specific-users-process"></a>B. 特定のユーザーのプロセスを一覧表示する  
 次の例では、ログイン名を使用して、現在のユーザーに関する情報を表示します。  
  
```  
USE master;  
GO  
EXEC sp_who 'janetl';  
GO  
```  
  
### <a name="c-displaying-all-active-processes"></a>C. すべてのアクティブなプロセスを表示しています  
  
```  
USE master;  
GO  
EXEC sp_who 'active';  
GO  
```  
  
### <a name="d-displaying-a-specific-process-identified-by-a-session-id"></a>D. セッション ID で識別される特定のプロセスの表示  
  
```  
USE master;  
GO  
EXEC sp_who '10' --specifies the process_id;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_lock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [sys.sysプロセス &#40;Transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
