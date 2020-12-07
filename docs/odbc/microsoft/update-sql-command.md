---
description: UPDATE - SQL コマンド
title: UPDATE-SQL コマンド |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- update [ODBC]
ms.assetid: ff1e0331-c060-4304-b280-039725b45f63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6aa25f786448a14da47321c0f5ce1825716c03d2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471412"
---
# <a name="update---sql-command"></a>UPDATE - SQL コマンド
テーブル内のレコードを新しい値で更新します。  
  
 Visual FoxPro ODBC ドライバーでは、このコマンドのネイティブな Visual FoxPro 言語構文がサポートされています。 ドライバー固有の情報については、「 **ドライバーの解説**」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>引数  
 更新 [ *DatabaseName1!*] *TableName1*  
 レコードを新しい値で更新するテーブルを指定します。  
  
 *DatabaseName1!* テーブルを含むデータソースで指定されたデータベース以外のデータベースの名前を指定します。 データベースが現在のものではない場合は、テーブルを含むデータベースの名前を含める必要があります。 データベース名の後とテーブル名の前に、感嘆符 (!) の区切り記号を含めます。  
  
 SET *Column_Name1* =  *eExpression1*[, *Column_Name2* =  *eExpression2*  
 更新される列とその新しい値を指定します。 WHERE 句を省略した場合、列のすべての行が同じ値で更新されます。  
  
 WHERE *FilterCondition1*[および &#124; または *FilterCondition2*...]  
 新しい値で更新されるレコードを指定します。  
  
 *Filtercondition* は、レコードが新しい値で更新されるために満たす必要がある条件を指定します。 フィルター条件はいくつでも含めることができ、AND または OR 演算子を使用して接続できます。 また、NOT 演算子を使用して論理式の値を反転させることも、 **empty**() を使用して空のフィールドをチェックすることもできます。  
  
## <a name="remarks"></a>解説  
 UPDATE-SQL は、1つのテーブル内のレコードのみを更新できます。  
  
 REPLACE と異なり、UPDATE-SQL では、共有アクセス用に開かれたテーブル内の複数のレコードを更新するときにレコードロックが使用されます。 これにより、マルチユーザー環境でのレコードの競合が減少しますが、パフォーマンスが低下する可能性があります。 パフォーマンスを最大にするには、テーブルを排他的に使用するために開くか、 **FLOCK**() を使用してテーブルをロックします。  
  
## <a name="driver-remarks"></a>ドライバーの解説  
 アプリケーションが ODBC SQL ステートメントの更新をデータソースに送信すると、Visual FoxPro ODBC ドライバーは、コマンドを変換せずに Visual FoxProUPDATE コマンドに変換します。  
  
## <a name="see-also"></a>参照  
 [DELETE-SQL コマンド](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT - SQL コマンド](../../odbc/microsoft/insert-sql-command.md)
