---
description: データ型のシノニム (Transact-SQL)
title: データ型のシノニム (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- data types [SQL Server], synonyms
- alternate names [SQL Server]
- synonyms [SQL Server], data types
ms.assetid: 390eef67-1a49-4185-a971-e07765be9717
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f689cdae7253c43ca39c06dc09953c4db02d0def
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126292"
---
# <a name="data-type-synonyms-transact-sql"></a>データ型のシノニム (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

ISO との互換性を保つために、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にはデータ型のシノニムが用意されています。 次の表に、シノニム、およびシノニムがマップされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のシステム データ型を一覧表示します。
  
|シノニム|SQL Server システム データ型|  
|---|---|
|**Binary varying**|**varbinary**|  
|**char varying**|**varchar**|  
|**character**|**char**|  
|**character**|**char(1)**|  
|**character(**_n_**)**|**char(n)**|  
|**character varying(**_n_**)**|**varchar(n)**|  
|**Dec**|**decimal**|  
|**Double precision**|**float**|  
|**float**[**(**_n_**)**] for _n_ = 1-7|**real**|  
|**float**[**(**_n_**)**] for _n_ = 8-15|**float**|  
|**integer**|**int**|  
|**national character(**_n_**)**|**nchar(n)**|  
|**national char(**_n_**)**|**nchar(n)**|  
|**national character varying(**_n_**)**|**nvarchar(n)**|  
|**national char varying(**_n_**)**|**nvarchar(n)**|  
|**national text**|**ntext**|  
|**timestamp**|rowversion|  
  
データ型のシノニムは、データ定義言語 (DDL) ステートメントの中で、対応する基本データ型の名前の代わりに使用できます。 このようなステートメントには、CREATE TABLE、CREATE PROCEDURE、および DECLARE *\@variable* などがあります。 ただし、オブジェクトの作成後は、シノニムを確認できなくなります。 オブジェクトが作成されると、オブジェクトにはシノニムに関連付けられている基本データ型が割り当てられます。 オブジェクトを作成したステートメント内にシノニムが指定されたという記録は存在しません。
  
結果セット列や式など、元のオブジェクトから派生したオブジェクトには、基本データ型が割り当てられます。 元のオブジェクトまたは派生したオブジェクトを使用するすべてのメタデータ関数では、シノニムではなく、基本データ型が報告されます。

* **sp_help** やその他のシステム ストアド プロシージャなどのメタデータ操作
* 情報スキーマ ビュー
* テーブルまたは結果セット列のデータ型を報告するデータ アクセス API のメタデータ操作
  
たとえば、`national character varying` を指定して、テーブルを作成できます。
  
```sql
CREATE TABLE ExampleTable (PriKey int PRIMARY KEY, VarCharCol national character varying(10))  
```  
  
`VarCharCol` が **nvarchar(10)** データ型に割り当てられ、すべての後続のメタデータ関数では、列は **nvarchar(10)** 列として報告されます。 メタデータ関数は報告されませんとして、 **各国語文字 varying (10)** 列です。
  
## <a name="see-also"></a>関連項目
[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
