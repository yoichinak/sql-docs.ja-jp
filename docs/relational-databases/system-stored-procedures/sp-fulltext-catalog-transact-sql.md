---
description: sp_fulltext_catalog (Transact-sql)
title: sp_fulltext_catalog (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_catalog_TSQL
- sp_fulltext_catalog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_catalog
ms.assetid: e49b98e4-d1f1-42b2-b16f-eb2fc7aa1cf5
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: eb810e5130f04a7f55ac0e262ecfe6f11b784a98
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543422"
---
# <a name="sp_fulltext_catalog-transact-sql"></a>sp_fulltext_catalog (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  フルテキスト カタログの作成と削除、およびカタログのインデックス作成の開始と中止を行います。 各データベースに対して複数のフルテキストカタログを作成できます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに、[ [フルテキスト](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)カタログの作成]、[ [フルテキスト](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)カタログの変更]、および [ [フルテキスト](../../t-sql/statements/drop-fulltext-catalog-transact-sql.md) カタログの削除] を使用します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_fulltext_catalog [ @ftcat= ] 'fulltext_catalog_name' ,   
     [ @action= ] 'action'   
     [ , [ @path= ] 'root_directory' ]   
```  
  
## <a name="arguments"></a>引数  
`[ @ftcat = ] 'fulltext_catalog_name'` フルテキストカタログの名前を指定します。 カタログ名は、データベースごとに一意である必要があります。 *fulltext_catalog_name* は **sysname**です。  
  
`[ @action = ] 'action'` 実行するアクションを指定します。 *アクション* は **varchar (20)**,、これらの値のいずれかを指定することができます。  
  
> [!NOTE]  
>  必要に応じて、フルテキストカタログの作成、削除、変更を行うことができます。 複数のカタログで同時にスキーマを変更することは避けてください。 これらのアクションは、 **sp_fulltext_table** ストアドプロシージャを使用して実行できます。この方法をお勧めします。  
  
|[値]|説明|  
|-----------|-----------------|  
|**作成**|ファイルシステムに空の新しいフルテキストカタログを作成し、 *fulltext_catalog_name*と*root_directory*(存在する場合) を使用して、関連付けられた行を**sysfulltextcatalogs**に追加します。 *fulltext_catalog_name* は、データベース内で一意である必要があります。|  
|**」**|*Fulltext_catalog_name*を削除するには、ファイルシステムから削除し、関連付けられている行を**sysfulltextcatalogs**で削除します。 このカタログに1つ以上のテーブルのインデックスが含まれている場合、このアクションは失敗します。 **sp_fulltext_table** カタログからテーブルを削除するには、'*table_name*'、' drop ' を実行する必要があります。<br /><br /> カタログが存在しない場合、エラーが表示されます。|  
|**start_incremental**|*Fulltext_catalog_name*の増分作成を開始します。 カタログが存在しない場合、エラーが表示されます。 フルテキストインデックスの作成が既にアクティブになっている場合は、警告が表示されますが、作成操作は行われません。 増分作成では、フルテキストインデックスが作成されているテーブルに **timestamp** 列がある場合に限り、変更された行のみがフルテキストインデックスに対して取得されます。|  
|**start_full**|*Fulltext_catalog_name*の完全作成を開始します。 このフルテキストカタログに関連付けられているすべてのテーブルのすべての行は、インデックスが既に作成されている場合でも、フルテキストインデックス作成のために取得されます。|  
|**Stop**|*Fulltext_catalog_name*のインデックスの作成を停止します。 カタログが存在しない場合、エラーが表示されます。 インデックスの作成を既に中止している場合、警告は表示されません。|  
|**リビルド**|*Fulltext_catalog_name*を再構築します。 カタログの再構築では、既存のカタログが削除され、代わりに新しいカタログが作成されます。 フルテキスト インデックスの参照を持つすべてのテーブルが新しいカタログに関連付けられます。 再構築すると、データベース システム テーブル内のフルテキスト メタデータがリセットされます。<br /><br /> 変更の追跡が無効になっている場合、再構築しても、新しく作成されたフルテキストカタログの再作成は行われません。 この場合、再作成するには、 **start_full**または**start_incremental**アクションを使用して**sp_fulltext_catalog**を実行します。|  
  
`[ @path = ] 'root_directory'`**Create**アクションのルートディレクトリです (完全な物理パスではありません)。 *root_directory* は **nvarchar (100)** で、既定値は NULL です。これは、セットアップ時に指定された既定の場所を使用することを示します。 Mssql ディレクトリの Ftdata サブディレクトリです。たとえば、C:\Program ・ SQL Server\MSSQL13. のようになります。MSSQLSERVER\MSSQL\FTData. 指定されたルートディレクトリは、同じコンピューター上のドライブに存在し、ドライブ文字以外で構成されている必要があり、相対パスにすることはできません。 ネットワークドライブ、リムーバブルドライブ、フロッピーディスク、および UNC パスはサポートされていません。 フルテキストカタログは、のインスタンスに関連付けられているローカルハードドライブ上に作成する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
 ** \@ path**は*action*が**create**の場合にのみ有効です。 **Create** (**stop**、 **rebuild**など) 以外のアクションでは、 ** \@ パス**を NULL にするか、省略する必要があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスがクラスター内の仮想サーバーの場合、指定するカタログ ディレクトリは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソースが依存する共有ディスク ドライブ上にある必要があります。 @pathが指定されていない場合、既定のカタログディレクトリの場所は、仮想サーバーのインストール時に指定されたディレクトリ内の共有ディスクドライブに配置されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 **Start_full**アクションは、 *fulltext_catalog_name*にフルテキストデータの完全なスナップショットを作成するために使用されます。 **Start_incremental**アクションは、データベース内の変更された行のインデックスを再作成するために使用されます。 増分作成は、テーブルに **timestamp**型の列がある場合にのみ適用できます。 フルテキストカタログ内のテーブルに **timestamp**型の列が含まれていない場合、テーブルは完全作成を行います。  
  
 フルテキスト カタログおよびインデックス データは、フルテキスト カタログ ディレクトリに作成したファイルに格納されます。 フルテキストカタログディレクトリは、path に指定されたディレクトリのサブディレクトリとして作成されるか、 ** \@ path**が指定されていない** \@ 場合はサーバー**の既定のフルテキストカタログディレクトリに作成されます。 フルテキストカタログディレクトリの名前は、サーバー上で一意であることを保証するように構築されています。 このため、サーバー上のすべてのフルテキストカタログディレクトリは、同じパスを共有できます。  
  
## <a name="permissions"></a>アクセス許可  
 呼び出し元は、 **db_owner** ロールのメンバーである必要があります。 要求されたアクションに応じて、呼び出し元は、対象のフルテキストカタログに対する ALTER 権限または CONTROL 権限を拒否しないようにする必要があります ( **db_owner** )。  
  
## <a name="examples"></a>例  
  
### <a name="a-create-a-full-text-catalog"></a>A. フルテキスト カタログを作成する  
 次の例では、 **AdventureWorks2012**データベースに空のフルテキストカタログ**Cat_Desc**を作成します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'create';  
GO  
```  
  
### <a name="b-to-rebuild-a-full-text-catalog"></a>B. フルテキスト カタログを再構築するには  
 この例では、 **AdventureWorks2012**データベース内の既存のフルテキストカタログ**Cat_Desc**を再構築します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'rebuild';  
GO  
```  
  
### <a name="c-start-the-population-of-a-full-text-catalog"></a>C. フルテキストカタログの作成を開始します。  
 この例では、 **Cat_Desc** カタログの完全作成を開始します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'start_full';  
GO  
```  
  
### <a name="d-stop-the-population-of-a-full-text-catalog"></a>D. フルテキストカタログの作成を停止します。  
 この例では、 **Cat_Desc** カタログの作成を停止します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'stop';  
GO  
```  
  
### <a name="e-to-remove-a-full-text-catalog"></a>E. フルテキストカタログを削除するには  
 次の例では、 **Cat_Desc** カタログを削除します。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_catalog 'Cat_Desc', 'drop';  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [FULLTEXTCATALOGPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_database &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [sp_help_fulltext_catalogs_cursor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-cursor-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [フルテキスト検索](../../relational-databases/search/full-text-search.md)  
  
  
