---
description: sp_addscriptexec (Transact-sql)
title: sp_addscriptexec (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addscriptexec
- sp_addscriptexec_TSQL
helpviewer_keywords:
- sp_addscriptexec
ms.assetid: 1627db41-6a80-45b6-b0b9-c0b7f9a1c886
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 81d3b8ac9e8eda12ed27099fed5623d0fd3da489
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536763"
---
# <a name="sp_addscriptexec-transact-sql"></a>sp_addscriptexec (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  SQL スクリプト (.sql ファイル) をパブリケーションのすべてのサブスクライバーにポストします。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addscriptexec [ @publication = ] publication  
    [ , [ @scriptfile = ] 'scriptfile' ]  
    [ , [ @skiperror = ] 'skiperror' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @scriptfile = ] 'scriptfile'` SQL スクリプトファイルへの完全なパスです。 *scriptfile* は **nvarchar (4000)**,、既定値はありません。  
  
`[ @skiperror = ] 'skiperror'` スクリプトの処理中にエラーが発生した場合に、ディストリビューションエージェントまたはマージエージェントを停止するかどうかを示します。 *SkipError* は **ビット**,、既定値は0です。  
  
 **0** = エージェントは停止します。  
  
 **1** = エージェントはスクリプトを続行し、エラーを無視します。  
  
`[ @publisher = ] 'publisher'` 以外のパブリッシャーを指定し [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publisher* は **sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーからパブリッシュする場合は、*パブリッシャー*を使用しないでください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_addscriptexec** は、トランザクションレプリケーションおよびマージレプリケーションで使用します。  
  
 **sp_addscriptexec** は、スナップショットレプリケーションには使用されません。  
  
 **Sp_addscriptexec**を使用するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービスアカウントに、スナップショットの場所に対する読み取り権限と書き込み権限、およびスクリプトが格納されている場所に対する読み取り権限が必要です。  
  
 [Sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)は、サブスクライバーでスクリプトを実行するために使用されます。スクリプトは、サブスクリプションデータベースに接続するときに、ディストリビューションエージェントまたはマージエージェントによって使用されるセキュリティコンテキストで実行されます。 以前のバージョンのでエージェントを実行すると [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、 [sqlcmd](../../tools/sqlcmd-utility.md)ではなく[osql ユーティリティ](../../tools/osql-utility.md)が使用されます。  
  
 **sp_addscriptexec** は、スクリプトをサブスクライバーに適用する場合に役立ちます。 [sqlcmd](../../tools/sqlcmd-utility.md) を使用して、スクリプトの内容をサブスクライバーに適用します。 ただし、サブスクライバー構成は異なることがあるので、パブリッシャーにポストする前にテストしたスクリプトでも、サブスクライバーでエラーが生じる可能性があります。 *skiperror* は、ディストリビューションエージェントまたはマージエージェントエラーを無視して続行する機能を提供します。 [Sqlcmd](../../tools/sqlcmd-utility.md)を使用して、 **sp_addscriptexec**を実行する前にスクリプトをテストします。  
  
> [!NOTE]  
>  スキップされたエラーは、参照のためにエージェント履歴に引き続き記録されます。  
  
 スナップショット配信に FTP を使用してパブリケーションのスクリプトファイルをポストするために **sp_addscriptexec** を使用することは、サブスクライバーに対してのみサポートされてい [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addscriptexec**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [同期中にスクリプトを実行 &#40;レプリケーション Transact-sql プログラミング&#41;](../../relational-databases/replication/execute-scripts-during-synchronization-replication-transact-sql-programming.md)   
 [データの同期](../../relational-databases/replication/synchronize-data.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
