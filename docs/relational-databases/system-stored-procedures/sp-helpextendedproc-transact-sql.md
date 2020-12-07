---
description: sp_helpextendedproc (Transact-SQL)
title: sp_helpextendedproc (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpextendedproc
- sp_helpextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpextendedproc
ms.assetid: 7e1f017e-c898-4225-b375-6a73ef9aac7b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 12255797c4c9799e6e6ec3110dea58f4617142eb
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549677"
---
# <a name="sp_helpextendedproc-transact-sql"></a>sp_helpextendedproc (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在定義されている拡張ストアドプロシージャと、プロシージャ (関数) が属するダイナミックリンクライブラリ (DLL) の名前を報告します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [CLR 統合](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_helpextendedproc [ [@funcname = ] 'procedure' ]  
```  
  
## <a name="arguments"></a>引数  
`[ @funcname = ] 'procedure'` 情報を報告する拡張ストアドプロシージャの名前を指定します。 *プロシージャ* は **sysname**,、既定値は NULL です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|拡張ストアドプロシージャの名前。|  
|**dll**|**nvarchar (255)**|DLL の名前。|  
  
## <a name="remarks"></a>解説  
 *プロシージャ*を指定した場合は、指定した拡張ストアドプロシージャに対して**sp_helpextendedproc**レポートが作成されます。 このパラメーターが指定されていない場合、 **sp_helpextendedproc** は、すべての拡張ストアドプロシージャ名と各拡張ストアドプロシージャが属する DLL 名を返します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_helpextendedproc**を実行する権限は、 **public**に与えられます。  
  
## <a name="examples"></a>例  
  
### <a name="a-reporting-help-on-all-extended-stored-procedures"></a>A. すべての拡張ストアド プロシージャに関するヘルプをレポートする  
 次の例では、すべての拡張ストアド プロシージャについてレポートします。  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc;  
GO  
```  
  
### <a name="b-reporting-help-on-a-single-extended-stored-procedure"></a>B. 1つの拡張ストアドプロシージャに関するヘルプをレポートする  
 次の例では、拡張ストアドプロシージャに関するレポートを作成し `xp_cmdshell` ます。  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc xp_cmdshell;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_addextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
