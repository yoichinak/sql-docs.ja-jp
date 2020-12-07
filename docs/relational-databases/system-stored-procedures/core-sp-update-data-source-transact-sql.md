---
description: sp_update_data_source (Transact-sql)
title: sp_update_data_source (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_data_source
- sp_update_data_source_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_data_source
- management data warehouse, data collector stored procedures
- core.sp_update_data_source stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 66b95f96-6df7-4657-9b3c-86a58c788ca5
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2ad50aaa81cb61b6ead9388e41e025993e54c364
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550105"
---
# <a name="coresp_update_data_source-transact-sql"></a>sp_update_data_source (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  管理データ ウェアハウスの core.source_info_internal テーブルで既存行の更新または新規行の挿入を行います。 このプロシージャは、アップロードパッケージが管理データウェアハウスへのデータのアップロードを開始するたびに、データコレクターの実行時コンポーネントによって呼び出されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
core.sp_update_data_source [ @collection_set_uid = ] 'collection_set_uid'  
    ,[ @machine_name = ] 'machine_name'  
    , [ @named_instance = ] 'named_instance'  
    , [ @days_until_expiration = ] days_until_expiration  
    , [ @source_id = ] source_id OUTPUT  
```  
  
## <a name="arguments"></a>引数  
 [ @collection_set_uid =] '*collection_set_uid*'  
 コレクション セットの GUID を指定します。 *collection_set_uid* は **uniqueidentifier**,、既定値はありません。 GUID を取得するには、msdb データベースの dbo.syscollector_collection_sets ビューにクエリを実行します。  
  
 [ @machine_name =] '*machine_name*'  
 コレクション セットが存在するサーバーの名前を指定します。 *machine_name* は **sysname** で、既定値はありません。  
  
 [ @named_instance =] '*named_instance*'  
 コレクションセットのインスタンスの名前です。 *named_instance* は **sysname**であり、既定値はありません。  
  
> [!NOTE]  
>  *named_instance*には、コンピューター名と、 *computername*instancename という形式のインスタンス名で構成される完全修飾インスタンス名を指定する必要があり \\ *instancename*ます。  
  
 [ @days_until_expiration =] *days_until_expiration*  
 スナップショット データ保持期間の日数を指定します。 *days_until_expiration* は **smallint**です。  
  
 [ @source_id =] *source_id*  
 更新元の一意の識別子。 *source_id* は **INT** で、出力として返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 アップロード パッケージが管理データ ウェアハウスへのデータのアップロードを開始するたびに、データ コレクターの実行時コンポーネントが core.sp_update_data_source を呼び出します。 前回のアップロード時以降に次のいずれかの変更が行われている場合は、core.source_info_internal テーブルが更新されます。  
  
-   新しいコレクションセットが追加されました。  
  
-   days_until_expiration の値が変更された。  
  
## <a name="permissions"></a>アクセス許可  
 **Mdw_writer** (EXECUTE 権限を持つ) 固定データベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、データソース (この場合はディスク使用量コレクションセット) を更新し、有効期限までの日数を設定して、ソースの識別子を返します。 この例では、既定のインスタンスが使用されています。  
  
```  
USE <management_data_warehouse>;  
GO  
DECLARE @source_id int;  
EXEC core.sp_update_data_source   
@collection_set_uid = '7B191952-8ECF-4E12-AEB2-EF646EF79FEF',   
@machine_name = '<computername>',  
@named_instance = 'MSSQLSERVER',  
@days_until_expiration = 10,  
@source_id = @source_id OUTPUT;  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [データ コレクター ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [管理データ ウェアハウス](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
