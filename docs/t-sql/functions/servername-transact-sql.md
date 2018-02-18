---
title: "@@SERVERNAME (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 09/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@SERVERNAME'
- '@@SERVERNAME_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- '@@SERVERNAME function'
- local servers [SQL Server]
ms.assetid: b0ef33fb-954a-4294-b05b-a87c14ce25a3
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5f1e7dbd47562368653ce75eee9d2a412164a9c9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40servername-transact-sql"></a>&#x40;&#x40;サーバー名 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を実行しているローカル サーバーの名前を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
@@SERVERNAME  
```  
  
## <a name="return-types"></a>戻り値の型  
 **nvarchar**  
  
## <a name="remarks"></a>解説  
 サーバー名には、インストール時に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップ プログラムによってコンピューター名が設定されます。 サーバーの名前を変更するには、**sp_addserver** を使用し、その後 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を再起動します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の複数のインスタンスがインストールされている状態で、ローカル サーバー名がセットアップ以降変更されていない場合は、@@SERVERNAME によって次のローカル サーバー名情報が返されます。  
  
|インスタンス|サーバー情報|  
|--------------|------------------------|  
|既定のインスタンス|'*servername*'|  
|名前付きインスタンス|'*servername*\\*instancename*'|  
|フェールオーバー クラスター インスタンス - 既定のインスタンス|'*virtualservername*'|  
|フェールオーバー クラスター インスタンス - 名前付きインスタンス|'*virtualservername*\\*instancename*'|  
  
 @@SERVERNAME 関数が返す文字列と、SERVERPROPERTY 関数の SERVERNAME プロパティが返す文字列は、形式は似ていますが、その情報は異なる可能性があります。 SERVERNAME プロパティの場合は、コンピューターのネットワーク名の変更を自動的にレポートします。  
  
 これに対して、@@SERVERNAME はこのような変更をレポートしません。 @@SERVERNAME は、**sp_addserver** ストアド プロシージャまたは **sp_dropserver** ストアド プロシージャを使用して、ローカル サーバー名に加えられた変更をレポートします。  
  
## <a name="examples"></a>使用例  
 次に、`@@SERVERNAME` の使用例を示します。  
  
```  
SELECT @@SERVERNAME AS 'Server Name'  
```  
  
 次に結果セットの例を示します。  
  
```  
Server Name  
---------------------------------  
ACCTG  
  
```  
  
## <a name="see-also"></a>参照  
 [構成関数 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)  
  
  
