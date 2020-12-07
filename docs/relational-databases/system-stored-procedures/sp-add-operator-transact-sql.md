---
description: sp_add_operator (Transact-SQL)
title: sp_add_operator (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_operator
- sp_add_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_operator
ms.assetid: 817cd98a-4dff-4ed8-a546-f336c144d1e0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e2b67e5754fdc0124d105d99954361535933c88b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539241"
---
# <a name="sp_add_operator-transact-sql"></a>sp_add_operator (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  警告およびジョブで使用するオペレーター (通知受信者) を作成します。  
  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_add_operator [ @name = ] 'name'   
     [ , [ @enabled = ] enabled ]   
     [ , [ @email_address = ] 'email_address' ]   
     [ , [ @pager_address = ] 'pager_address' ]   
     [ , [ @weekday_pager_start_time = ] weekday_pager_start_time ]   
     [ , [ @weekday_pager_end_time = ] weekday_pager_end_time ]   
     [ , [ @saturday_pager_start_time = ] saturday_pager_start_time ]   
     [ , [ @saturday_pager_end_time = ] saturday_pager_end_time ]   
     [ , [ @sunday_pager_start_time = ] sunday_pager_start_time ]   
     [ , [ @sunday_pager_end_time = ] sunday_pager_end_time ]   
     [ , [ @pager_days = ] pager_days ]   
     [ , [ @netsend_address = ] 'netsend_address' ]   
     [ , [ @category_name = ] 'category' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @name = ] 'name'` オペレーター (通知受信者) の名前。 この名前は一意である必要があり、パーセント () 文字を含めることはできません **%** 。 *名前* は **sysname**,、既定値はありません。  
  
`[ @enabled = ] enabled` オペレーターの現在の状態を示します。 *有効* になっているは **tinyint**,、既定値は **1** (有効) です。 **0**の場合、オペレーターは無効になり、通知を受信しません。  
  
`[ @email_address = ] 'email_address'` オペレーターの電子メールアドレス。 この文字列はメール システムに直接渡されます。 *email_address* は **nvarchar (100)**,、既定値は NULL です。  
  
 *Email_address*には、物理電子メールアドレスまたはエイリアスを指定できます。 次に例を示します。  
  
 '**jdoe**' または '**jdoe \@ xyz.com**'  
  
> [!NOTE]  
>  データベース メールには電子メール アドレスを使用する必要があります。  
  
`[ @pager_address = ] 'pager_address'` オペレーターのポケットベルアドレス。 この文字列はメール システムに直接渡されます。 *pager_address* は **nvarchar (100)**,、既定値は NULL です。  
  
`[ @weekday_pager_start_time = ] weekday_pager_start_time`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]月曜日から金曜日までの平日に、指定したオペレーターにエージェントがポケットベルによる通知を送信するまでの時間。 *weekday_pager_start_time*は **int**,、既定値は **090000**,、9:00 A.M. を示す を 24 時間形式で表したものです。HHMMSS 形式で入力する必要があります。  
  
`[ @weekday_pager_end_time = ] weekday_pager_end_time` 月曜日から金曜日までの平日に、 **SQLServerAgent** サービスが、指定されたオペレーターにポケットベルによる通知を送信しなくなる時刻。 *weekday_pager_end_time*は **int**,、既定値は 18万,、6:00 pm を示す を 24 時間形式で表したものです。HHMMSS 形式で入力する必要があります。  
  
`[ @saturday_pager_start_time = ] saturday_pager_start_time` 土曜日に、 **SQLServerAgent** サービスが、指定されたオペレーターにポケットベルによる通知を送信するまでの時間。 *saturday_pager_start_time* は **int**,、既定値は 090000,、9:00 A.M. を示す を 24 時間形式で表したものです。HHMMSS 形式で入力する必要があります。  
  
`[ @saturday_pager_end_time = ] saturday_pager_end_time` 土曜日に、 **SQLServerAgent** サービスが、指定されたオペレーターにポケットベルによる通知を送信しなくなる時刻。 *saturday_pager_end_time*は **int**,、既定値は **18万**,、6:00 pm を示す を 24 時間形式で表したものです。HHMMSS 形式で入力する必要があります。  
  
`[ @sunday_pager_start_time = ] sunday_pager_start_time` 日曜日に、 **SQLServerAgent** サービスが、指定されたオペレーターにポケットベルによる通知を送信するまでの時間。 *sunday_pager_start_time*は **int**,、既定値は **090000**,、9:00 A.M. を示す を 24 時間形式で表したものです。HHMMSS 形式で入力する必要があります。  
  
`[ @sunday_pager_end_time = ] sunday_pager_end_time` 日曜日に、 **SQLServerAgent** サービスが、指定されたオペレーターにポケットベルによる通知を送信しなくなる時刻。 *sunday_pager_end_time*は **int**,、既定値は **18万**,、6:00 pm を示す を 24 時間形式で表したものです。HHMMSS 形式で入力する必要があります。  
  
`[ @pager_days = ] pager_days` ページで演算子が使用できる曜日を示す数値です (指定された開始/終了時刻に従います)。 *pager_days*は **tinyint**,、既定値は **0** の場合、操作がページを受信できないことを示します。 有効な値は **0** ~ **127**です。 *pager_days*は、必要な日数の個々の値を加算することによって計算されます。 たとえば、月曜日から金曜日の場合は、 **2** + **4** + **8** + **16** + **32**  =  **62**になります。 次の表は、各曜日の値を示しています。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|土曜日|  
|**2**|月曜日|  
|**4**|Tuesday|  
|**8**|水曜日|  
|**16**|Thursday|  
|**32**|金曜日|  
|**64**|土曜日|  
  
`[ @netsend_address = ] 'netsend_address'` ネットワークメッセージの送信先オペレーターのネットワークアドレス。 *netsend_address*は **nvarchar (100)**,、既定値は NULL です。  
  
`[ @category_name = ] 'category'` この演算子のカテゴリの名前。 *category* は **sysname**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 **sp_add_operator** は、 **msdb** データベースから実行する必要があります。  
  
 ページングは電子メールシステムでサポートされています。ページングを使用する場合は、電子メールとポケットベルの機能が必要です。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] は、ジョブを簡単に管理できるグラフィカルなツールです。ジョブのインフラストラクチャを作成し、管理するには、このツールを使用することをお勧めします。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_add_operator**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 次の例では、`danwi` に対してオペレーター情報を設定します。 オペレーターは有効になっています。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントは、月曜日から金曜日の午前 8 時から午後 5 時まで、 ポケットベルによる通知を送信します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_operator  
    @name = N'Dan Wilson',  
    @enabled = 1,  
    @email_address = N'danwi',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 62 ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_delete_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_update_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
