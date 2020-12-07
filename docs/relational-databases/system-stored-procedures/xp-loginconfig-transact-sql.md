---
description: xp_loginconfig (Transact-sql)
title: xp_loginconfig (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_loginconfig_TSQL
- xp_loginconfig
dev_langs:
- TSQL
helpviewer_keywords:
- xp_loginconfig
ms.assetid: d380e799-2857-408a-bcbf-5e73a8e6aa5a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9e86352f992698387334531398bafc5bdfdc2d61
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419256"
---
# <a name="xp_loginconfig-transact-sql"></a>xp_loginconfig (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  のインスタンスのログインセキュリティ構成を報告し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
xp_loginconfig ['config_name']  
```  
  
## <a name="arguments"></a>引数  
 **'** *config_name* **'**  
 表示する構成値を指定します。 *Config_name*が指定されていない場合は、すべての構成値が報告されます。 *config_name* は **sysname**で、既定値は NULL です。次のいずれかの値を指定できます。  
  
|値|説明|  
|-----------|-----------------|  
|**login mode**|ログインセキュリティモード。 使用できる値は、 **Mixed** と **Windows 認証**です。<br /><br /> 置換後の方法:<br /><br /> `SELECT SERVERPROPERTY('IsIntegratedSecurityOnly'); GO`|  
|**default login**|信頼関係接続が許可されているユーザー (ログイン名が照合されないユーザー) に対する、既定の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン ID の名前。 既定のログインは **guest**です。 この値は、旧バージョンとの互換性のために用意されています。|  
|**[既定のドメイン]**|信頼関係接続のネットワークユーザーの既定の Windows ドメインの名前。 既定のドメインは、Windows および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているコンピューターのドメインです。 この値は、旧バージョンとの互換性のために用意されています。|  
|**監査レベル**|監査レベル。 指定できる値は、 **none**、 **success**、 **failure**、および **all**です。 監査はエラー ログや Windows イベント ビューアーに書き込まれます。|  
|**set hostname**|クライアントのログイン レコードのホスト名が、Windows ネットワーク ユーザー名と置き換えられるかどうかを示します。 指定できる値は、 **true** または **false**です。 これが設定されている場合、ネットワークユーザー名は **sp_who**の出力に表示されます。|  
|**付け**|有効なアンダースコア文字 (_) にマップされている特殊な Windows 文字を報告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 指定できる値は、 **ドメイン区切り記号** (既定値)、 **スペース**、 **null**、または任意の1文字です。 この値は、旧バージョンとの互換性のために用意されています。|  
|**マップ $**|有効なドル記号 ($) にマップされている特殊な Windows 文字を報告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 指定できる値は、 **ドメイン区切り**文字、 **スペース**、 **null**、または任意の1文字です。 既定値は **space**です。 この値は、旧バージョンとの互換性のために用意されています。|  
|**map #**|有効なシャープ記号 (#) にマップされている特殊な Windows 文字を報告 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。 指定できる値は、 **ドメイン区切り**文字、 **スペース**、 **null**、または任意の1文字です。 既定値はハイフンです。 この値は、旧バージョンとの互換性のために用意されています。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|構成値。|  
|**config value**|**sysname**|構成値の設定|  
  
## <a name="remarks"></a>解説  
 **xp_loginconfig** を使用して構成値を設定することはできません。  
  
 ログインモードと監査レベルを設定するには、を使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] します。  
  
## <a name="permissions"></a>アクセス許可  
 **Master**データベースに対する CONTROL 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-how-to-report-all-configuration-values"></a>A. すべての構成値をレポートする方法  
 次の例では、現在構成されている設定をすべて表示します。  
  
```  
EXEC xp_loginconfig;  
GO  
```  
  
### <a name="b-how-to-report-a-specific-configuration-value"></a>B. 特定の構成値をレポートする方法  
 次の例は、ログインモードのみの設定を示しています。  
  
```  
EXEC xp_loginconfig 'login mode';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_denylogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [システムストアドプロシージャ &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_revokelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
