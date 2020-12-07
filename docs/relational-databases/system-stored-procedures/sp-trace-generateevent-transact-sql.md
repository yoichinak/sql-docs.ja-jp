---
description: sp_trace_generateevent (Transact-sql)
title: sp_trace_generateevent (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_generateevent_TSQL
- sp_trace_generateevent
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_generateevent
ms.assetid: 3ef05bfb-b467-4403-89cc-6e77ef9247dd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d8a5e027b2d76aa1e6965f1fe782b8987a927ce3
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541589"
---
# <a name="sp_trace_generateevent-transact-sql"></a>sp_trace_generateevent (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  でユーザー定義イベントを作成し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
>**注:**  このストアドプロシージャは **非推奨とされます** 。 他のすべてのトレース関連のストアド プロシージャの使用は非推奨とされます。  
  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_trace_generateevent [ @eventid = ] event_id   
     [ , [ @userinfo = ] 'user_info' ]  
     [ , [ @userdata = ] user_data ]  
```  
  
## <a name="arguments"></a>引数  
`[ @eventid = ] event_id` 有効にするイベントの ID を設定します。 *event_id* は **int**,、既定値はありません。 ID は、82 ~ 91 のイベント番号のいずれかである必要があります。これは、 [sp_trace_setevent](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)で設定されたユーザー定義イベントを表します。  
  
`[ @userinfo = ] 'user_info'` イベントの理由を示す、オプションのユーザー定義文字列を指定します。 *user_info* は **nvarchar (128)**,、既定値は NULL です。  
  
`[ @userdata = ] user_data` は、イベントに対してユーザーが指定したオプションのデータです。 *user_data* は **varbinary (8000)**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 次の表は、このストアド プロシージャの完了時に返されるコード値を示しています。  
  
|リターン コード|説明|  
|-----------------|-----------------|  
|**0**|エラーなし。|  
|**1**|不明なエラー。|  
|**3**|指定されたイベントは無効です。 イベントが存在しないか、またはストアドプロシージャに対して適切ではありません。|  
|**13**|メモリが不足しています。 指定されたアクションを実行するのに十分なメモリがない場合に返されます。|  
  
## <a name="remarks"></a>解説  
 **sp_trace_generateevent**は、 **xp_trace_ \* **の拡張ストアドプロシージャによって以前に実行された多くの操作を実行します。 **Xp_trace_generate_event**ではなく**sp_trace_generateevent**を使用します。  
  
 **Sp_trace_generateevent**では、ユーザー定義イベントの ID 番号のみを使用できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で他のイベント ID 番号を使用すると、エラーが発生します。  
  
 すべての SQL トレースストアドプロシージャ (**sp_trace_xx**) のパラメーターは厳密に型指定されます。 これらのパラメーターを、引数の説明で指定されている正しいデータ型で指定しないと、このストアド プロシージャではエラーが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは ALTER TRACE 権限を持っている必要があります。  
  
## <a name="examples"></a>例  
 次の例では、サンプルテーブルにユーザーが構成可能なイベントを作成します。  
  
```  
--Create a sample table.  
CREATE TABLE user_config_test(col1 int, col2 char(10));  
  
--DROP the trigger if it already exists.  
IF EXISTS  
   (SELECT * FROM sysobjects WHERE name = 'userconfig_trg')  
   DROP TRIGGER userconfig_trg;  
  
--Create an ON INSERT trigger on the sample table.  
CREATE TRIGGER userconfig_trg  
   ON user_config_test FOR INSERT;  
AS  
EXEC master..sp_trace_generateevent  
   @event_class = 82, @userinfo = N'Inserted row into user_config_test';  
  
--When an insert action happens, the user-configurable event fires. If   
you were capturing the event id=82, you will see it in the Profiler output.  
INSERT INTO user_config_test VALUES(1, 'abc');  
```  
  
## <a name="see-also"></a>関連項目  
 [fn_trace_geteventinfo &#40;Transact-sql&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [SQL トレース (SQL Trace)](../../relational-databases/sql-trace/sql-trace.md)  
  
  
