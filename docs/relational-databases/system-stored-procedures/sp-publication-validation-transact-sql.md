---
description: sp_publication_validation (Transact-SQL)
title: sp_publication_validation (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_publication_validation
- sp_publication_validation_TSQL
helpviewer_keywords:
- sp_publication_validation
ms.assetid: 06be2363-00c0-4936-97c1-7347f294a936
author: markingmyname
ms.author: maghan
ms.openlocfilehash: dccdb0f168b7b1e113a38c64a111e35e5bf62d77
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535002"
---
# <a name="sp_publication_validation-transact-sql"></a>sp_publication_validation (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  指定されたパブリケーション内の各アーティクルに対して、アーティクル検証要求を開始します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_publication_validation [ @publication = ] 'publication'  
    [ , [ @rowcount_only = ] type_of_check_requested ]  
    [ , [ @full_or_fast = ] full_or_fast ]  
    [ , [ @shutdown_agent = ] shutdown_agent ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @rowcount_only = ] 'rowcount_only'` テーブルの行数のみを返すかどうかを指定します。 *rowcount_only* は **smallint** であり、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**0**|互換性の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ある7.0 のチェックサムを実行します。<br /><br /> 注: アーティクルが行方向にフィルター選択されている場合、チェックサム操作ではなく rowcount 操作が実行されます。|  
|**1** (既定値)|行数チェックのみを実行します。|  
|**2**|行数とバイナリチェックサムを実行します。<br /><br /> 注: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] バージョン7.0 のサブスクライバーの場合、行数の検証のみが実行されます。|  
  
`[ @full_or_fast = ] 'full_or_fast'` 行数を計算するために使用されるメソッドです。 *full_or_fast* は **tinyint** で、次のいずれかの値を指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**0**|COUNT(*) を使用してフル カウントします。|  
|**1**|Sysindexes から高速にカウントさ **れ**ます。 [sys.sysインデックス](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md)の行のカウントは、実際のテーブルの行をカウントするよりもはるかに高速です。 ただし、 [sys.sysインデックス](../../relational-databases/system-compatibility-views/sys-sysindexes-transact-sql.md) は遅延更新されるため、行数が正確でない場合があります。|  
|**2** (既定値)|最初に高速カウントを試み、条件高速カウントを行います。 Fast メソッドが相違点を示している場合、は完全なメソッドに戻ります。 *Expected_rowcount*が NULL で、ストアドプロシージャを使用して値を取得している場合は、常に完全なカウント (*) が使用されます。|  
  
`[ @shutdown_agent = ] 'shutdown_agent'` 検証の完了時にディストリビューションエージェントを直ちにシャットダウンするかどうかを指定します。 *shutdown_agent* は **ビット**,、既定値は **0**です。 **0**の場合、レプリケーションエージェントはシャットダウンされません。 **1**の場合、最後の記事が検証された後にレプリケーションエージェントがシャットダウンします。  
  
`[ @publisher = ] 'publisher'` 以外のパブリッシャーを指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *publisher* は **sysname**で、既定値は NULL です。  
  
> [!NOTE]  
>  パブリッシャーの検証を要求するときは、*パブリッシャー*を使用しないでください [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_publication_validation** は、トランザクションレプリケーションで使用します。  
  
 **sp_publication_validation** は、パブリケーションに関連付けられているアーティクルがアクティブ化された後でいつでも呼び出すことができます。 この手順は、データを検証する定期的にスケジュールされたジョブの一部として、手動で (1 回) または実行することができます。  
  
 アプリケーションに即時更新サブスクライバーがある場合、 **sp_publication_validation** は誤ったエラーを検出することがあります。 **sp_publication_validation** は、最初にパブリッシャーで行数またはチェックサムを計算し、次にサブスクライバーで計算します。 行数またはチェックサムがパブリッシャーで完了していて、サブスクライバーでは完了していない場合、即時更新トリガーはサブスクライバーからパブリッシャーに更新を通知できるため、値が変更される可能性があります。 パブリケーションの検証中にサブスクライバーとパブリッシャーの値が変更されないようにするには、検証中のパブリッシャーでの Microsoft 分散トランザクション コーディネーター (MS DTC) サービスを停止します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_publication_validation**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [サブスクライバーでデータを検証する](../../relational-databases/replication/validate-data-at-the-subscriber.md)   
 [sp_article_validation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)   
 [sp_table_validation &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-table-validation-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
