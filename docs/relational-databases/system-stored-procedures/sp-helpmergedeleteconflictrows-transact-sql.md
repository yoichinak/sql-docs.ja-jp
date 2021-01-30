---
description: sp_helpmergedeleteconflictrows (Transact-SQL)
title: sp_helpmergedeleteconflictrows (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
f1_keywords:
- sp_helpmergedeleteconflictrows
- sp_helpmergedeleteconflictrows_TSQL
helpviewer_keywords:
- sp_helpmergedeleteconflictrows
ms.assetid: 222be651-5690-4341-9dfb-f9ec1d80c970
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 07ca90c1eb7792ea5d197fe37a3542f526f870b6
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99179244"
---
# <a name="sp_helpmergedeleteconflictrows-transact-sql"></a>sp_helpmergedeleteconflictrows (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  削除の競合が失われたデータ行に関する情報を返します。 このストアドプロシージャは、分散競合ログが使用されている場合に、パブリッシャー側のパブリケーションデータベースまたはサブスクライバー側でサブスクリプションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpmergedeleteconflictrows [ [ @publication = ] 'publication']  
    [ , [ @source_object = ] 'source_object']  
    [ , [ @publisher = ] 'publisher'  
    [ , [ @publisher_db = ] 'publsher_db'  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* の **sysname**,、既定値は **%** です。 パブリケーションが指定されている場合は、パブリケーションによって修飾されたすべての競合が返されます。  
  
`[ @source_object = ] 'source_object'` ソースオブジェクトの名前を指定します。 *source_object* は **nvarchar (386)**,、既定値は NULL です。  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。*publisher* は **sysname** で、既定値は NULL です。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャーデータベースの名前を指定します。*publisher_db* は **sysname**,、既定値は NULL です。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**source_object**|**nvarchar (386)**|削除競合のソースオブジェクト。|  
|**rowguid**|**uniqueidentifier**|削除競合の行識別子。|  
|**conflict_type**|**int**|競合の種類を示すコード:<br /><br /> **1** = UpdateConflict: 行レベルで競合が検出されました。<br /><br /> **2** = ColumnUpdateConflict: 列レベルで競合が検出されました。<br /><br /> **3** = UpdateDeleteWinsConflict: Delete は競合を優先します。<br /><br /> **4** = UpdateWinsDeleteConflict: 競合が失われた削除済みの rowguid がこのテーブルに記録されます。<br /><br /> **5** = uploadinsertfailed: サブスクライバーからの挿入をパブリッシャーで適用できませんでした。<br /><br /> **6** = downloadinsertfailed: パブリッシャーからの挿入をサブスクライバーで適用できませんでした。<br /><br /> **7** = uploaddeletefailed: サブスクライバーでの削除をパブリッシャーにアップロードできませんでした。<br /><br /> **8** = downloaddeletefailed: パブリッシャーでの削除をサブスクライバーにダウンロードできませんでした。<br /><br /> **9** = uploadupdatefailed: サブスクライバーでの更新をパブリッシャーで適用できませんでした。<br /><br /> **10** = downloadupdatefailed: パブリッシャーでの更新をサブスクライバーに適用できませんでした。|  
|**reason_code**|**Int**|状況に依存する可能性があるエラーコード。|  
|**reason_text**|**varchar (720)**|状況依存のエラーの説明。|  
|**origin_datasource**|**varchar(255)**|競合の発生元。|  
|**pubid**|**uniqueidentifier**|パブリケーション識別子。|  
|**MSrepl_create_time**|**datetime**|競合情報が追加された時刻。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>コメント  
 **sp_helpmergedeleteconflictrows** は、マージレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helpmergedeleteconflictrows** を実行できるのは、 **sysadmin** 固定サーバーロールおよび **db_owner** 固定データベースロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
