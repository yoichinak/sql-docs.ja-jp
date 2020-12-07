---
description: sp_validate_redirected_publisher (Transact-sql)
title: sp_validate_redirected_publisher (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_validate_redirected_publisher
- sp_validate_redirected_publisher_TSQL
helpviewer_keywords:
- sp_validate_redirected_publisher
ms.assetid: 2b7fdbad-17e4-4442-b0b2-9b5e8f84b91d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 42184546069fb5358fbdc8863998b7bda74f89a4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534762"
---
# <a name="sp_validate_redirected_publisher-transact-sql"></a>sp_validate_redirected_publisher (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  パブリッシング データベースの現在のホストがレプリケーションをサポートできることを確認します。 ディストリビューション データベースから実行する必要があります。 このプロシージャは **sp_get_redirected_publisher**によって呼び出されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
      sp_validate_redirected_publisher   
    [ @original_publisher = ] 'original_publisher',  
    [ @publisher_db = ] 'database_name',   
    [ @redirected_publisher = ] 'new_publisher' output  
```  
  
## <a name="arguments"></a>引数  
`[ @original_publisher = ] 'original_publisher'` データベースを最初にパブリッシュしたのインスタンスの名前 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 *original_publisher* は **sysname**であり、既定値はありません。  
  
`[ @publisher_db = ] 'publisher_db'` パブリッシュされるデータベースの名前。 *publisher_db* は **sysname**であり、既定値はありません。  
  
`[ @redirected_publisher = ] 'redirected_publisher'` パブリッシャー/データベースのペアに対して **sp_redirect_publisher** が呼び出されたときに指定されたリダイレクトの対象。 *redirected_publisher* は **sysname**であり、既定値はありません。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 [なし] :  
  
## <a name="remarks"></a>解説  
 パブリッシャーとパブリッシングデータベースのエントリが存在しない場合、 **sp_validate_redirected_publisher**出力パラメーター * \@ redirected_publisher*に null が返されます。 エントリが存在する場合は、成功と失敗の両方のケースで出力パラメーターに返されます。  
  
 検証が成功した場合、 **sp_validate_redirected_publisher** は成功を示す値を返します。  
  
 検証が失敗した場合は、エラーを説明するエラーが発生します。  
  
## <a name="permissions"></a>アクセス許可  
 呼び出し元は、 **sysadmin** 固定サーバーロールのメンバーであるか、ディストリビューションデータベースの **db_owner** 固定データベースロールのメンバーであるか、パブリッシャーデータベースに関連付けられている定義済みパブリケーションのパブリケーションアクセスリストのメンバーである必要があります。  
  
## <a name="see-also"></a>参照  
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_get_redirected_publisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-get-redirected-publisher-transact-sql.md)   
 [sp_redirect_publisher &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-redirect-publisher-transact-sql.md)   
 [sp_validate_replica_hosts_as_publishers &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-validate-replica-hosts-as-publishers-transact-sql.md)  
  
  
