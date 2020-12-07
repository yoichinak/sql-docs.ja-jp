---
description: CHECKPOINT (Transact-SQL)
title: CHECKPOINT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKPOINT_TSQL
- CHECKPOINT
dev_langs:
- TSQL
helpviewer_keywords:
- events [SQL Server], checkpoints
- automatic checkpoints
- writing dirty pages to disk
- pages [SQL Server], dirty
- checkpoints [SQL Server]
- CHECKPOINT statement
- log truncate mode [SQL Server]
- dirty pages
- logs [SQL Server], checkpoints
- manual checkpoints [SQL Server]
- pages [SQL Server], checkpoints
ms.assetid: ccdfc689-ad4e-44c0-83f7-0f2cfcfb6406
author: juliemsft
ms.author: jrasnick
ms.openlocfilehash: 3f2d5761829c38aba06f36b4d473c8ea9dc36214
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124490"
---
# <a name="checkpoint-transact-sql"></a>CHECKPOINT (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在接続している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースで手動チェックポイントを生成します。  
  
> [!NOTE]  
>  さまざまな種類のデータベース チェックポイントと一般的なチェックポイント操作については、「[データベース チェックポイント&#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
CHECKPOINT [ checkpoint_duration ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *checkpoint_duration*  
 手動チェックポイントを完了するのに必要な時間を秒単位で指定します。 *checkpoint_duration* を指定すると、[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] は、要求された時間内にチェックポイントを実行しようとします。 *checkpoint_duration* は、データ型が **int** の式で、0 より大きい値にする必要があります。 このパラメーターを省略すると、[!INCLUDE[ssDE](../../includes/ssde-md.md)] では、データベース アプリケーションのパフォーマンスに与える影響が最小限になるように、チェックポイントの持続時間が調整されます。 *checkpoint_duration* は拡張オプションです。  
  
## <a name="factors-affecting-the-duration-of-checkpoint-operations"></a>チェックポイントの操作時間に影響を与える要因  
 通常、書き込む必要のあるダーティ ページの数が増えると、チェックポイント操作に必要とされる時間が長くなります。 他のアプリケーションのパフォーマンスに与える影響を最小にするため、既定では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってチェックポイント操作による書き込み頻度が調節されます。 書き込みの頻度が減ると、チェックポイント操作の完了に必要な時間は長くなります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、*checkpoint_duration* 値が CHECKPOINT コマンドで指定されていない場合、この方法に基づいて手動チェックポイントが実行されます。  
  
 *checkpoint_duration* の使用によるパフォーマンスへの影響は、ダーティ ページの数、システムにあるアクティビティ、実際に指定された時間によって異なります。 たとえば、通常、チェックポイントが 120 秒で完了する場合、*checkpoint_duration* を 45 秒に設定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって、既定で割り当てられるリソースよりも多くのリソースがチェックポイントに割り当てられます。 逆に、*checkpoint_duration* を 180 秒に指定すると、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、既定で割り当てられるリソースよりも少ないリソースしか割り当てられません。 一般に、*checkpoint_duration* が短いとチェックポイントに割り当てるリソースが増え、*checkpoint_duration* が長いとチェックポイントに割り当てるリソースが減ります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、常に可能な限りチェックポイントを完了し、チェックポイントが完了するとすぐに CHECKPOINT ステートメントによって値が返されます。 したがってチェックポイントの完了は、状況に応じて、指定した時間よりも早まったり、遅くなったりすることがあります。  
  
##  <a name="security"></a><a name="Security"></a> セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 CHECKPOINT のアクセス許可は、**sysadmin** 固定サーバー ロールのメンバと、**db_owner** および **db_backupoperator** 固定データベース ロールのメンバに既定で割り当てられ、転送できません。  
  
## <a name="see-also"></a>参照  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [データベース チェックポイント &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)   
 [recovery interval サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)   
 [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)  
  
  
