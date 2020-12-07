---
description: sp_helpmergeconflictrows (Transact-SQL)
title: sp_helpmergeconflictrows (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergeconflictrows_TSQL
- sp_helpmergeconflictrows
helpviewer_keywords:
- sp_helpmergeconflictrows
ms.assetid: 131395a5-cb18-4795-a7ae-fa09d8ff347f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d6d8ea39fd9ccc48f96c838367d5f859226098d1
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809838"
---
# <a name="sp_helpmergeconflictrows-transact-sql"></a>sp_helpmergeconflictrows (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定された競合テーブルの行を返します。 このストアドプロシージャは、競合テーブルが格納されているコンピューター上で実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpmergeconflictrows [ [ @publication = ] 'publication' ]  
        , [ @conflict_table = ] 'conflict_table'  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @publisher_db = ] 'publsher_db' ]   
    [ , [ @logical_record_conflicts = ] logical_record_conflicts ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前を指定します。 *publication* の **sysname**,、既定値は **%** です。 パブリケーションが指定されている場合は、パブリケーションによって修飾されたすべての競合が返されます。 たとえば、 **MSmerge_conflict_Customers** テーブルに **WA** および **ca** パブリケーションの競合行がある場合、パブリケーション名 **ca** を渡すと、 **ca** パブリケーションに関連する競合が取得されます。  
  
`[ @conflict_table = ] 'conflict_table'` 競合テーブルの名前を指定します。 *conflict_table* は **sysname**であり、既定値はありません。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンでは、競合テーブルの名前は、パブリッシュされたアーティクルごとに1つのテーブルと共に、 **MSmerge_conflict \_ _パブリケーション \_ アーティクル_** での形式名を使用して付けられます。  
  
`[ @publisher = ] 'publisher'` パブリッシャーの名前を指定します。 *publisher* は **sysname**で、既定値は NULL です。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシャーデータベースの名前を指定します。*publisher_db* は **sysname**,、既定値は NULL です。  
  
`[ @logical_record_conflicts = ] logical_record_conflicts` 結果セットに論理レコードの競合に関する情報が含まれているかどうかを示します。 *logical_record_conflicts* は **int**,、既定値は0です。 **1** は、論理レコードの競合情報が返されることを意味します。  
  
## <a name="result-sets"></a>結果セット  
 **sp_helpmergeconflictrows** は、ベーステーブル構造とこれらの追加列で構成される結果セットを返します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**origin_datasource**|**varchar(255)**|競合の発生元。|  
|**conflict_type**|**int**|競合のタイプを示すコード。<br /><br /> **1** = 更新の競合: 行レベルで競合が検出されます。<br /><br /> **2** = 列更新の競合: 列レベルで競合が検出されました。<br /><br /> **3** = 更新の削除 Wins の競合: 削除によって競合が優先されます。<br /><br /> **4** = 更新 Wins 削除の競合: 競合が失われた削除済みの rowguid がこのテーブルに記録されます。<br /><br /> **5** = 挿入のアップロードに失敗しました: サブスクライバーからの挿入をパブリッシャーで適用できませんでした。<br /><br /> **6** = ダウンロードの挿入に失敗しました: パブリッシャーからの挿入をサブスクライバーで適用できませんでした。<br /><br /> **7** = 削除のアップロードに失敗しました: サブスクライバーでの削除をパブリッシャーにアップロードできませんでした。<br /><br /> **8** = 削除のダウンロードに失敗: パブリッシャーでの削除をサブスクライバーにダウンロードできませんでした。<br /><br /> **9** = 更新のアップロードに失敗しました: サブスクライバーでの更新をパブリッシャーで適用できませんでした。<br /><br /> **10** = 更新のダウンロードに失敗しました: パブリッシャーでの更新をサブスクライバーに適用できませんでした。<br /><br /> **12** = 論理レコードの更新による Wins の削除: 競合が失われた削除された論理レコードがこのテーブルに記録されます。<br /><br /> **13** = 論理レコードの競合の挿入更新: 論理レコードへの挿入が更新と競合しています。<br /><br /> **14** = 論理レコードの削除 Wins 更新の競合: 競合が失われる更新された論理レコードがこのテーブルに記録されます。|  
|**reason_code**|**int**|状況に依存する可能性があるエラーコード。|  
|**reason_text**|**varchar (720)**|状況依存のエラーの説明。|  
|**pubid**|**uniqueidentifier**|パブリケーション識別子。|  
|**MSrepl_create_time**|**datetime**|競合情報が追加された時刻。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>注釈  
 **sp_helpmergeconflictrows** は、マージレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helpmergeconflictrows**を実行できるのは、固定サーバーロール**sysadmin** 、 **db_owner**固定データベースロールのメンバー、およびディストリビューションデータベースの**replmonitor**ロールのメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [マージパブリケーションの競合情報を表示 &#40;レプリケーション Transact-sql プログラミング&#41;](../replication/view-and-resolve-data-conflicts-for-merge-publications.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
