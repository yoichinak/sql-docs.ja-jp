---
description: sp_pdw_add_network_credentials (Azure Synapse Analytics)
title: sp_pdw_add_network_credentials
titleSuffix: Azure Synapse Analytics
ms.date: 03/14/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0729eeff-ac7e-43f0-80fa-ff5346a75985
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.custom: seo-dt-2019
ms.openlocfilehash: 212e8e5ab05204a6497282e79c4134dcff844299
ms.sourcegitcommit: 894c1a23e922dc29b82c1d2c34c7b0ff28b38654
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93067322"
---
# <a name="sp_pdw_add_network_credentials-azure-synapse-analytics"></a>sp_pdw_add_network_credentials (Azure Synapse Analytics)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  これにより、にネットワーク資格情報が格納さ [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] れ、サーバーに関連付けられます。 たとえば、このストアドプロシージャを使用して、 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 対象サーバーでデータベースのバックアップと復元操作を実行したり、TDE に使用する証明書のバックアップを作成したりするための適切な読み取り/書き込み権限を付与します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql  
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  
  
sp_pdw_add_network_credentials 'target_server_name',  'user_name', 'password'  
```  
[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="arguments"></a>引数  
 ' *target_server_name* '  
 対象サーバーのホスト名または IP アドレスを指定します。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] は、このストアドプロシージャに渡されたユーザー名とパスワードの資格情報を使用して、このサーバーにアクセスします。  
  
 InfiniBand ネットワーク経由で接続するには、対象サーバーの InfiniBand IP アドレスを使用します。  
  
 *target_server_name* は nvarchar (]) として定義されています。  
  
 ' *user_name* '  
 対象サーバーにアクセスする権限を持つ user_name を指定します。 対象サーバーの資格情報が既に存在する場合は、新しい資格情報に更新されます。  
  
 *user_name* は nvarchar (513) として定義されています。  
  
 ' *password* ꞌ  
 *User_name* のパスワードを指定します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="permissions"></a>アクセス許可  
 **ALTER SERVER STATE** 権限が必要です。  
  
## <a name="error-handling"></a>エラー処理  
 [制御] ノードおよびすべての計算ノードで資格情報を追加できない場合、エラーが発生します。  
  
## <a name="general-remarks"></a>全般的な解説  
 このストアドプロシージャは、の NetworkService アカウントにネットワーク資格情報を追加し [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] ます。 NetworkService アカウントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 制御ノードとコンピューティングノードで SMP の各インスタンスを実行します。 たとえば、バックアップ操作を実行すると、制御ノードと各コンピューティングノードは NetworkService アカウントの資格情報を使用して、対象サーバーに対する読み取りと書き込みのアクセス許可を取得します。  
  
## <a name="examples-sssdwfull-and-sspdw"></a>例: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-add-credentials-for-performing-a-database-backup"></a>A. データベースバックアップを実行するための資格情報を追加する  
 次の例では、ドメインユーザーのユーザー名とパスワードの資格情報を、10.172.63.255 という IP アドレスを持つ対象サーバーに関連付けます。 ユーザーは、対象サーバーに対する読み取り/書き込み権限を持っています。 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] は、これらの資格情報を格納し、バックアップ操作と復元操作に必要な場合に、対象サーバーとの間での読み書きに使用します。  
  
```sql  
EXEC sp_pdw_add_network_credentials '10.172.63.255', 'seattle\david', '********';  
```  
  
 Backup コマンドでは、サーバー名を IP アドレスとして入力する必要があります。  
  
> [!NOTE]  
>  InfiniBand でデータベースのバックアップを実行するには、必ずバックアップサーバーの InfiniBand IP アドレスを使用してください。  
  
## <a name="see-also"></a>参照  
 [sp_pdw_remove_network_credentials &#40;Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
  

