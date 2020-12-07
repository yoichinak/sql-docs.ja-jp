---
description: SET OFFSETS (Transact-SQL)
title: SET OFFSETS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET_OFFSETS_TSQL
- OFFSETS_TSQL
- SET OFFSETS
- OFFSETS
dev_langs:
- TSQL
helpviewer_keywords:
- position relative to start of statement [SQL Server]
- OFFSETS option
- offsets [SQL Server]
- SET OFFSETS statement
ms.assetid: c7bcc697-0930-4630-acae-d8ccbfa4414c
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8accd5a69be5182b0828eefcf8ac7f41e1ce0caf
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544127"
---
# <a name="set-offsets-transact-sql"></a>SET OFFSETS (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメント内の指定したキーワードのオフセット (ステートメントの先頭からの相対的な位置) を、DB-Library アプリケーションに返します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
 
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
  
SET OFFSETS keyword_list { ON | OFF }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *keyword_list*  
 SELECT、FROM、ORDER、TABLE、PROCEDURE、STATEMENT、PARAM、EXECUTE などの [!INCLUDE[tsql](../../includes/tsql-md.md)] 構成要素をコンマで区切って指定します。  
  
## <a name="remarks"></a>解説  
 SET OFFSETS は DB-Library アプリケーションだけで使用されます。  
  
 SET OFFSETS は、実行時ではなく、解析時に設定されます。 解析時に設定されるということは、SET ステートメントがバッチまたはストアド プロシージャ内に指定されている場合、コードが実際にその場所まで実行されるかどうかに関係なく、設定が有効になることを意味します。つまり他のどのステートメントが実行されるよりも前に、SET ステートメントが効力を発するということになります。 たとえば、絶対に実行されることのない IF...ELSE ステートメント ブロックに SET ステートメントが指定されていたとしても、IF...ELSE ステートメント ブロックは解析されるので、SET ステートメントは有効になります。  
  
 SET OFFSETS がストアド プロシージャで設定された場合、SET OFFSETS の値は、制御がストアド プロシージャから返された後、元に戻されます。 したがって、動的 SQL に指定されている SET OFFSETS ステートメントは、動的 SQL ステートメントの後にあるステートメントにまったく影響しません。  
  
 OFFSETS オプションが ON でエラーがない場合は、SET PARSEONLY はオフセットを返します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="see-also"></a>参照  
 [SET ステートメント &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET PARSEONLY &#40;Transact-SQL&#41;](../../t-sql/statements/set-parseonly-transact-sql.md)  
  
  
