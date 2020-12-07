---
description: '&#x40;&#x40;SERVERNAME (Transact-SQL)'
title: '@@SERVERNAME (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@SERVERNAME'
- '@@SERVERNAME_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@SERVERNAME function'
- local servers [SQL Server]
ms.assetid: b0ef33fb-954a-4294-b05b-a87c14ce25a3
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8407991622201fe3798695c4aecdd4514c5492f9
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379684"
---
# <a name="x40x40servername-transact-sql"></a>&#x40;&#x40;SERVERNAME (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているローカル サーバーの名前を返します。  
 ![記事リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
@@SERVERNAME  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 **nvarchar**  
  
## <a name="remarks"></a>解説  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップによって、サーバー名がインストール時のコンピューター名に設定されます。 サーバーの名前を変更するには、**sp_addserver** を使用し、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスが複数インストールされている状態で、ローカル サーバー名がセットアップ以来変更されていない場合は、@@SERVERNAME によって次のローカル サーバー名情報が返されます。  
  
|インスタンス|サーバー情報|  
|--------------|------------------------|  
|既定のインスタンス|'*servername*'|  
|名前付きインスタンス|'*servername*\\*instancename*'|  
|フェールオーバー クラスター インスタンス - 既定のインスタンス|'*network_name_for_fci_in_wsfc*'|  
|フェールオーバー クラスター インスタンス - 名前付きインスタンス|'*network_name_for_fci_in_wsfc*\\*instancename*'|  
  
 @@SERVERNAME 関数と SERVERPROPERTY 関数の SERVERNAME プロパティは、似たような形式の文字列を返す場合がありますが、情報は異なる可能性があります。 SERVERNAME プロパティの場合は、コンピューターのネットワーク名の変更を自動的にレポートします。  
  
 一方、@@SERVERNAME はこのような変更をレポートしません。 @@SERVERNAME は、**sp_addserver** ストアド プロシージャまたは **sp_dropserver** ストアド プロシージャを使用してローカル サーバー名に加えられた変更をレポートします。  
  
## <a name="examples"></a>例  
 次の例に、`@@SERVERNAME` の使用方法を示します。  
  
```sql  
SELECT @@SERVERNAME AS 'Server Name'  
```  
  
 次に結果セットの例を示します。  
  
```  
Server Name  
---------------------------------  
ACCTG  
  
```  
  
## <a name="see-also"></a>関連項目  
 [構成関数 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)  
  
  
