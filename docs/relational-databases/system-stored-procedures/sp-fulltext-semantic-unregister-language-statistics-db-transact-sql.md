---
description: sp_fulltext_semantic_unregister_language_statistics_db (Transact-sql)
title: sp_fulltext_semantic_unregister_language_statistics_db (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_unregister_language_statistics_db_TSQL
- sp_fulltext_semantic_unregister_language_statistics_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_semantic_unregister_language_statistics_db
ms.assetid: 1426ca4a-9a76-489e-98da-8f6d13ff9732
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6db576de824f098911229409498527e1aaf9d3ad
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543391"
---
# <a name="sp_fulltext_semantic_unregister_language_statistics_db-transact-sql"></a>sp_fulltext_semantic_unregister_language_statistics_db (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  の現在のインスタンスから既存のセマンティック言語統計データベースの登録 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を解除し、関連付けられているメタデータを削除します。  
  
 このステートメントでは、データベースをデタッチしたり、ファイルシステムから物理データベースファイルを削除したりすることはありません。 データベースの登録の解除後は、それをデタッチし、物理的なデータベース ファイルを削除することができます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引数  
 このプロシージャは、引数を必要としません。 のインスタンスに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はセマンティック言語統計データベースが1つしかないため、データベースを識別する必要はありません。  
  
## <a name="return-code-value"></a>リターン コード値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-set"></a>結果セット  
 なし。  
  
## <a name="general-remarks"></a>全般的な解説  
 セマンティック言語統計データベースの登録が解除されると、それに関連付けられているすべてのメタデータも削除されます。  
  
 **sp_fulltext_semantic_unregister_language_statistics_db** では、次の手順を実行します。  
  
1.  の現在のインスタンスに対して、実行中のセマンティック作成がないことを確認 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。  
  
2.  指定されたセマンティック言語統計データベースに関連付けられているすべてのメタデータを削除します。  

 詳細については、「 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)」を参照してください。  
  
## <a name="metadata"></a>Metadata  
 のインスタンスにインストールされているセマンティック言語統計データベースの詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] カタログビューの [Fulltext_semantic_language_statistics_database &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)に対してクエリを実行します。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 CONTROL SERVER 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、 **sp_fulltext_semantic_unregister_language_statistics_db**を呼び出して、セマンティック言語統計データベースの登録を解除する方法を示します。  
  
```sql  
EXEC sp_fulltext_semantic_unregister_language_statistics_db;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
