---
description: sys.sequences (Transact-SQL)
title: sys. シーケンス (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sequences_TSQL
- sys.sequences
- sequences
- sequences_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, sys. sequences catalog view
- sys.sequences catalog view
ms.assetid: 0e1b0e32-1cce-40f7-83c8-860ec660138a
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8dcd78028499875016828e31bd3386eaf23c85a4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550406"
---
# <a name="syssequences-transact-sql"></a>sys.sequences (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  データベース内のシーケンス オブジェクトごとに 1 行のデータを格納します。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|\<inherited columns>||は、すべての[列を継承します。](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)|  
|**start_value**|**NULL 以外の sql_variant**|シーケンスオブジェクトの開始値。 ALTER SEQUENCE を使用してシーケンス オブジェクトを再開するときに、この値から再開されます。 シーケンスオブジェクトは、 **start_value**ではなく、 **minimum_value**または**maximum_value**に進みます。|  
|**increment**|**NULL 以外の sql_variant**|生成された各値の後にシーケンスオブジェクトをインクリメントするために使用される値。|  
|**minimum_value**|**sql_variant NULL**|シーケンスオブジェクトによって生成できる最小値。 この値に達すると、シーケンスオブジェクトは、より多くの値を生成するときにエラーを返すか、または CYCLE オプションが指定されている場合に再起動します。 MINVALUE が指定されていない場合、この列は、シーケンスジェネレーターのデータ型でサポートされる最小値を返します。|  
|**maximum_value**|**sql_variant NULL**|シーケンスオブジェクトによって生成できる最大値。 この値に達すると、シーケンスオブジェクトは、より多くの値を生成しようとしたときにエラーを返すか、または CYCLE オプションが指定されている場合に再起動します。 MAXVALUE が指定されていない場合、この列は、シーケンス ジェネレーターのデータ型によってサポートされる最大値を返します。|  
|**is_cycling**|**bit NOT NULL**|シーケンス オブジェクトに対して NO CYCLE が指定されている場合は 0 を返し、CYCLE が指定されている場合は 1 を返します。|  
|**is_cached**|**bit NOT NULL**|シーケンスオブジェクトに対してキャッシュが指定されていない場合は0、CACHE が指定されている場合は1を返します。|  
|**cache_size**|**int NULL**|シーケンス オブジェクトの指定されたキャッシュ サイズを返します。 シーケンスが NO CACHE オプションを使用して作成されている場合、またはキャッシュ サイズを指定せずに CACHE が指定されている場合、この列には NULL が格納されます。 キャッシュ サイズとして指定された値がシーケンス オブジェクトで返すことができる値の最大数より大きい場合、取得不可能なキャッシュ サイズがそのまま表示されます。|  
|**system_type_id**|**tinyint NOT NULL**|シーケンスオブジェクトのデータ型のシステム型の ID。|  
|**user_type_id**|**int NOT NULL**|ユーザーによって定義された、シーケンスオブジェクトのデータ型の ID。|  
|**有効桁数 (precision)**|**tinyint NOT NULL**|データ型の最大有効桁数。|  
|**scale**|**tinyint NOT NULL**|型の小数点以下の最大桁数。 Scale は、ユーザーに完全なメタデータを提供するために、精度と共に返されます。 シーケンスオブジェクトでは、整数型のみが許可されているため、小数点以下桁数は常に0になります。|  
|**current_value**|**NULL 以外の sql_variant**|最後の値の義務。 つまり、NEXT VALUE FOR 関数の最後の実行から返された値、または **sp_sequence_get_range** プロシージャを実行した最後の値です。 シーケンスが使用されていない場合は、START の値を返します。|  
|**is_exhausted**|**bit NOT NULL**|0は、シーケンスからより多くの値を生成できることを示します。 1は、シーケンスオブジェクトが MAXVALUE パラメーターに達し、シーケンスが CYCLE に設定されていないことを示します。 NEXT VALUE FOR 関数は、ALTER SEQUENCE を使用してシーケンスが再起動されるまでエラーを返します。|  
|**last_used_value**|**sql_variant NULL**|[Next Value For](../../t-sql/functions/next-value-for-transact-sql.md)関数によって生成された最後の値を返します。 SQL Server 2017 以降に適用されます。|  
  
## <a name="permissions"></a>アクセス許可  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]以降のバージョンでは、カタログビューでのメタデータの表示は、ユーザーが所有しているか、ユーザーが権限を許可されている securables に制限されます。 詳細については、「 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [シーケンス番号](../../relational-databases/sequence-numbers/sequence-numbers.md)   
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [sp_sequence_get_range &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)  
  
  
