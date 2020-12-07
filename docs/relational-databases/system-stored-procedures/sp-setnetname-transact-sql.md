---
description: sp_setnetname (Transact-SQL)
title: sp_setnetname (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_setnetname
- sp_setnetname_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_setnetname
ms.assetid: f416ba81-3835-4588-b0a3-2fe75589490e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 71584754f3b175201623a222feae6722f39809ce
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543073"
---
# <a name="sp_setnetname-transact-sql"></a>sp_setnetname (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  のリモートインスタンスの実際のネットワークコンピューター名に、 **sys. サーバー** のネットワーク名を設定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 このプロシージャを使用すると、無効な識別子が含まれているネットワーク名を持つコンピューターに対して、リモートストアドプロシージャ呼び出しを実行でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_setnetname  
@server = 'server',   
     @netname = 'network_name'  
```  
  
## <a name="arguments"></a>引数  
 ** @server = '** *サーバー* **'**  
 ユーザーが作成したリモート ストアド プロシージャ呼び出しの構文で参照しているリモート サーバーの名前を指定します。 この*サーバー*を使用するには、既に1行の**サーバーが存在**している必要があります。 *server* のデータ型は **sysname**で、既定値はありません。  
  
 ** @netname = '** *network_name* **'**  
 リモートストアドプロシージャ呼び出しが行われるコンピューターのネットワーク名を指定します。 *network_name* は **sysname**であり、既定値はありません。  
  
 この名前は Windows コンピューター名と一致する必要があり、名前には [!INCLUDE[msCoName](../../includes/msconame-md.md)] 識別子で許可されていない文字を含めることができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 コンピューター名に無効な識別子が含まれていると、Windows コンピューターへのリモートストアドプロシージャの呼び出しで問題が発生することがあります。  
  
 リンク サーバーとリモート サーバーは同じ名前空間に存在するため、同じ名前にはできません。 ただし、指定したサーバーに対してリンクサーバーとリモートサーバーの両方を定義するには、別の名前を割り当て、 **sp_setnetname** を使用して、いずれかのネットワーク名を基になるサーバーのネットワーク名に設定します。  
  
```  
--Assume sqlserv2 is actual name of SQL Server   
--database server  
EXEC sp_addlinkedserver 'sqlserv2';  
GO  
EXEC sp_addserver 'rpcserv2';  
GO  
EXEC sp_setnetname 'rpcserv2', 'sqlserv2';  
```  
  
> [!NOTE]  
>  **Sp_setnetname**を使用してリンクサーバーをローカルサーバーに戻すことはサポートされていません。 この方法で参照されているサーバーは、分散トランザクションに参加できません。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールと**setupadmin**固定サーバーロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リモートストアドプロシージャ呼び出しを実行するためにで使用される一般的な管理シーケンスを示しています。  
  
```  
USE master;  
GO  
EXEC sp_addserver 'Win_1';  
EXEC sp_setnetname 'Win_1','Win-1';  
EXEC Win_1.master.dbo.sp_who;  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_addserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
