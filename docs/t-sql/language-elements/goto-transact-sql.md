---
description: GOTO (Transact-SQL)
title: GOTO (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- GOTO
- GOTO_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- skipping statements
- Transact-SQL statements, skipping
- labels [SQL Server]
- statements [SQL Server], skipping
- GOTO statement
ms.assetid: 589b6f8e-dc80-416f-9e74-48bed5337f58
author: cawrites
ms.author: chadam
ms.openlocfilehash: 4653639f9e83ebc8d9e3fa727b8f966555aeadfa
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99115014"
---
# <a name="goto-transact-sql"></a>GOTO (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  実行の流れを指定のラベルに分岐します。 GOTO の後の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントはスキップされ、処理はそのラベルから続行されます。 GOTO ステートメントとラベルは、プロシージャ、バッチ、またはステートメント ブロック内のどこででも使用できます。 GOTO ステートメントは入れ子にすることができます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
Define the label:   
label:   
Alter the execution:  
GOTO label   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *label*  
 GOTO によりラベルを指定した場合、そのラベルが以降の処理を開始する位置になります。 ラベルは、[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従う必要があります。 GOTO の使用の有無にかかわらず、ラベルをコメント行として使用することができます。  
  
## <a name="remarks"></a>解説  
 GOTO は、条件付きフロー制御ステートメント、ステートメント ブロック、またはプロシージャ内に存在できますが、バッチの外にあるラベルに移動できません。 GOTO による分岐は、GOTO の前後に定義されたラベルに移動できます。  
  
## <a name="permissions"></a>アクセス許可  
 GOTO 権限は、特に指定のない限りすべての有効なユーザーに与えられます。  
  
## <a name="examples"></a>例  
 次の例では、`GOTO` を分岐手段として使用する方法を示します。  
  
```  
DECLARE @Counter int;  
SET @Counter = 1;  
WHILE @Counter < 10  
BEGIN   
    SELECT @Counter  
    SET @Counter = @Counter + 1  
    IF @Counter = 4 GOTO Branch_One --Jumps to the first branch.  
    IF @Counter = 5 GOTO Branch_Two  --This will never execute.  
END  
Branch_One:  
    SELECT 'Jumping To Branch One.'  
    GOTO Branch_Three; --This will prevent Branch_Two from executing.  
Branch_Two:  
    SELECT 'Jumping To Branch Two.'  
Branch_Three:  
    SELECT 'Jumping To Branch Three.';  
```  
  
## <a name="see-also"></a>参照  
 [フロー制御言語 &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [BEGIN...END &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-end-transact-sql.md)   
 [BREAK &#40;Transact-SQL&#41;](../../t-sql/language-elements/break-transact-sql.md)   
 [CONTINUE &#40;Transact-SQL&#41;](../../t-sql/language-elements/continue-transact-sql.md)   
 [IF...ELSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/if-else-transact-sql.md)   
 [WAITFOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/waitfor-transact-sql.md)   
 [WHILE &#40;Transact-SQL&#41;](../../t-sql/language-elements/while-transact-sql.md)  
  
  
