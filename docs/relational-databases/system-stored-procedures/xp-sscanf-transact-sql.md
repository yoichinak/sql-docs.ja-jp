---
description: xp_sscanf (Transact-sql)
title: xp_sscanf (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_sscanf_TSQL
- xp_sscanf
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sscanf
ms.assetid: 619a9df1-7008-407e-a75a-bc6f851454a8
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 53bf62fe03371b4406d5538f8ffe441e2f8970d6
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89525350"
---
# <a name="xp_sscanf-transact-sql"></a>xp_sscanf (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  文字列からのデータを、それぞれのフォーマット引数によって与えられる引数の位置に読み込みます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
xp_sscanf { string OUTPUT , format } [ ,argument [ ,...n ] ]   
```  
  
## <a name="arguments"></a>引数  
 **string**  
 引数の値を読み取る文字列を指定します。  
  
 OUTPUT  
 指定した場合、 *引数* の値が出力パラメーターに格納されます。  
  
 *format*  
 は、C 言語の **sscanf** 関数でサポートされているものに類似した書式設定された文字列です。 現在、% s 書式引数のみがサポートされています。  
  
 *argument*  
 **Varchar**変数は、対応する*format*引数の値に設定されます。  
  
 *n*  
 は、最大で50個の引数を指定できることを示すプレースホルダーです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 **xp_sscanf** は次のメッセージを返します。  
  
 `Command(s) completed successfully.`  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、`xp_sscanf` を使用して、ソース文字列のフォーマットにおけるそれぞれの位置に基づいて、ソース文字列から 2 つの値を抽出します。  
  
```  
DECLARE @filename varchar (20), @message varchar (20);  
EXEC xp_sscanf 'sync -b -fproducts10.tmp -rrandom', 'sync -b -f%s -r%s',   
  @filename OUTPUT, @message OUTPUT;  
SELECT @filename, @message;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------- --------------------   
products10.tmp        random  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;の一般的な拡張ストアドプロシージャ ](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_sprintf &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-sprintf-transact-sql.md)  
  
  
