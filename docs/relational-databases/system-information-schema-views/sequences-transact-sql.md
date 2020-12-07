---
description: シーケンス (Transact-sql)
title: シーケンス (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 12/30/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SEQUENCES
- SEQUENCES_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SEQUENCES view
- INFORMATION_SCHEMA.SEQUENCES view
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7fa13582e155387bbe7b7122e0051d830be2261b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546336"
---
# <a name="sequences-transact-sql"></a>シーケンス (Transact-sql)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

現在のデータベースの現在のユーザーがアクセスできるシーケンスごとに1行のデータを返します。

これらのビューから情報を取得するには、 **INFORMATION_SCHEMA**の完全修飾名を指定し_ます。 view_name_。

|列名|データ型|説明|
|-----------------|---------------|-----------------|
|**SEQUENCE_CATALOG**|**nvarchar(128)**|シーケンスの修飾子|
|**SEQUENCE_SCHEMA**|**nvarchar (** 128) * *|シーケンスを含むスキーマの名前|
|**SEQUENCE_NAME**|**nvarchar(128)**|[シーケンス名]|
|**DATA_TYPE**|**nvarchar (** 128 **)**|Sequence データ型|
|**NUMERIC_PRECISION**|**tinyint**|シーケンスの有効桁数|
|**NUMERIC_PRECISION_RADIX**|**smallint**|数値データの概数、正確な数値データ、整数データ、または通貨データの有効桁数の基数。 その他の場合は NULL が返されます。|
|**NUMERIC_SCALE**|**int**|数値データの概数、正確な数値データ、整数データ、または通貨データの桁数。 その他の場合は NULL が返されます。|
|**START_VALUE**|**int**|シーケンス オブジェクトによって返される最初の値です。|
|**MINIMUM_VALUE**|**int**|シーケンスオブジェクトの境界。 新しいシーケンス オブジェクトの既定の最小値は、シーケンス オブジェクトのデータ型の最小値です。 これは、0 を tinyint データ型およびその他のすべてのデータ型の負の数。|
|**MAXIMUM_VALUE**|**int**|シーケンスオブジェクトの境界。 新しいシーケンス オブジェクトの既定の最大値は、シーケンス オブジェクトのデータ型の最大値です。|
|**許容**|**int**|NEXT VALUE FOR 関数を呼び出すたびに必要なシーケンス オブジェクトの値を増分 (負の場合は減少) させるのに使用される値。 増分値が負の値の場合はシーケンス オブジェクトは降順で、それ以外の場合は昇順です。 0 は増分として使用できません。 新しいシーケンス オブジェクトの既定の増分値は 1 です。
|**CYCLE_OPTION**|**int**|最小値または最大値を超過した場合に、シーケンス オブジェクトを最小値 (または降順シーケンス オブジェクトの最大値) から再起動するか、例外をスローするかを指定するプロパティ。 新しいシーケンス オブジェクトの既定のサイクル オプションは、NO CYCLE です。
|**DECLARED_DATA_TYPE**|**int**|ユーザー定義データ型のデータ型です。|
|**DECLARED_DATA_PRECISION**|**int**|ユーザー定義データ型の有効桁数です。|
|**DECLARED_NUJMERIC_SCALE**|**int**|ユーザー定義データ型の数値の小数点以下桁数です。|

**例** 次の例では、テストデータベースのスキーマに関する情報を返します。

```sql
SELECT * FROM test.INFORMATION_SCHEMA.SEQUENCES;
```

## <a name="see-also"></a>参照

- [情報スキーマビュー &#40;Transact-sql&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)
- [sys.sequences &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md)
