---
description: sp_helpserver (Transact-SQL)
title: sp_helpserver (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpserver
- sp_helpserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpserver
ms.assetid: e8f42de7-c738-41c3-8bf5-dbd559dc7184
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6dace48b51c971095b136190ab1094ea8db79984
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89526660"
---
# <a name="sp_helpserver-transact-sql"></a>sp_helpserver (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  特定のリモート サーバーまたはレプリケーション サーバー、あるいはすべてのリモート サーバーとレプリケーション サーバーに関する情報をレポートします。 サーバー名、サーバーのネットワーク名、サーバーのレプリケーションの状態、サーバーの識別番号、および照合順序名を指定します。 では、リンクサーバーに接続したり、リンクサーバーに対してクエリを実行したりするためのタイムアウト値も提供されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpserver [ [ @server = ] 'server' ]   
  [ , [ @optname = ] 'option' ]   
  [ , [ @show_topology = ] 'show_topology' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @server = ] 'server'` 情報を報告するサーバーを指定します。 *サーバー*を指定しない場合、master.sys のすべてのサーバーに関するレポートが作成され**ます。** *サーバー* は **sysname**,、既定値は NULL です。  
  
`[ @optname = ] 'option'` サーバーを説明するオプションです。 *オプション* は **varchar (** 35 **)**,、既定値は NULL の場合、これらの値のいずれかを指定する必要があります。  
  
|[値]|説明|  
|-----------|-----------------|  
|**照合順序互換**|リンクサーバーに対する分散クエリの実行に影響します。 このオプションを true に設定した場合、|  
|**データアクセス**|分散クエリ アクセスに対してリンク サーバーを有効または無効にします。|  
|**dist**|ディストリビューターです。|  
|**dpub**|リモートパブリッシャーをこのディストリビューターに発行します。|  
|**lazy schema validation (lazy schema validation)**|クエリ開始時のリモート テーブルのスキーマ チェックをスキップします。|  
|**pub**|文書.|  
|**rpc-epmap**|指定されたサーバーからの RPC を有効にします。|  
|**rpc 出力**|指定されたサーバーへの RPC を有効にします。|  
|**sub**|サブスクライバ.|  
|**システム**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**リモート照合順序を使用する**|ローカルサーバーの照合順序ではなく、リモート列の照合順序を使用します。|  
  
`[ @show_topology = ] 'show_topology'` 指定したサーバーと他のサーバーとの関係を指定します。 *show_topology* は **varchar (** 1 **)**,、既定値は NULL です。 *Show_topology*が**t**と等しくない場合、またはが NULL の場合、 **sp_helpserver**結果セットセクションに一覧表示された列を返します。 *Show_topology*が**t**と等しい場合、結果セットに示されている列に加えて、 **sp_helpserver** **topx**および**topx**情報も返されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)。  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|サーバー名。|  
|**network_name**|**sysname**|サーバーのネットワーク名|  
|**status**|**varchar (** 70 **)**|サーバーの状態。|  
|**id**|**char (** 4 **)**|サーバーの識別番号|  
|**collation_name**|**sysname**|サーバーの照合順序。|  
|**connect_timeout**|**int**|リンクサーバーに接続するためのタイムアウト値。|  
|**query_timeout**|**int**|リンク サーバーに対するクエリのタイムアウト値|  
  
## <a name="remarks"></a>解説  
 1 つのサーバーについて複数の状態値が返されることもあります。  
  
## <a name="permissions"></a>アクセス許可  
 アクセス許可はチェックされません。  
  
## <a name="examples"></a>例  
  
### <a name="a-displaying-information-about-all-servers"></a>A. すべてのサーバーに関する情報の表示  
 次の例では、パラメーターを指定せずに `sp_helpserver` を使用して、すべてのサーバーに関する情報を表示します。  
  
```  
USE master;  
GO  
EXEC sp_helpserver;  
```  
  
### <a name="b-displaying-information-about-a-specific-server"></a>B. 特定のサーバーに関する情報を表示する  
 次の例では、サーバーに関するすべての情報を表示し `SEATTLE2` ます。  
  
```  
USE master;  
GO  
EXEC sp_helpserver 'SEATTLE2';  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_adddistpublisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_addserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_addsubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_changesubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
