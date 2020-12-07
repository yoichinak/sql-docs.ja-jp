---
description: sp_update_operator (Transact-SQL)
title: sp_update_operator (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_operator_TSQL
- sp_update_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_operator
ms.assetid: 231750a6-4828-4d03-afe6-b91d38c42ed3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4dbc3c382ecd1c58e9bd76624700a1c62804a82c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545906"
---
# <a name="sp_update_operator-transact-sql"></a>sp_update_operator (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  アラートおよびジョブで使用するオペレーター (通知受信者) に関する情報を更新します。  
  
   ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_update_operator   
     [ @name =] 'name'   
     [ , [ @new_name = ] 'new_name' ]   
     [ , [ @enabled = ] enabled]   
     [ , [ @email_address = ] 'email_address' ]  
     [ , [ @pager_address = ] 'pager_number']   
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
 [ @name =] '*name*'  
 変更するオペレーターの名前を指定します。 *名前* は **sysname**,、既定値はありません。  
  
 [ @new_name =] '*new_name*'  
 オペレーターの新しい名前です。 この名前は一意である必要があります。 *new_name* は **sysname**,、既定値は NULL です。  
  
 [ @enabled =] *有効*  
 オペレーターの現在の状態を示す数値 (現在有効になっている場合は**1** 、それ以外の場合は **0** )。 *有効* になっているは **tinyint**,、既定値は NULL です。 有効でない場合、オペレーターは警告通知を受信しません。  
  
 [ @email_address =] '*email_address*'  
 オペレーターの電子メールアドレス。 この文字列はメール システムに直接渡されます。 *email_address* は **nvarchar (100)**,、既定値は NULL です。  
  
 [ @pager_address =] '*pager_number*'  
 オペレーターのポケットベルアドレス。 この文字列はメール システムに直接渡されます。 *pager_number* は **nvarchar (100)**,、既定値は NULL です。  
  
 [ @weekday_pager_start_time =] *weekday_pager_start_time*  
 月曜日から金曜日までの間に、ポケットベルによる通知がこのオペレーターに送信されるまでの時間を指定します。 *weekday_pager_start_time*は **int**,、既定値は NULL の場合、24時間制で使用するために HHMMSS 形式で入力する必要があります。  
  
 [ @weekday_pager_end_time =] *weekday_pager_end_time*  
 月曜日から金曜日までの間で、指定したオペレーターに対してポケットベル通知を終了する時間を指定します。 *weekday_pager_end_time*は **int**,、既定値は NULL の場合、24時間制で使用するために HHMMSS 形式で入力する必要があります。  
  
 [ @saturday_pager_start_time =] *saturday_pager_start_time*  
 土曜日に、指定したオペレーターにポケットベルによる通知が送信されるまでの時間を指定します。 *saturday_pager_start_time*は **int**,、既定値は NULL の場合、24時間制で使用するために HHMMSS 形式で入力する必要があります。  
  
 [ @saturday_pager_end_time =] *saturday_pager_end_time*  
 土曜日に、指定したオペレーターにポケットベルによる通知を送信できない時間を指定します。 *saturday_pager_end_time*は **int**,、既定値は NULL の場合、24時間制で使用するために HHMMSS 形式で入力する必要があります。  
  
 [ @sunday_pager_start_time =] *sunday_pager_start_time*  
 日曜日に、指定したオペレーターにポケットベルによる通知が送信されるまでの時間を指定します。 *sunday_pager_start_time*は **int**,、既定値は NULL の場合、24時間制で使用するために HHMMSS 形式で入力する必要があります。  
  
 [ @sunday_pager_end_time =] *sunday_pager_end_time*  
 毎週日曜日に、指定したオペレーターに対してポケットベル通知を終了する時間を指定します。 *sunday_pager_end_time*は **int**,、既定値は NULL の場合、24時間制で使用するために HHMMSS 形式で入力する必要があります。  
  
 [ @pager_days =] *pager_days*  
 オペレーターがページの受信に使用できる曜日を指定します (指定した開始/終了時刻に従います)。 *pager_days*は **tinyint**,、既定値は NULL の場合、 **0** ~ **127**の値である必要があります。 *pager_days* は、必要な日数の個々の値を加算することによって計算されます。 たとえば、月曜日から金曜日の場合は、 **2** + **4** + **8** + **16** + **32**  =  **64**になります。  
  
|[値]|説明|  
|-----------|-----------------|  
|**1**|土曜日|  
|**2**|月曜日|  
|**4**|Tuesday|  
|**8**|水曜日|  
|**16**|Thursday|  
|**32**|金曜日|  
|**64**|土曜日|  
  
 [ @netsend_address =] '*netsend_address*'  
 ネットワークメッセージの送信先オペレーターのネットワークアドレス。 *netsend_address*は **nvarchar (100)**,、既定値は NULL です。  
  
 [ @category_name =] '*category*'  
 このアラートのカテゴリの名前。 *category* は **sysname**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 sp_update_operator は、msdb データベースから実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では sysadmin 固定サーバー ロールのメンバーに与えられています。  
  
## <a name="examples"></a>例  
 次の例では、無効であったオペレーターの状態を有効に更新し、ポケットベルを受信できる曜日 (月曜～金曜日、 午前 8 時～午後 5 時) を設定します。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_operator   
    @name = N'François Ajenstat',  
    @enabled = 1,  
    @email_address = N'françoisa',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 64 ;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_add_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
