---
description: sp_addmessage (Transact-sql)
title: sp_addmessage (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addmessage
- sp_addmessage_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addmessage
ms.assetid: 54746d30-f944-40e5-a707-f2d9be0fb9eb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 306fc9b2316d599380b3a6e781d4f8a1ef646626
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89529222"
---
# <a name="sp_addmessage-transact-sql"></a>sp_addmessage (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  のインスタンスに新しいユーザー定義エラーメッセージを格納 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] します。 **Sp_addmessage**を使用して格納されたメッセージを表示するには、**メッセージ**カタログビューを使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addmessage [ @msgnum= ] msg_id , [ @severity= ] severity , [ @msgtext= ] 'msg'   
     [ , [ @lang= ] 'language' ]   
     [ , [ @with_log= ] { 'TRUE' | 'FALSE' } ]   
     [ , [ @replace= ] 'replace' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @msgnum = ] msg_id` メッセージの ID を示します。 *msg_id* は **int** で、既定値は NULL です。 ユーザー定義エラーメッセージの*msg_id*には、50001 ~ 2147483647 の整数を指定できます。 *Msg_id*と*言語*の組み合わせは一意である必要があります。指定された言語の ID が既に存在する場合は、エラーが返されます。  
  
`[ @severity = ]severity` は、エラーの重大度レベルです。 *重大度* は **smallint** で、既定値は NULL です。 有効なレベルは 1 ～ 25 です。 重大度レベルの詳細については、「 [データベース エンジン エラーの重大度](../../relational-databases/errors-events/database-engine-error-severities.md)」を参照してください。  
  
`[ @msgtext = ] 'msg'` エラーメッセージのテキストを示します。 *msg* は **nvarchar (255)** で、既定値は NULL です。  
  
`[ @lang = ] 'language'` は、このメッセージの言語です。 *language* は **sysname** 既定値は NULL です。 複数の言語を同じサーバーにインストールすることができるため、 *language* は各メッセージを記述する言語を指定します。 *Language*を省略すると、その言語はセッションの既定の言語になります。  
  
`[ @with_log = ] { 'TRUE' | 'FALSE' }` メッセージが発生したときに Windows アプリケーションログに書き込むかどうかを指定します。 ** \@ with_log**は**varchar (5)** で、既定値は FALSE です。 TRUE の場合、エラーは常に Windows アプリケーションログに書き込まれます。 FALSE の場合、常に Windows のアプリケーション ログに書き込まれるわけではありませんが、エラーの発生状況によっては書き込まれることもあります。 このオプションを使用できるのは、 **sysadmin** サーバーロールのメンバーだけです。  
  
> [!NOTE]  
>  Windows のアプリケーション ログにメッセージを書き込む場合は、[!INCLUDE[ssDE](../../includes/ssde-md.md)]のエラー ログ ファイルにも同じ内容が書き込まれます。  
  
`[ @replace = ] 'replace'` 文字列の *置換*として指定した場合、既存のエラーメッセージは新しいメッセージテキストと重大度レベルで上書きされます。 *replace* は **varchar (7)** で、既定値は NULL です。 *Msg_id*が既に存在する場合は、このオプションを指定する必要があります。 米国英語のメッセージを置き換えると、同じ *msg_id*を持つ他のすべての言語のすべてのメッセージの重大度レベルが置き換えられます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の英語以外のバージョンで、別の言語を使用してメッセージを追加するには、あらかじめ英語版のメッセージが存在している必要があります。 2 つのバージョンのメッセージの重大度は同じであることが必要です。  
  
 パラメーターを含むメッセージをローカライズする場合は、元のメッセージのパラメーターに対応するパラメーター番号を使用します。 各パラメーター番号の後に感嘆符 (!) を挿入します。  
  
|元のメッセージ|ローカライズされたメッセージ|  
|----------------------|-----------------------|  
|' 元のメッセージ param 1:% s、<br /><br /> param 2: %d'|' ローカライズされたメッセージ param 1: %1!、<br /><br /> param 2: %2! '|  
  
 言語の構文に相違があるため、ローカライズされたメッセージのパラメーター番号は、元のメッセージと同じ順に出現しないことがあります。  
  
## <a name="permissions"></a>アクセス許可  
**Sysadmin**または**serveradmin**固定サーバーロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-defining-a-custom-message"></a>A. カスタムメッセージの定義  
 次の例では、カスタムメッセージを **sys. メッセージ**に追加します。  
  
```  
USE master;  
GO  
EXEC sp_addmessage 50001, 16,   
   N'Percentage expects a value between 20 and 100.   
   Please reexecute with a more appropriate value.';  
GO  
```  
  
### <a name="b-adding-a-message-in-two-languages"></a>B. 2 種類の言語のメッセージを追加する  
 次の例では、まず英語のメッセージを追加し、次に同じメッセージのフランス語版を追加します。`.`  
  
```  
USE master;  
GO  
EXEC sp_addmessage @msgnum = 60000, @severity = 16,   
   @msgtext = N'The item named %s already exists in %s.',   
   @lang = 'us_english';  
  
EXEC sp_addmessage @msgnum = 60000, @severity = 16,   
   @msgtext = N'L''élément nommé %1! existe déjà dans %2!',   
   @lang = 'French';  
GO  
```  
  
### <a name="c-changing-the-order-of-parameters"></a>C. パラメーターの順序を変更する  
 次の例では、まず英語のメッセージを追加し、次にパラメーターの順序を変えてローカライズされたメッセージを追加します。  
  
```  
USE master;  
GO  
  
EXEC sp_addmessage   
    @msgnum = 60000,   
    @severity = 16,  
    @msgtext =   
        N'This is a test message with one numeric  
        parameter (%d), one string parameter (%s),   
        and another string parameter (%s).',  
    @lang = 'us_english';  
  
EXEC sp_addmessage   
    @msgnum = 60000,   
    @severity = 16,  
    @msgtext =   
        -- In the localized version of the message,  
        -- the parameter order has changed. The   
        -- string parameters are first and second  
        -- place in the message, and the numeric   
        -- parameter is third place.  
        N'Dies ist eine Testmeldung mit einem   
        Zeichenfolgenparameter (%3!),  
        einem weiteren Zeichenfolgenparameter (%2!),   
        und einem numerischen Parameter (%1!).',  
    @lang = 'German';  
GO    
  
-- Changing the session language to use the U.S. English  
-- version of the error message.  
SET LANGUAGE us_english;  
GO  
  
RAISERROR(60000,1,1,15,'param1','param2') -- error, severity, state,  
GO                                       -- parameters.  
  
-- Changing the session language to use the German  
-- version of the error message.  
SET LANGUAGE German;  
GO  
  
RAISERROR(60000,1,1,15,'param1','param2'); -- error, severity, state,   
GO                                       -- parameters.  
```  
  
## <a name="see-also"></a>参照  
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [sp_altermessage &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)   
 [sp_dropmessage &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
