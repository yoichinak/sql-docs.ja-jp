---
description: sys.fulltext_semantic_languages (Transact-sql)
title: sys.fulltext_semantic_languages (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- fulltext_semantic_languages
- fulltext_semantic_languages_TSQL
- sys.fulltext_semantic_languages
- sys.fulltext_semantic_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_semantic_languages catalog view
ms.assetid: b42a85e6-1db9-4a22-8a70-014574c95198
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: a9225482581772618f6116e45c3cedb46a35c0ac
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99191463"
---
# <a name="sysfulltext_semantic_languages-transact-sql"></a>sys.fulltext_semantic_languages (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  統計モデルが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに登録されている各言語の行を返します。 言語モデルが登録されている場合、その言語はセマンティックインデックス作成に対して有効になります。  
  
 このカタログビューは [sys.fulltext_languages &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)に似ています。  
    
|列名|種類|説明|  
|-|-|-|   
|lcid|INT|言語の Microsoft Windows ロケール識別子 (LCID) です。|  
|name|sysname|はsys.sys言語のエイリアスの値 &#40;**lcid** の値に対応する [transact-sql&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md)か、数値の lcid の文字列形式です。|  
  
## <a name="general-remarks"></a>全般的な解説  
 詳細については、「 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)」を参照してください。  
  
## <a name="metadata"></a>Metadata  
 セマンティックインデックス作成をサポートするためにインストールされているセマンティック言語統計データベースの詳細については、カタログビューに対してクエリを実行 [sys.fulltext_semantic_language_statistics_database &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md)を参照してください。  
  
## <a name="security"></a>セキュリティ  
  
### <a name="permissions"></a>アクセス許可  
 カタログ ビューでのメタデータの表示が、ユーザーが所有しているかそのユーザーが権限を許可されている、セキュリティ保護可能なメタデータに制限されます。  
  
## <a name="examples"></a>例  
 次の例では、 **sys.fulltext_semantic_languages** に対してクエリを実行し、の現在のインスタンスのセマンティックインデックス作成に登録されているすべての言語モデルに関する情報を取得する方法を示し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
```  
SELECT * FROM sys.fulltext_semantic_languages;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [セマンティック検索のインストールと構成](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
