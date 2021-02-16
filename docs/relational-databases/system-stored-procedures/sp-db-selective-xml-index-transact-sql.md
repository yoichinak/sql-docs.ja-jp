---
description: sp_db_selective_xml_index (Transact-sql)
title: sp_db_selective_xml_index (Transact-sql)
ms.custom: ''
ms.date: 02/11/2021
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: reference
f1_keywords:
- sp_db_selective_xml_index_TSQL
- sp_db_selective_xml_index
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_selective_xml_index procedure
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ed30d2b8df6141b308d32dee8f2fdcec0c2eceb1
ms.sourcegitcommit: c83c17e44b5e1e3e2a3b5933c2a1c4afb98eb772
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2021
ms.locfileid: "100525177"
---
# <a name="sp_db_selective_xml_index-transact-sql"></a>sp_db_selective_xml_index (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースに対して選択的 XML インデックス機能を有効または無効にします。 パラメーターを指定しないでストアド プロシージャを呼び出すと、選択的 XML インデックスが特定のデータベースで有効になっている場合は 1 が返されます。  

> [!NOTE]  
> 以降では [!INCLUDE[sssql14-md](../../includes/sssql14-md.md)] 、選択的 XML インデックス機能を無効にすることはできません。 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] で [!INCLUDE[sssql11-md](../../includes/sssql11-md.md)] は、このストアドプロシージャを使用して選択的 XML インデックス機能を無効にするには、 [ALTER Database SET オプション &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md) コマンドを使用して、データベースを単純復旧モデルに配置する必要があります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
  
      sys.sp_db_selective_xml_index[[ @dbname = ] 'dbname'],   
[[ @selective_xml_index = ] 'selective_xml_index']  
```  
  
## <a name="arguments"></a>引数  
`[ @ dbname = ] 'dbname'` 選択的 XML インデックスを有効または無効にするデータベースの名前。 *Dbname* が NULL の場合、現在のデータベースが想定されます。 *@dbname* は **sysname** です。


`[ @selective_xml_index = ] 'selective_xml_index'` インデックスを有効にするか無効にするかを決定します。 使用可能な値: ' on '、' off '、' true '、' false '。 ' On '、' true '、' off '、または ' false ' 以外の別の値が渡された場合は、エラーが発生します。 *@selective_xml_index* の型は **varchar (6)** です。

  
## <a name="return-code-values"></a>リターン コードの値  
 選択的 XML インデックスが特定のデータベースで有効になっている場合は **1** 、無効になっている場合は **0** です。  
  
## <a name="examples"></a>例  
  
### <a name="a-enable-selective-xml-index-functionality"></a>A. 選択的 XML インデックス機能を有効にする  
 次の例では、現在のデータベースに対して選択的 XML インデックスを有効にします。  
  
```sql
EXECUTE sys.sp_db_selective_xml_index  
    @dbname = NULL  
  , @selective_xml_index = N'on';  
GO  
```  
  
 次の例では、AdventureWorks2012 データベースで選択的 XML インデックスを有効にします。  
  
```sql
EXECUTE sys.sp_db_selective_xml_index  
    @dbname = N'AdventureWorks2012'  
  , @selective_xml_index = N'true';  
GO  
```  
  
### <a name="b-disable-selective-xml-index-functionality"></a>B. 選択的 XML インデックス機能を無効にする  
 次の例では、現在のデータベースで選択的 XML インデックスを無効にします。  
  
```sql
EXECUTE sys.sp_db_selective_xml_index  
    @dbname = NULL  
  , @selective_xml_index = N'off';  
GO  
```  
  
 次の例では、AdventureWorks2012 データベースに対して選択的 XML インデックスを無効にします。  
  
```sql
EXECUTE sys.sp_db_selective_xml_index  
    @dbname = N'AdventureWorks2012'  
  , @selective_xml_index = N'false';  
GO  
```  
  
### <a name="c-detect-if-selective-xml-index-is-enabled"></a>C. 選択的 XML インデックスが有効かどうかを検出します  
 次の例では、選択的 XML インデックスが有効になっているかどうかを検出します。 選択的 XML インデックスが有効になっている場合は1を返します。  
  
```sql
EXECUTE sys.sp_db_selective_xml_index;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [選択的 XML インデックス &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)  
   