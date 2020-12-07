---
description: REFERENTIAL_CONSTRAINTS (Transact-sql)
title: REFERENTIAL_CONSTRAINTS (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- REFERENTIAL_CONSTRAINTS
- REFERENTIAL_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS view
- REFERENTIAL_CONSTRAINTS view
ms.assetid: 5d358f18-0a85-4b55-af4b-98d5f4cd1020
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 42ebb05e1ec3bf70426cb0cef662623e2beb57f7
ms.sourcegitcommit: 968969b62bc158b9843aba5034c9d913519bc4a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/06/2020
ms.locfileid: "91753954"
---
# <a name="referential_constraints-transact-sql"></a>REFERENTIAL_CONSTRAINTS (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  現在のデータベース内の FOREIGN KEY 制約ごとに 1 行のデータを返します。 この情報スキーマビューでは、現在のユーザーがアクセス許可を持っているオブジェクトに関する情報が返されます。  
  
 これらのビューから情報を取得するには、INFORMATION_SCHEMA の完全修飾名を指定し **ます。**_view_name_。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|制約修飾子。|  
|**CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|制約を含むスキーマの名前。<br /><br /> **&#42;&#42; の重要な &#42;&#42;** オブジェクトのスキーマを決定するために INFORMATION_SCHEMA ビューを使用しないでください。 INFORMATION_SCHEMA ビューは、オブジェクトのメタデータのサブセットのみを表します。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**CONSTRAINT_NAME**|**sysname**|制約名。|  
|**UNIQUE_CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|UNIQUE 制約修飾子です。|  
|**UNIQUE_CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|UNIQUE 制約を含むスキーマの名前。<br /><br /> **&#42;&#42; の重要な &#42;&#42;** オブジェクトのスキーマを決定するために INFORMATION_SCHEMA ビューを使用しないでください。 INFORMATION_SCHEMA ビューは、オブジェクトのメタデータのサブセットのみを表します。 オブジェクトのスキーマを調べる唯一の信頼性のある方法は、sys.objects カタログ ビューに対するクエリを実行する方法です。|  
|**UNIQUE_CONSTRAINT_NAME**|**sysname**|UNIQUE 制約。|  
|**MATCH_OPTION**|**varchar (** 7 **)**|参照に関する制約の一致条件。 常に SIMPLE を返します。 これは、一致が定義されていないことを意味します。 次のいずれかに当てはまる場合には、条件は一致したと見なされます。<br /><br /> 外部キー列内の少なくとも 1 つの値が NULL である。<br /><br /> 外部キー列のすべての値が NULL ではなく、主キーテーブルに同じキーを持つ行があります。|  
|**UPDATE_RULE**|**varchar (** 11 **)**|ステートメントが、この制約で定義されている参照整合性に違反したときに実行されるアクション [!INCLUDE[tsql](../../includes/tsql-md.md)] です。 次のいずれかを返します。 <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> この制約の on UPDATE に対してアクションが指定されていない場合、制約で参照されている主キーの更新は外部キーに反映されません。 少なくとも 1 つの外部キーに同じ値が含まれるために、このような主キーの更新が参照整合性違反を引き起こす場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] による親テーブルと参照元テーブルへの変更は実行されません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] また、ではエラーが発生します。<br /><br /> この制約の ON UPDATE で CASCADE が指定されている場合は、主キーの値の変更が外部キーの値に自動的に反映されます。|  
|**DELETE_RULE**|**varchar (** 11 **)**|この制約によって定義される参照整合性に [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントが違反したときに実行されるアクションです。 次のいずれかを返します。 <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> この制約の on DELETE に対してアクションが指定されていない場合、制約内で参照される主キーの削除は外部キーに反映されません。 このような主キーを削除すると、参照整合性違反が発生します。これは、少なくとも1つの外部キーに同じ値が含まれているため [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です。では、親テーブルと参照元テーブルが変更されることはありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] また、ではエラーが発生します。<br /><br /> この制約の on DELETE で CASCADE が指定されている場合、主キーの値に対する変更は、外部キーの値に自動的に反映されます。|  
  
## <a name="see-also"></a>参照  
 [システムビュー &#40;Transact-sql&#41;](../../t-sql/language-reference.md)   
 [情報スキーマビュー &#40;Transact-sql&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.foreign_keys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
