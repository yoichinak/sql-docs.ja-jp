---
title: "sp_helplanguage (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helplanguage
- sp_helplanguage_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_helplanguage
- default languages
ms.assetid: 8c4651a5-7dbc-49c5-8691-dc72103c2dfa
caps.latest.revision: "19"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a94f66688ce53aef2dcf575d58e16ed6f2f1672b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/27/2017
---
# <a name="sphelplanguage-transact-sql"></a>sp_helplanguage (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] での特定の代替言語、またはすべての言語に関する情報を報告します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helplanguage [ [ @language = ] 'language' ]  
```  
  
## <a name="arguments"></a>引数  
 [  **@language=** ] **'***language***'**  
 情報を表示する代替言語の名前です。 *language* のデータ型は **sysname** で、既定値は NULL です。 *language* を指定した場合は、指定した言語に関する情報が返されます。 指定しない場合は、**sys.syslanguages** 互換性ビューにあるすべての言語に関する情報が返されます。  
  
## <a name="return-code-values"></a>戻り値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|Description|  
|-----------------|---------------|-----------------|  
|**langid**|**smallint**|言語 ID 番号です。|  
|**dateformat**|**nchar (3)**|日付の形式です。|  
|**datefirst**|**tinyint**|週の最初の曜日。1 は月曜、2 は火曜のようになり、7 は日曜になります。|  
|**upgrade**|**int**|この言語を使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の最新アップグレード バージョンです。|  
|**name**|**sysname**|言語名です。|  
|**alias**|**sysname**|言語の別名です。|  
|**months**|**nvarchar (372)**|月の名前です。|  
|**shortmonths**|**nvarchar (132)**|月の短縮名です。|  
|**days**|**nvarchar(217)**|曜日です。|  
|**lcid**|**int**|この言語を使用する Windows のロケール ID です。|  
|**msglangid**|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]メッセージ グループ ID です。|  
  
## <a name="permissions"></a>権限  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-returning-information-about-a-single-language"></a>A. 特定の言語に関する情報を返す  
 次の例では、代替言語 `French` に関する情報を表示します。  
  
```  
sp_helplanguage French;  
```  
  
### <a name="b-returning-information-about-all-languages"></a>B. すべての言語に関する情報を返す  
 次の例では、インストールされているすべての代替言語に関する情報を表示します。  
  
```  
sp_helplanguage;  
```  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [@@LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/functions/language-transact-sql.md)   
 [SET LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
