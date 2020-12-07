---
description: sp_registercustomresolver (Transact-sql)
title: sp_registercustomresolver (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_registercustomresolver
- sp_registercustomresolver_TSQL
helpviewer_keywords:
- sp_registercustomresolver
ms.assetid: 6d2b0472-0e1f-4005-833c-735d1940fe93
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bd973ace7e8edbd7a5ec561fd53a19f8a7a05a92
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543175"
---
# <a name="sp_registercustomresolver-transact-sql"></a>sp_registercustomresolver (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マージレプリケーションの同期処理中に呼び出すことができるビジネスロジックハンドラーまたは COM ベースのカスタム競合回避モジュールを登録します。 このストアドプロシージャは、ディストリビューター側で実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_registercustomresolver [ @article_resolver = ] 'article_resolver'   
    [ , [ @resolver_clsid = ] 'resolver_clsid' ]  
    [ , [ @is_dotnet_assembly = ] 'is_dotnet_assembly' ]  
    [ , [ @dotnet_assembly_name = ] 'dotnet_assembly_name' ]  
    [ , [ @dotnet_class_name = ] 'dotnet_class_name' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @article_resolver = ] 'article_resolver'` 登録するカスタムビジネスロジックのフレンドリ名を指定します。 *article_resolver* は **nvarchar (255)**,、既定値はありません。  
  
`[ @resolver_clsid = ] 'resolver_clsid'` 登録する COM オブジェクトの CLSID 値を指定します。 カスタムビジネスロジック *resolver_clsid* は **nvarchar (50)**,、既定値は NULL です。 ビジネスロジックハンドラーアセンブリを登録するときに、このパラメーターを有効な CLSID に設定するか、NULL に設定する必要があります。  
  
`[ @is_dotnet_assembly = ] 'is_dotnet_assembly'` 登録するカスタムビジネスロジックの種類を指定します。 *is_dotnet_assembly* は **nvarchar (50)**,、既定値は FALSE です。 **true** は、登録されているカスタムビジネスロジックがビジネスロジックハンドラーアセンブリであることを示します。 **false** は、COM コンポーネントであることを示します。  
  
`[ @dotnet_assembly_name = ] 'dotnet_assembly_name'` は、ビジネスロジックハンドラーを実装するアセンブリの名前です。 *dotnet_assembly_name* は **nvarchar (255)**,、既定値は NULL です。 マージ エージェントの実行可能ファイルがあるディレクトリ、マージ エージェントを同期的に起動するアプリケーションがあるディレクトリ、およびグローバル アセンブリ キャッシュ (GAC) の、いずれとも異なる場所にアセンブリが配置されている場合は、アセンブリの完全なパスを指定する必要があります。  
  
`[ @dotnet_class_name = ] 'dotnet_class_name'` は、 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> ビジネスロジックハンドラーを実装するためにをオーバーライドするクラスの名前です。 名前は、 **Namespace. Classname**という形式で指定する必要があります。 *dotnet_class_name* は **nvarchar (255)**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_registercustomresolver** は、マージレプリケーションで使用します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_registercustomresolver**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [マージ アーティクルのビジネス ロジック ハンドラーの実装](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [マージアーティクルのカスタム競合回避モジュールの実装](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [sp_lookupcustomresolver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
