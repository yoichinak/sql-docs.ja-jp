---
title: "HASHBYTES (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 07/29/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- HASHBYTES_TSQL
- HASHBYTES
dev_langs: TSQL
helpviewer_keywords:
- hash input
- HASHBYTES
ms.assetid: 0ea6a4d1-313e-4f70-b939-dd2cd570f6d6
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 63552f4b6fb61b3b24d4d670b9ea255d8e417699
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="hashbytes-transact-sql"></a>HASHBYTES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で入力の MD2、MD4、MD5、SHA、SHA1、または SHA2 ハッシュを返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
HASHBYTES ( '<algorithm>', { @input | 'input' } )  
  
<algorithm>::= MD2 | MD4 | MD5 | SHA | SHA1 | SHA2_256 | SHA2_512   
```  
  
## <a name="arguments"></a>引数  
 **'**\<algorithm>**'**  
 入力のハッシュに使用するハッシュ アルゴリズムを指定します。 これは必須の引数で、既定値はありません。 単一引用符で囲む必要があります。 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]以降で SHA2_256、および SHA2_512 以外のすべてのアルゴリズムが使用されなくなりました。 古いアルゴリズム(推奨しません)は引き続き動作しますが、deprecation イベントが発生します。  
  
 **@input**  
 ハッシュされるデータを含む変数を指定します。**@input** のデータ型は、**varchar**、**nvarchar**、または **varbinary** です。  
  
 **'** *input* **'**  
 ハッシュする文字またはバイナリ文字列に評価される式を指定します。  
  
 出力はアルゴリズムの標準に準拠します。MD2、MD4、および MD5 の場合は 128 ビット (16 バイト)、SHA および SHA1 の場合は 160 ビット (20 バイト)、SHA2_256 の場合は 256 ビット (32 バイト)、SHA2_512 の場合は 512 ビット (64 バイト) です。  
  
**適用範囲**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]から[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]およびそれ以前では、使用できる入力値は 8,000 バイトに制限されます。  
  
## <a name="return-value"></a>戻り値  
 **varbinary** (最大 8,000 バイト)  
  
## <a name="examples"></a>使用例  
  
### <a name="a-return-the-hash-of-a-variable"></a>A: が変数のハッシュを返す  
 次の例では、変数 `@HashThis` に格納されている **nvarchar** 型のデータの `SHA1` ハッシュを返します。  
  
```  
DECLARE @HashThis nvarchar(4000);  
SET @HashThis = CONVERT(nvarchar(4000),'dslfdkjLK85kldhnv$n000#knf');  
SELECT HASHBYTES('SHA1', @HashThis);  
  
```  
  
### <a name="b-return-the-hash-of-a-table-column"></a>B: は、テーブルの列のハッシュを返す  
 次の例では、`Test1` 表内の `c1` 列の値の SHA1 ハッシュを返します。  
  
```  
CREATE TABLE dbo.Test1 (c1 nvarchar(50));  
INSERT dbo.Test1 VALUES ('This is a test.');  
INSERT dbo.Test1 VALUES ('This is test 2.');  
SELECT HASHBYTES('SHA1', c1) FROM dbo.Test1;  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
-------------------------------------------  
0x0E7AAB0B4FF0FD2DFB4F0233E2EE7A26CD08F173  
0xF643A82F948DEFB922B12E50B950CEE130A934D6  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>参照  
 [暗号化アルゴリズムの選択](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  
