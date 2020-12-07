---
description: SESSIONPROPERTY (Transact-SQL)
title: SESSIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SESSIONPROPERTY
- SESSIONPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, SESSIONPROPERTY function
- SESSIONPROPERTY function
- sessions [SQL Server], SET options settings
ms.assetid: 1f3730b4-1495-4d3a-af43-e57952812df9
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6c7c3133c15e10425af767d56d90a8d3a5b8277f
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2020
ms.locfileid: "91379347"
---
# <a name="sessionproperty-transact-sql"></a>SESSIONPROPERTY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  セッションの SET オプション設定を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
SESSIONPROPERTY (option)  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *オプション*  
 このセッションの現在のオプション設定値です。 *オプション* 値は次のいずれかを指定することができます。  
  
|オプション|説明|  
|------------|-----------------|  
|ANSI_NULLS|= (等号) と <> (不等号) を NULL 値に対して使用した場合の ISO 動作を指定します。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ANSI_PADDING|列に定義されているサイズよりも短い値を列に格納する方法と、値の後に文字とバイナリ データ型で空白が続いている値を列に格納する方法を指定します。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ANSI_WARNINGS|0 除算や算術オーバーフローなど、特定の状態に対するエラー メッセージまたは警告の出力について、ISO 標準の動作の適用を指定します。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|ARITHABORT|クエリ実行中にオーバーフロー エラーまたは 0 除算エラーが発生した場合に、クエリを終了するかどうかを決定します。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|CONCAT_NULL_YIELDS_ NULL|連結の結果が NULL として取り扱われるのか、空文字列として取り扱われるのかを制御します。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|NUMERIC_ROUNDABORT|式の丸め処理で精度が低下するときに、エラー メッセージや警告を生成するかどうかを指定します。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|QUOTED_IDENTIFIER|引用符を使用して、識別子とリテラル文字列を区切る方法に関して、ISO 規格に従うかどうかを指定します。<br /><br /> 1 = ON<br /><br /> 0 = OFF|  
|\<Any other string>|NULL = 入力は無効です。|  
  
## <a name="return-types"></a>戻り値の型  
 **sql_variant**  
  
## <a name="remarks"></a>解説  
 SET オプションは、サーバー レベル、データベース レベル、およびユーザー指定のオプションを組み合わせることによって表します。  
  
## <a name="examples"></a>例  
 次の例では、`CONCAT_NULL_YIELDS_NULL` オプションの設定を返します。  
  
```sql  
SELECT   SESSIONPROPERTY ('CONCAT_NULL_YIELDS_NULL')  
```  
  
## <a name="see-also"></a>参照  
 [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)   
 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)   
 [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  
