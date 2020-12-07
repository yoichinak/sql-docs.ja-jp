---
description: core.sp_purge_data (Transact-SQL)
title: sp_purge_data (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_purge_data_TSQL
- sp_purge_data
dev_langs:
- TSQL
helpviewer_keywords:
- sp_purge_data
- management data warehouse, data collector stored procedures
- core.sp_purge_data stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 056076c3-8adf-4f51-8a1b-ca39696ac390
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ff33927812ccab2f2665e80709bcf6074ebacc1a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89530401"
---
# <a name="coresp_purge_data-transact-sql"></a>core.sp_purge_data (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  保有ポリシーに基づいて、管理データ ウェアハウスからデータを削除します。 このプロシージャは、指定されたインスタンスに関連付けられている管理データ ウェアハウスに対して、mdw_purge_data [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブによって毎日実行されます。 このストアドプロシージャを使用すると、管理データウェアハウスからデータをオンデマンドで削除できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
core.sp_purge_data  
    [ [ @retention_days = ] retention_days ]  
    [ , [ @instance_name = ] 'instance_name' ]  
    [ , [ @collection_set_uid = ] 'collection_set_uid' ]  
    [ , [ @duration = ] duration ]  
```  
  
## <a name="arguments"></a>引数  
 [ @retention_days =] *retention_days*  
 管理データウェアハウスのテーブルにデータを保持する日数を指定します。 *Retention_days*よりも古いタイムスタンプを持つデータは削除されます。 *retention_days* は **smallint**,、既定値は NULL です。 指定する場合、値は正の値である必要があります。 NULL の場合は、core.snapshots ビューの valid_through 列の値によって、削除対象の行が判断されます。  
  
 [ @instance_name =] '*instance_name*'  
 コレクションセットのインスタンスの名前です。 *instance_name* は **sysname**,、既定値は NULL です。  
  
 *instance_name*には、コンピューター名と、 *computername*instancename という形式のインスタンス名で構成される完全修飾インスタンス名を指定する必要があり \\ *instancename*ます。 NULL の場合は、ローカルサーバー上の既定のインスタンスが使用されます。  
  
 [ @collection_set_uid =] '*collection_set_uid*'  
 コレクション セットの GUID を指定します。 *collection_set_uid* は **uniqueidentifier**,、既定値は NULL です。 NULL の場合、すべてのコレクションセットからの条件を満たす行が削除されます。 この値を取得するには、syscollector_collection_sets カタログ ビューに対してクエリを実行します。  
  
 [ @duration =] *期間*  
 消去操作を実行する最大時間 (分) です。 *duration* は **smallint**,、既定値は NULL です。 指定する場合、値はゼロまたは正の整数にする必要があります。 NULL の場合は、条件を満たすすべての行が削除されるか操作が手動で停止されるまで、操作は実行されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 このプロシージャでは、保有期間に基づいて削除対象となる core.snapshots ビューの行が選択されます。 削除の対象となるすべての行が、snapshots_internal テーブルから削除されます。 前の行を削除すると、すべての管理データウェアハウステーブルで連鎖削除操作がトリガーされます。 これは、収集されたデータを格納するすべてのテーブルに対して定義されている ON DELETE CASCADE 句を使って実行されます。  
  
 各スナップショットとその関連データは、明示的なトランザクションで削除されてからコミットされます。 そのため、パージ操作が手動で停止された場合、またはに指定された値を超えた場合は、コミットされて @duration いないデータのみが残ります。 このデータは、ジョブの次回の実行時に削除できます。  
  
 プロシージャは、管理データウェアハウスデータベースのコンテキストで実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 **Mdw_admin** (EXECUTE 権限を持つ) 固定データベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-running-sp_purge_data-with-no-parameters"></a>A. パラメーターを使用せずに sp_purge_data を実行する  
 次の例では、パラメーターを指定せずに core.sp_purge_data を実行します。 そのため、すべてのパラメーターに既定値の NULL が使用され、それに関連付けられている動作が実行されます。  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data;  
GO  
```  
  
### <a name="b-specifying-retention-and-duration-values"></a>B. 保有期間と実行時間の値を指定する  
 次の例では、7日よりも前の管理データウェアハウスからデータを削除します。 また、パラメーターを指定して、 @duration 操作が5分以内に実行されるようにします。  
  
```  
USE <management_data_warehouse>;  
EXECUTE core.sp_purge_data @retention_days = 7, @duration = 5;  
GO  
```  
  
### <a name="c-specifying-an-instance-name-and-collection-set"></a>C. インスタンス名とコレクションセットの指定  
 次の例では、指定されたインスタンスの特定のコレクションセットの管理データウェアハウスからデータを削除し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 @retention_daysが指定されていないので、valid_through 列の値は、削除の対象となるコレクションセットの行を決定するために使用されます。  
  
```  
USE <management_data_warehouse>;  
GO  
-- Get the collection set unique identifier for the Disk Usage system collection set.  
DECLARE @disk_usage_collection_set_uid uniqueidentifier = (SELECT collection_set_uid   
    FROM msdb.dbo.syscollector_collection_sets WHERE name = N'Disk Usage');   
  
EXECUTE core.sp_purge_data @instance_name = @@SERVERNAME, @collection_set_uid = @disk_usage_collection_set_uid;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
