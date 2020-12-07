---
description: sp_fulltext_semantic_register_language_statistics_db (Transact-sql)
title: sp_fulltext_semantic_register_language_statistics_db (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_semantic_register_language_statistics_db
- sp_fulltext_semantic_register_language_statistics_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_semantic_register_language_statistics_db
ms.assetid: bef1b104-5a44-4327-9ae4-45eae3000f7e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: deb1973dcff95f79d70ca3f458c38208db3b1f47
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548045"
---
# <a name="sp_fulltext_semantic_register_language_statistics_db-transact-sql"></a>sp_fulltext_semantic_register_language_statistics_db (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の現在のインスタンスで、事前にデータが設定されているセマンティック言語統計データベースを登録します。  
  
 セマンティック抽出は、この言語統計データベースをアタッチし、このストアドプロシージャを使用して登録した後にのみ開始できます。 このタスクは、のインスタンスごとに1回だけ実行する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db  
    [ @dbname = ] 'database_name';  
GO  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 引数  
 [ @dbname =] '*database_name*'  
 の現在のインスタンスに登録するセマンティック言語統計データベースの名前を指定し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 データベースが既にアタッチされている必要があります。 *database_name* は **sysname**であり、NULL にすることはできません。  
  
## <a name="return-code-value"></a>リターン コード値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-set"></a>結果セット  
 なし。  
  
## <a name="general-remarks"></a>全般的な解説  
 セマンティック言語統計データベースには、テキストコンテンツのセマンティック処理に必要な言語関連の統計情報が含まれています。  
  
 **sp_fulltext_semantic_register_language_statistics_db** では、次の手順を実行します。  
  
1.  のインスタンス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がセマンティック処理をサポートするバージョンであることを確認します。  
  
2.  のインスタンスに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セマンティック言語統計データベースが定義されていないことを確認します。  
  
3.  データベースが有効なセマンティック言語統計データベースであることを確認します。  
  
4.  セマンティック言語統計データベースに対する権限を設定して、ユーザーによるデータベースへのアクセスを制限します。  
  
5.  のインスタンスのセマンティック言語統計データベースの名前を定義するメタデータを挿入し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
6.  インストールされているセマンティック言語統計データベースと内部言語モデルテーブル間のマッピングを定義するメタデータを挿入します。  
  
7.  データベースを使用する準備ができているかどうかを確認します。  
  
 詳細については、「 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)」を参照してください。  
  
## <a name="metadata"></a>Metadata  
 のインスタンスにインストールされているセマンティック言語統計データベースの詳細については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] カタログビューの [Fulltext_semantic_language_statistics_database &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)に対してクエリを実行します。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 CONTROL SERVER 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、 **sp_fulltext_semantic_register_language_statistics_db**を呼び出して、セマンティック言語統計データベースを登録する方法を示します。  
  
```sql  
EXEC sp_fulltext_semantic_register_language_statistics_db @dbname = 'semanticsDb';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
