---
description: クエリ通知-sys.dm_qn_subscriptions
title: sys.dm_qn_subscriptions (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_qn_subscriptions
- dm_qn_subscriptions_TSQL
- sys.dm_qn_subscriptions
- sys.dm_qn_subscriptions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_qn_subscriptions dynamic management view
ms.assetid: a3040ce6-f5af-48fc-8835-c418912f830c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 197d3fd3ab4108c898c9377bbeed2f0e16e83d76
ms.sourcegitcommit: 32135463a8494d9ed1600a58f51819359e3c09dc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/08/2020
ms.locfileid: "91834477"
---
# <a name="query-notifications---sysdm_qn_subscriptions"></a>クエリ通知-sys.dm_qn_subscriptions
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバーのアクティブ クエリ通知サブスクリプションに関する情報を返します。 このビューは、サーバーまたは指定したデータベース内のアクティブなサブスクリプションを確認したり、指定したサーバー プリンシパルを確認する際に使用できます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|サブスクリプションの ID。|  
|**database_id**|**int**|通知クエリが実行されたデータベースの ID。 このデータベースには、このサブスクリプションに関連する情報が格納されます。|  
|**sid**|**varbinary(85)**|このサブスクリプションを作成して所有しているサーバー プリンシパルのセキュリティ ID。|  
|**object_id**|**int**|サブスクリプションパラメーターに関する情報を格納する内部テーブルの ID。|  
|**created**|**datetime**|サブスクリプションが作成された日付と時刻。|  
|**timeout**|**int**|サブスクリプションのタイムアウト (秒単位)。 この時間が経過すると、通知のフラグが設定されます。<br /><br /> 注: 実際の起動時間は、指定されたタイムアウトよりも長くなる場合があります。ただし、サブスクリプションを無効にする変更が、指定されたタイムアウトの後、サブスクリプションが開始される前に発生した場合、は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 変更が行われた時点で発生していることを確認します。|  
|**status**|**int**|サブスクリプションの状態を示します。 コードの一覧については、「解説」の表を参照してください。|  
  
## <a name="relationship-cardinalities"></a>リレーションシップ基数  
  
|ソース|宛先|オン|Type|  
|----------|--------|--------|----------|  
|**sys.dm_qn_subscriptions**|**sys.databases**|**database_id**|多対一|  
|**sys.dm_qn_subscriptions**|**sys.internal_tables**|**object_id**|多対一|  
  
## <a name="remarks"></a>注釈  
 状態コードが 0 の場合は、未定義の状態であることを示します。  
  
 次のステータスコードは、変更のためにサブスクリプションが発生したことを示しています。  
  
|コード|マイナーステータス|［情報］|  
|----------|------------------|----------|  
|65798|データが変更されたため、サブスクリプションが起動しました|挿入によってトリガーされたサブスクリプション|  
|65799|データが変更されたため、サブスクリプションが起動しました|削除|  
|65800|データが変更されたため、サブスクリプションが起動しました|更新|  
|65801|データが変更されたため、サブスクリプションが起動しました|Merge|  
|65802|データが変更されたため、サブスクリプションが起動しました|テーブルを切り捨てる|  
|66048|タイムアウトが発生したため、サブスクリプションが起動しました|未定義の情報モード|  
|66315|オブジェクトが変更されたため、サブスクリプションが起動しました|オブジェクトまたはユーザーが削除されました|  
|66316|オブジェクトが変更されたため、サブスクリプションが起動しました|オブジェクトが変更されました|  
|66565|データベースがデタッチまたは削除されたため、サブスクリプションが起動しました|サーバーまたはデータベースが再起動されました|  
|66571|データベースがデタッチまたは削除されたため、サブスクリプションが起動しました|オブジェクトまたはユーザーが削除されました|  
|66572|データベースがデタッチまたは削除されたため、サブスクリプションが起動しました|オブジェクトが変更されました|  
|67341|サーバーのリソースが不足しているため、サブスクリプションがトリガーされました|サーバーのリソースが不足しているため、サブスクリプションがトリガーされました|  
  
 次のステータスコードは、サブスクリプションを作成できなかったことを示しています。  
  
|コード|マイナーステータス|［情報］|  
|----------|------------------|----------|  
|132609|ステートメントがサポートされていないため、サブスクリプションを作成できませんでした|クエリが複雑すぎます|  
|132610|ステートメントがサポートされていないため、サブスクリプションを作成できませんでした|サブスクリプションの無効なステートメント|  
|132611|ステートメントがサポートされていないため、サブスクリプションを作成できませんでした|サブスクリプションの設定オプションが無効です|  
|132612|ステートメントがサポートされていないため、サブスクリプションを作成できませんでした|分離レベルが無効です|  
|132622|ステートメントがサポートされていないため、サブスクリプションを作成できませんでした|内部的に使用|  
|132623|ステートメントがサポートされていないため、サブスクリプションを作成できませんでした|テーブルあたりのテンプレートの制限を超える|  
  
 次の状態コードは内部で使用され、check kill モードおよび init モードとして分類されます。  
  
|コード|マイナーステータス|［情報］|  
|----------|------------------|----------|  
|198656|内部使用: check kill モードおよび init モード|未定義の情報モード|  
|198928|サブスクリプションが破棄されました|Db がアタッチされたため、サブスクリプションが起動しました|  
|198929|サブスクリプションが破棄されました|ユーザーが削除されたため、サブスクリプションが起動しました|  
|198930|サブスクリプションが破棄されました|サブスクリプションが削除されたため、サブスクリプションが削除されました|  
|198931|サブスクリプションが破棄されました|サブスクリプションが強制終了されました|  
|199168|サブスクリプションがアクティブです|未定義の情報モード|  
|199424|サブスクリプションが初期化されていますが、まだアクティブではありません|未定義の情報モード|  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
> [!NOTE]  
>  ユーザーが VIEW SERVER STATE 権限を持っていない場合、このビューは、現在のユーザーが所有するサブスクリプションに関する情報を返します。  
  
## <a name="examples"></a>例  
  
### <a name="a-return-active-query-notification-subscriptions-for-the-current-user"></a>A. 現在のユーザーのアクティブなクエリ通知サブスクリプションを返す  
 次の例では、現在のユーザーのアクティブなクエリ通知サブスクリプションを返します。 ユーザーが VIEW SERVER STATE 権限を所有している場合は、サーバー内のアクティブなサブスクリプションがすべて返されます。  
  
```  
SELECT id, database_id, sid, object_id, created, timeout, status  
FROM sys.dm_qn_subscriptions;  
GO  
```  
  
### <a name="b-returning-active-query-notification-subscriptions-for-a-specified-user"></a>B. 指定されたユーザーのアクティブなクエリ通知サブスクリプションを返す  
 次の例では、ログイン `Ruth0` によってサブスクライブされたアクティブなクエリ通知サブスクリプションを返します。  
  
```  
SELECT id, database_id, sid, object_id, created, timeout, status  
FROM sys.dm_qn_subscriptions  
WHERE sid = SUSER_SID('Ruth0');  
GO  
```  
  
### <a name="c-returning-internal-table-metadata-for-query-notification-subscriptions"></a>C. クエリ通知サブスクリプションの内部テーブルメタデータを返す  
 次の例では、クエリ通知サブスクリプションに関する内部テーブルのメタデータを返します。  
  
```  
SELECT qn.id AS query_subscription_id  
    ,it.name AS internal_table_name  
    ,it.object_id AS internal_table_id  
FROM sys.internal_tables AS it  
JOIN sys.dm_qn_subscriptions AS qn ON it.object_id = qn.object_id  
WHERE it.internal_type_desc = 'QUERY_NOTIFICATION';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [動的管理ビューと動的管理関数 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [クエリ通知関連の動的管理ビュー &#40;Transact-sql&#41;](./system-dynamic-management-views.md)   
 [KILL QUERY NOTIFICATION SUBSCRIPTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-query-notification-subscription-transact-sql.md)  
  
