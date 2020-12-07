---
description: sp_set_firewall_rule (Azure SQL データベース)
title: sp_set_firewall_rule (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 07/28/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_set_firewall_rule
- sp_set_firewall_rule_TSQL
- sys.sp_set_firewall_rule
- sys.sp_set_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_firewall_rule
- firewall_rules, setting server rules
ms.assetid: a974a561-5382-4039-8499-3a56767bcefe
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: ed1df2288067d30f9443736b914b7560c0c6a784
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810481"
---
# <a name="sp_set_firewall_rule-azure-sql-database"></a>sp_set_firewall_rule (Azure SQL データベース)
[!INCLUDE [asdb-asa](../../includes/applies-to-version/asdb-asa.md)]

  [!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーのサーバーレベルのファイアウォールの設定を作成または更新します。 このストアドプロシージャを使用できるのは、master データベースで、サーバーレベルプリンシパルログインまたは Azure Active Directory プリンシパルが割り当てられている場合のみです。  
  
  
## <a name="syntax"></a>構文  
  
```
sp_set_firewall_rule [@name =] 'name', 
    [@start_ip_address =] 'start_ip_address', 
    [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 次の表は、でサポートされている引数とオプションを示して [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] います。  
  
|名前|DataType|説明|  
|----------|--------------|-----------------|  
|[ @name =] ' name '|**NVARCHAR (128)**|サーバーレベルのファイアウォールの設定を説明し、区別するための名前です。|  
|[ @start_ip_address =] ' start_ip_address '|**VARCHAR (50)**|サーバーレベルのファイアウォール設定の範囲の最下位の IP アドレスです。 この IP アドレス以上の IP アドレスは、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーへの接続を試行できます。 設定できる最下位の IP アドレスは `0.0.0.0` です。|  
|[ @end_ip_address =] ' end_ip_address '|**VARCHAR (50)**|サーバーレベルのファイアウォール設定の範囲の最上位の IP アドレスです。 これ以下の IP アドレスは、[!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーへの接続を試みることができます。 設定できる最上位の IP アドレスは `255.255.255.255` です。<br /><br /> 注: このフィールドと *start_ip_address* フィールドの両方がと等しい場合は、Azure の接続試行が許可され `0.0.0.0` ます。|  
  
## <a name="remarks"></a>注釈  
 サーバー レベルのファイアウォール設定の名前は一意である必要があります。 ストアド プロシージャの設定の名前がファイアウォール設定テーブルに既に存在する場合、開始 IP アドレスと終了 IP アドレスが更新されます。 そうでない場合は、新しいサーバー レベルのファイアウォール設定が作成されます。  
  
 開始 IP アドレスおよび終了 IP アドレスが `0.0.0.0` であるサーバーレベルのファイアウォール設定を追加すると、Azure から [!INCLUDE[ssSDS](../../includes/sssds-md.md)] サーバーにアクセスできるようになります。 *Name*パラメーターに値を指定します。これは、サーバーレベルのファイアウォール設定の内容を思い出すのに役立ちます。  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] では、接続の認証に必要なログイン データおよびサーバー レベルのファイアウォール規則は、各データベースで一時的にキャッシュされます。 このキャッシュは定期的に更新されます。 認証キャッシュを強制的に更新し、データベースにログイン テーブルの最新バージョンがあることを確認するには、[DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md) を実行します。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーレベルのファイアウォールルールを作成または変更できるのは、プロビジョニング処理によって作成されたサーバーレベルのプリンシパルログイン、または管理者として割り当てられた Azure Active Directory プリンシパルだけです。 Sp_set_firewall_rule を実行するには、ユーザーが master データベースに接続されている必要があります。  
  
## <a name="examples"></a>例  
 次のコードでは、Azure からのアクセスを有効にする、`Allow Azure` という名前のサーバーレベルのファイアウォール設定を作成します。 仮想 master データベースで次のを実行します。  
  
```  
-- Enable Azure connections.  
exec sp_set_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 次のコードでは、IP アドレス `Example setting 1` だけを許可する、`0.0.0.2` という名前のサーバーレベルのファイアウォールの設定を作成します。 次に、 `sp_set_firewall_rule` `0.0.0.4` そのファイアウォール設定で、終了 IP アドレスをに更新するために、ストアドプロシージャが再度呼び出されます。 これにより、IP アドレス、、およびがサーバーにアクセスできるようになる範囲が作成さ `0.0.0.2` `0.0.0.3` `0.0.0.4` れます。  
  
```  
-- Create server-level firewall setting for only IP 0.0.0.2  
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.2';  
  
-- Update server-level firewall setting to create a range of allowed IP addresses
exec sp_set_firewall_rule N'Example setting 1', '0.0.0.2', '0.0.0.4';  
  
```  
  
## <a name="see-also"></a>参照  
 [Azure SQL Database ファイアウォール](/azure/azure-sql/database/firewall-configure)   
 [方法: ファイアウォール設定を構成する (Azure SQL Database)](/azure/azure-sql/database/firewall-configure)   
 [sys.firewall_rules &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-firewall-rules-azure-sql-database.md)