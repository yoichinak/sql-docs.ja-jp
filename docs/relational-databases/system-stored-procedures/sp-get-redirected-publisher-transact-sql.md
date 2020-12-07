---
description: sp_get_redirected_publisher (Transact-sql)
title: sp_get_redirected_publisher (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_get_redirected_publisher_TSQL
- sp_get_redirected_publisher
ms.assetid: d47a9ab5-f2cc-42a8-8be9-a33895ce44f0
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5a71799e3d7820ce4a142d6c9ec7d55b743214fb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89538936"
---
# <a name="sp_get_redirected_publisher-transact-sql"></a>sp_get_redirected_publisher (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  元のパブリッシャーがリダイレクトされているかどうかを判断するために、レプリケーション エージェントがディストリビューターに対してクエリを実行するときに使用されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_get_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @bypass_publisher_validation = ] [0 | 1 ]  
```  
  
## <a name="arguments"></a>引数  
`[ @original_publisher = ] 'original_publisher'` データベースを最初にパブリッシュした SQL Server のインスタンスの名前。 *original_publisher* は **sysname**であり、既定値はありません。
  
`[ @publisher_db = ] 'publisher_db'` パブリッシュされるデータベースの名前。 *publisher_db* は **sysname**であり、既定値はありません。  
  
`[ @bypass_publisher_validation = ] [0 | 1 ]` リダイレクトされたパブリッシャーの検証をバイパスするために使用します。 0の場合、検証が実行されます。 1 の場合は、検証が実行されません。 *bypass_publisher_validation* は **ビット**,、既定値は0です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**redirected_publisher**|**sysname**|リダイレクト後のパブリッシャーの名前。|  
|**error_number**|**int**|検証エラーのエラー番号。|  
|**error_severity**|**int**|検証エラーの重大度。|  
|**error_message**|**nvarchar (4000)**|検証エラーメッセージのテキスト。|  
  
## <a name="remarks"></a>解説  
 *redirected_publisher* は、現在の発行元の名前を返します。 パブリッシャーおよびパブリッシングデータベースが **sp_redirect_publisher**を使用してリダイレクトされていない場合は null を返します。  
  
 検証が要求されていない場合、またはパブリッシャーとパブリッシングデータベースのエントリが存在しない場合、 *error_number* と *error_severity* は0を返し、 *error_message* は null を返します。  
  
 検証が要求された場合、検証ストアドプロシージャ [sp_validate_redirected_publisher &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md) を呼び出して、リダイレクトの対象がパブリッシングデータベースに適したホストであることを確認します。 検証が成功した場合、 **sp_get_redirected_publisher** はリダイレクトされたパブリッシャー名を返します。 *error_number* 列および *error_severity* 列の場合は0、 *error_message* 列の場合は null になります。  
  
 検証が要求されて失敗した場合は、リダイレクトされたパブリッシャー名がエラー情報と共に返されます。  
  
## <a name="permissions"></a>アクセス許可  
 呼び出し元は、 **sysadmin** 固定サーバーロールのメンバーであるか、ディストリビューションデータベースの **db_owner** 固定データベースロールのメンバーであるか、パブリッシャーデータベースに関連付けられている定義済みパブリケーションのパブリケーションアクセスリストのメンバーである必要があります。  
  
## <a name="see-also"></a>参照  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_validate_redirected_publisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-validate-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
