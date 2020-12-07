---
description: sysmail_configure_sp (Transact-SQL)
title: sysmail_configure_sp (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_configure_sp_TSQL
- sysmail_configure_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_configure_sp
ms.assetid: 73b33c56-2bff-446a-b495-ae198ad74db1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b16f0e11cc38abbbaf14abd4b21e7334a578c1cb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538465"
---
# <a name="sysmail_configure_sp-transact-sql"></a>sysmail_configure_sp (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベース メールの構成設定を変更します。 **Sysmail_configure_sp**で指定された構成設定は、インスタンス全体に適用され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sysmail_configure_sp [ [ @parameter_name = ] 'parameter_name' ]  
    [ , [ @parameter_value = ] 'parameter_value' ]  
    [ , [ @description = ] 'description' ]  
```  
  
## <a name="arguments"></a>引数  
 [ **@parameter_name** =] **'**_parameter_name_**'**  
 変更するパラメーターの名前。  
  
 [ **@parameter_value** =] **'**_parameter_value_**'**  
 パラメーターの新しい値を指定します。  
  
 [ **@description** =] **'**_description_**'**  
 パラメーターの説明。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 データベース メールでは次のパラメーターが使用されます。  
  
| パラメーター名 | 説明 | 既定値 |
| -------------- | ----------- | ------------- |
|*AccountRetryAttempts*|指定したプロファイル内の各アカウントを使用して、外部メール処理が電子メール メッセージの送信を試行する回数。|**1**|  
|*AccountRetryDelay*|外部メール処理が次回のメッセージ送信の試行を待機する時間 (秒単位)。|**5000**|  
|*DatabaseMailExeMinimumLifeTime*|外部メール処理がアクティブな状態にとどまる最小時間 (秒単位)。 データベースメールが多数のメッセージを送信している場合は、この値を大きくしてデータベースメールアクティブにして、頻繁な起動と停止のオーバーヘッドを回避します。|**600**|  
|*DefaultAttachmentEncoding*|電子メールの添付ファイルの既定のエンコーディング。|MIME|  
|*MaxFileSize*|添付ファイルの最大サイズ (バイト単位)。|**100万**|  
|*ProhibitedExtensions*|電子メールへの添付ファイルとして送信できない拡張子のコンマ区切りのリスト。|**exe、dll、vbs、js**|  
|*Logginglevel.information*|データベース メール ログに記録されるメッセージ。 次の数値のいずれかです。<br /><br /> 1-これは通常モードです。 エラーのみをログに記録します。<br /><br /> 2-これは拡張モードです。 エラー、警告、および情報メッセージをログに記録します。<br /><br /> 3-詳細モードです。 エラー、警告、情報メッセージ、成功メッセージ、および追加の内部メッセージをログに記録します。 トラブルシューティングを行うには、このモードを使用してください。|**2**|  
  
 ストアドプロシージャ **sysmail_configure_sp** は **msdb** データベースにあり、 **dbo** スキーマが所有しています。 現在のデータベースが **msdb**でない場合は、3つの部分で構成される名前を使用してプロシージャを実行する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャの実行権限は、既定では **sysadmin** 固定サーバーロールのメンバーに与えています。  
  
## <a name="examples"></a>例  
 **A. 各アカウントに対して 10 回再試行するようデータベース メールを設定する**  
  
 次の例では、アカウントに到達できないことを考慮する前に、各アカウントを10回再試行するようにデータベースメールを設定しています。  
  
```  
EXECUTE msdb.dbo.sysmail_configure_sp  
    'AccountRetryAttempts', '10' ;  
```  
  
 **B. 添付ファイルの最大サイズを 2 MB に設定する**  
  
 次の例では、添付ファイルの最大サイズを 2 MB に設定します。  
  
```  
EXECUTE msdb.dbo.sysmail_configure_sp  
    'MaxFileSize', '2097152' ;  
```  
  
## <a name="see-also"></a>参照  
 [データベース メール](../../relational-databases/database-mail/database-mail.md)   
 [sysmail_help_configure_sp &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sysmail-help-configure-sp-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースメール ](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
