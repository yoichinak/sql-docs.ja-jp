---
description: sp_helptrigger (Transact-sql)
title: sp_helptrigger (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helptrigger
- sp_helptrigger_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helptrigger
ms.assetid: e486d39b-771d-488d-a786-7136433a2203
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5b7bf378b184a019c45fe20fac4dae8f995f7009
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543252"
---
# <a name="sp_helptrigger-transact-sql"></a>sp_helptrigger (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在のデータベースにある、指定したテーブルに定義されている DML トリガーの種類を返します。 sp_helptrigger は DDL トリガーでは使用できません。 代わりに、 [システムストアドプロシージャ](../../relational-databases/system-catalog-views/sys-triggers-transact-sql.md) カタログビューに対してクエリを実行します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helptrigger [ @tabname = ] 'table'   
     [ , [ @triggertype = ] 'type' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @tabname = ] 'table'` トリガー情報を返す現在のデータベース内のテーブルの名前を指定します。 *テーブル* は **nvarchar (776)**,、既定値はありません。  
  
`[ @triggertype = ] 'type'` 情報を返す DML トリガーの種類を示します。 *種類* は **char (6)**,、既定値は NULL の場合、これらの値のいずれかを指定できます。  
  
|[値]|説明|  
|-----------|-----------------|  
|**DELETE**|DELETE トリガー情報を返します。|  
|**INSERT**|挿入トリガー情報を返します。|  
|**UPDATE**|更新トリガー情報を返します。|  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 次の表に、結果セットに含まれる情報を示します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**trigger_name**|**sysname**|トリガーの名前。|  
|**trigger_owner**|**sysname**|トリガーが定義されたテーブルの所有者の名前。|  
|**isupdate**|**int**|1 = UPDATE トリガー<br /><br /> 0 = UPDATE トリガーではありません。|  
|**isdelete**|**int**|1 = DELETE トリガー<br /><br /> 0 = DELETE トリガーではありません。|  
|**isinsert**|**int**|1 = INSERT トリガー。<br /><br /> 0 = INSERT トリガー以外。|  
|**isafter**|**int**|1 = AFTER トリガー<br /><br /> 0 = AFTER トリガーではありません。|  
|**isinsteadof**|**int**|1 = INSTEAD OF トリガー<br /><br /> 0 = INSTEAD OF トリガー以外。|  
|**trigger_schema**|**sysname**|トリガーが属するスキーマの名前。|  
  
## <a name="permissions"></a>アクセス許可  
 テーブルに対する [メタデータ表示の構成](../../relational-databases/security/metadata-visibility-configuration.md) 権限が必要です。  
  
## <a name="examples"></a>例  
 次の例では、を実行し `sp_helptrigger` て、テーブルのトリガーに関する情報を生成し `Person.Person` ます。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_helptrigger 'Person.Person';  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
