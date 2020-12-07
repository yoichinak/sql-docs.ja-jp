---
description: sp_syscollector_update_collection_set (Transact-sql)
title: sp_syscollector_update_collection_set (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_update_collection_set_TSQL
- sp_syscollector_update_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_update_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 2dccc3cd-0e93-4e3e-a4e5-8fe89b31bd63
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fd55d65173d190d1c28708bfae46b10eaa0030a4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534841"
---
# <a name="sp_syscollector_update_collection_set-transact-sql"></a>sp_syscollector_update_collection_set (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ユーザー定義のコレクションセットのプロパティを変更したり、ユーザー定義のコレクションセットの名前を変更したりするために使用します。  
  
> [!WARNING]  
>  プロキシとして構成されている Windows アカウントが、まだログインしていない非対話型または対話型ユーザーである場合、プロファイルディレクトリは存在せず、ステージングディレクトリの作成は失敗します。 したがって、ドメイン コントローラーでプロキシ アカウントを使用している場合は、プロファイル ディレクトリが確実に作成されているようにするため、少なくとも 1 回は使用されている対話型アカウントを指定する必要があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_syscollector_update_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @new_name = ] 'new_name' ]  
    , [ [ @target = ] 'target' ]  
    , [ [ @collection_mode = ] collection_mode ]  
    , [ [ @days_until_expiration = ] days_until_expiration ]  
    , [ [ @proxy_id = ] proxy_id ]  
    , [ [ @proxy_name = ] 'proxy_name' ]  
    ,[ [ @schedule_uid = ] 'schedule_uid' ]  
    ,[ [ @schedule_name = ] 'schedule_uid' ]  
    , [ [ @logging_level = ] logging_level ]  
    , [ [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @collection_set_id = ] collection_set_id` コレクションセットの一意なローカル識別子を設定します。 *collection_set_id* は **int** で、 *name* が NULL の場合は値が必要です。  
  
`[ @name = ] 'name'` コレクションセットの名前を指定します。 *名前* は **sysname** であり、 *collection_set_id* が NULL の場合は値を持つ必要があります。  
  
`[ @new_name = ] 'new_name'` コレクションセットの新しい名前を指定します。 *new_name* は **sysname**であり、使用する場合、空の文字列にすることはできません。 *new_name* は一意である必要があります。 現在のコレクション セットの名前の一覧については、syscollector_collection_sets システム ビューにクエリを実行します。  
  
`[ @target = ] 'target'` 将来使用するために予約されています。  
  
`[ @collection_mode = ] collection_mode` 使用するデータコレクションの種類を示します。 *collection_mode* は **smallint** であり、次のいずれかの値を持つことができます。  
  
 0-キャッシュモード。 データの収集とアップロードは別々のスケジュールに基づいています。 連続コレクションのキャッシュモードを指定します。  
  
 1-非キャッシュモード。 データの収集とアップロードは同じスケジュールに基づいて実行されます。 アドホック コレクションまたはスナップショット コレクションの非キャッシュ モードを指定します。  
  
 非キャッシュモードからキャッシュモード (0) に変更する場合は、 *schedule_uid* または *schedule_name*のいずれかも指定する必要があります。  
  
`[ @days_until_expiration = ] days_until_expiration` 収集したデータを管理データウェアハウスに保存する日数を指定します。 *days_until_expiration* は **smallint**です。 *days_until_expiration* は、0または正の整数である必要があります。  
  
`[ @proxy_id = ] proxy_id` エージェントプロキシアカウントの一意の識別子を示し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 *proxy_id* は **int**です。  
  
`[ @proxy_name = ] 'proxy_name'` プロキシの名前を指定します。 *proxy_name* は **sysname** で、null 値が許容されます。  
  
`[ @schedule_uid = ] 'schedule_uid'` は、スケジュールを指す GUID です。 *schedule_uid* は **uniqueidentifier**です。  
  
 *Schedule_uid*を取得するには、sysschedules システムテーブルに対してクエリを実行します。  
  
 *Collection_mode*が0に設定されている場合、 *schedule_uid*または*schedule_name*を指定する必要があります。 *Collection_mode*が1に設定されている場合、指定した場合、 *schedule_uid*または*schedule_name*は無視されます。  
  
`[ @schedule_name = ] 'schedule_name'` スケジュールの名前を指定します。 *schedule_name* は **sysname** で、null 値が許容されます。 指定する場合、 *schedule_uid* は NULL である必要があります。 *Schedule_name*を取得するには、sysschedules システムテーブルに対してクエリを実行します。  
  
`[ @logging_level = ] logging_level` はログ記録レベルです。 *logging_level* は、次のいずれかの **値を使用** します。  
  
 0: 実行情報と [!INCLUDE[ssIS](../../includes/ssis-md.md)] 追跡するイベントを記録します。  
  
-   コレクションセットの開始/停止  
  
-   パッケージの開始/停止  
  
-   エラー情報  
  
 1-レベル0のログ記録と:  
  
-   実行の統計  
  
-   継続的に実行されているコレクションの進行状況  
  
-   からの警告イベント [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 2-レベル1のログ記録と、からの詳細なイベント情報 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 。  
  
 *Logging_level*の既定値は1です。  
  
`[ @description = ] 'description'` コレクションセットの説明を設定します。 *説明* は **nvarchar (4000)** です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 sp_syscollector_update_collection_set は、msdb システム データベースのコンテキストで実行する必要があります。  
  
 *Collection_set_id*または*名前*には値を指定する必要があります。どちらも NULL にすることはできません。 これらの値を取得するには、syscollector_collection_sets システム ビューにクエリを実行します。  
  
 コレクションセットが実行されている場合は、 *schedule_uid* と *説明*のみを更新できます。 コレクションセットを停止するには、 [sp_syscollector_stop_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md)を使用します。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行するには、(EXECUTE 権限を持つ) dc_admin または dc_operator 固定データベース ロールのメンバーシップが必要です。 dc_operator ロールのメンバーがこのストアド プロシージャで更新できるのは、その権限で変更できるプロパティに限られます。 次のプロパティについては、dc_admin のみ変更できます。  
  
-   @new_name  
  
-   @target  
  
-   @proxy_id  
  
-   @description  
  
-   @collection_mode  
  
-   @days_until_expiration  
  
## <a name="examples"></a>例  
  
### <a name="a-renaming-a-collection-set"></a>A. コレクション セットの名前を変更する  
 次の例では、ユーザー定義のコレクションセットの名前を変更します。  
  
```  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_update_collection_set  
@name = N'Simple collection set test 1',  
@new_name = N'Collection set test 1 in cached mode';  
GO  
```  
  
### <a name="b-changing-the-collection-mode-from-non-cached-to-cached"></a>B. コレクション モードを非キャッシュからキャッシュに変更する  
 次の例では、コレクション モードを非キャッシュ モードからキャッシュ モードに変更します。 この変更を行うには、スケジュール ID またはスケジュール名を指定する必要があります。  
  
```  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_update_collection_set  
@name = N'Collection set test 1 in cached mode',  
@collection_mode = 0,  
@schedule_uid = 'C7022AF3-51B8-4011-B159-64C47C88FF70';  
-- alternatively, use @schedule_name.  
-- @schedule_name = N'CollectorSchedule_Every_15min;  
GO  
```  
  
### <a name="c-changing-other-collection-set-parameters"></a>C. その他のコレクションセットのパラメーターの変更  
 次の例では、"Simple collection set test 2" という名前のコレクションセットのさまざまなプロパティを更新します。  
  
```  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_update_collection_set  
@name = N'Simple collection set test 2',  
@collection_mode = 1,  
@days_until_expiration = 5,  
@description = N'This is a test collection set that runs in noncached mode.',  
@logging_level = 0;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [[データ コレクション]](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)   
 [dbo.sysのスケジュール &#40;Transact-sql&#41;](../../relational-databases/system-tables/dbo-sysschedules-transact-sql.md)  
  
  
