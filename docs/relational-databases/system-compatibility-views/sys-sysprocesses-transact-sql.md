---
description: sys.sysのプロセス (Transact-sql)
title: sys.sysのプロセス (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysprocesses_TSQL
- sys.sysprocesses_TSQL
- sys.sysprocesses
- sysprocesses
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysprocesses compatibility view
- sysprocesses system table
ms.assetid: 60a36d36-54b3-4bd6-9cac-702205a21b16
author: rothja
ms.author: jroth
ms.openlocfilehash: 89e9bf9ab596e24148851f68ffa30515079fb51f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482081"
---
# <a name="syssysprocesses-transact-sql"></a>sys.sysのプロセス (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  のインスタンスで実行されているプロセスに関する情報を格納 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 これらのプロセスには、クライアントプロセスまたはシステムプロセスを使用できます。 sysprocesses にアクセスするには、master データベースのコンテキストからアクセスするか、3 つの要素から成る名前 (master.dbo.sysprocesses) を使用する必要があります。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|調べる|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セッション ID。|  
|kpid|**smallint**| Windows のスレッド ID です。|  
|ブロック済み|**smallint**|要求をブロックしているセッションの ID。 この列が NULL の場合は、要求がブロックされていないか、ブロックしているセッションのセッション情報が使用または識別できません。<br /><br /> -2 = ブロックしているリソースは、孤立した分散トランザクションが所有しています。<br /><br /> -3 = ブロックしているリソースは、遅延復旧トランザクションが所有しています。<br /><br /> -4 = 内部ラッチの状態遷移のため、ブロックしているラッチの所有者のセッション ID を特定できませんでした。|  
|waittype|**binary(2)**|予約済み。|  
|waittime|**bigint**|現在の待機時間 (ミリ秒単位) です。<br /><br /> 0 = プロセスは待機していません。|  
|lastwaittype|**nchar(32)**|最後または現在の待機の種類の名前を示す文字列。|  
|waitresource|**nchar(256)**|ロックリソースのテキスト表現。|  
|dbid|**smallint**|プロセスによって現在使用されているデータベースの ID。|  
|uid|**smallint**|コマンドを実行したユーザーの ID。 ユーザーおよびロールの数が32767を超えた場合、オーバーフローまたは NULL を返します。|  
|cpu|**int**|プロセスの累積 CPU 時間。 SET STATISTICS TIME オプションが ON と OFF のどちらであるかに関係なく、すべてのプロセスのエントリが更新されます。|  
|physical_io|**bigint**|プロセスの累積ディスクの読み取りと書き込み。|  
|memusage|**int**|このプロセスに現在割り当てられているプロシージャキャッシュ内のページ数。 負の値は、プロセスが別のプロセスによって割り当てられたメモリを解放していることを示します。|  
|login_time|**datetime**|クライアントプロセスがサーバーにログインした時刻。|  
|last_batch|**datetime**|クライアントプロセスがリモートストアドプロシージャ呼び出しまたは EXECUTE ステートメントを最後に実行した時刻。|  
|ecid|**smallint**|1つのプロセスに代わって動作するサブスレッドを一意に識別するために使用される実行コンテキスト ID。|  
|open_tran|**smallint**|プロセスの開いているトランザクションの数。|  
|status|**nchar(30)**|プロセス ID の状態。 次の値を指定できます。<br /><br /> **休止中**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]セッションをリセットしています。<br /><br /> **running** = セッションで1つ以上のバッチが実行されています。 複数のアクティブな結果セット (MARS) が有効になっている場合、1つのセッションで複数のバッチを実行できます。 詳細については、「[複数のアクティブな結果セット &#40;MARS&#41; の使用](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)」を参照してください。<br /><br /> **background** = セッションは、デッドロック検出などのバックグラウンドタスクを実行しています。<br /><br /> **rollback** = セッションでトランザクションのロールバックが進行中です。<br /><br /> **pending** = セッションは、ワーカースレッドが使用可能になるのを待機しています。<br /><br /> 実行**可能 = セッション**のタスクは、時間の経過を待機している間に、スケジューラの実行可能キューにあります。<br /><br /> **spinloop** = セッションのタスクは、スピンロックが解放されるのを待機しています。<br /><br /> **中断** = セッションは、i/o などのイベントが完了するのを待機しています。|  
|sid|**binary(86)**|ユーザーのグローバル一意識別子 (GUID)。|  
|hostname|**nchar(128)**|ワークステーションの名前。|  
|program_name|**nchar(128)**|アプリケーション プログラム名です。|  
|hostprocess|**nchar(10)**|ワークステーションプロセス ID 番号。|  
|cmd|**nchar (52)**|現在実行中のコマンドです。|  
|nt_domain|**nchar(128)**|クライアント (Windows 認証を使用している場合)、または信頼関係接続の  Windows ドメインです。|  
|nt_username|**nchar(128)**|プロセスの windows ユーザー名 (Windows 認証を使用している場合)、または信頼関係接続の場合は。|  
|net_address|**nchar(12)**|各ユーザーのワークステーションにあるネットワーク アダプターに割り当てられている一意識別子です。 ユーザーがログインすると、この識別子が net_address 列に挿入されます。|  
|net_library|**nchar(12)**|クライアントのネットワークライブラリが格納されている列。 各クライアント プロセスはネットワーク接続を行います。 ネットワーク接続には、接続を確立するためのネットワークライブラリが関連付けられています。|  
|loginame|**nchar(128)**|ログイン名。|  
|context_info|**binary(128)**|SET CONTEXT_INFO ステートメントを使用してバッチに格納されたデータ。|  
|sql_handle|**binary(20)**|現在実行されているバッチまたはオブジェクトを表します。<br /><br /> **メモ** この値は、オブジェクトのバッチまたはメモリアドレスから取得されます。 この値は、ハッシュベースのアルゴリズムを使用して計算されません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。|  
|stmt_start|**int**|指定された sql_handle の現在の SQL ステートメントの開始オフセットです。|  
|stmt_end|**int**|指定した sql_handle の現在の SQL ステートメントの終了オフセットです。<br /><br /> -1 = 現在のステートメントは、指定した sql_handle に対して fn_get_sql 関数が返す結果の最後まで実行されます。|  
|request_id|**int**|要求の ID。 特定のセッションで実行されている要求を識別するために使用されます。|
|page_resource |**binary (8)** |**適用対象**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] <br /><br /> `waitresource`列にページが含まれている場合は、ページリソースの8バイトの16進数表現。 |  
  
## <a name="remarks"></a>解説  
 ユーザーがサーバーに対する VIEW SERVER STATE 権限を持っている場合、ユーザーにはのインスタンスで実行中のすべてのセッションが表示されます。それ以外の場合、ユーザーには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 現在のセッションのみが表示されます。  
  
## <a name="see-also"></a>参照  
 [実行関連の動的管理ビューおよび関数 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [システムビューへのシステムテーブルのマッピング &#40;Transact-sql&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
