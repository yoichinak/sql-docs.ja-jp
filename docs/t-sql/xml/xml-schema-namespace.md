---
description: xml_schema_namespace
title: xml_schema_namespace (Transact-SQL)
ms.custom: ''
ms.date: 07/27/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- xml_schema_namespace_TSQL
- xml_schema_namespace
dev_langs:
- TSQL
helpviewer_keywords:
- XML schema collections [SQL Server], reconstructing schemas
- xml_schema_namespace function
- reconstructing schemas
- schemas [SQL Server], XML
- schema collections [SQL Server], reconstructing schemas
ms.assetid: ee9873d8-dd3a-4bff-a10c-68bbadbdf1a6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c74b2b1f47c9e928d7c3028add043e539134828d
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/23/2020
ms.locfileid: "91112986"
---
# <a name="xml_schema_namespace"></a>xml_schema_namespace
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  指定された XML スキーマ コレクション内のすべてのスキーマまたは特定のスキーマを再構築します。 この関数は、 **xml** データ型のインスタンスを返します。  
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```syntaxsql
xml_schema_namespace( Relational_schema , XML_schema_collection_name , [ Namespace ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *Relational_schema*  
 リレーショナル スキーマ名。 *Relational_schema* は **sysname** です。  
  
 *XML_schema_collection_name*  
 再構築する XML スキーマ コレクションの名前を指定します。 *XML_schema_collection_name* は **sysname** です。  
  
 *Namespace*  
 再構築する XML スキーマの名前空間 URI です。 上限は 1,000 文字です。 名前空間 URI を指定しない場合、XML スキーマ コレクション全体が再構築されます。 *名前空間*は **nvarchar(4000)** です。  
  
## <a name="return-types"></a>戻り値の型  
 **xml**  
  
## <a name="remarks"></a>解説  
 [CREATE XML SCHEMA COLLECTION](../../t-sql/statements/create-xml-schema-collection-transact-sql.md) または [ALTER XML SCHEMA COLLECTION](../../t-sql/statements/alter-xml-schema-collection-transact-sql.md) を使用してデータベース内の XML スキーマ コンポーネントをインポートする場合、検証に使用されたスキーマの情報が保持されます。 したがって、再構築されたスキーマは、元のスキーマ ドキュメントとは構文的に同じにならない可能性があります。 特に、コメント、空白、注釈は失われ、暗黙的な型の情報が明示されます。 たとえば、\<xs:element name="e1" /> を \<xs:element name="e1" type="xs:anyType"/> にします。 また、名前空間プレフィックスは保持されません。  
  
 名前空間のパラメーターを指定した場合、結果のスキーマ ドキュメントにはその名前空間内のすべてのスキーマ コンポーネントの定義が含まれます。それらのコンポーネントが異なるスキーマ ドキュメントまたは DDL のステップ、あるいはその両方に追加された場合であっても、同様です。  
  
 この関数を使用して、XML スキーマ ドキュメントを **sys.sys** XML スキーマ コレクションから構築することはできません。  
  
## <a name="examples"></a>例  
 次の例では、XML スキーマ コレクション `ProductDescriptionSchemaCollection` を、`AdventureWorks` データベース内の運用リレーショナル スキーマから取得します。  
  
```sql
USE AdventureWorks;  
GO  
SELECT xml_schema_namespace(N'production',N'ProductDescriptionSchemaCollection');  
GO  
```  
  
## <a name="see-also"></a>参照  
 [格納されている XML スキーマ コレクションの表示](../../relational-databases/xml/view-a-stored-xml-schema-collection.md)   
 [XML スキーマ コレクション &#40;SQL Server&#41;](../../relational-databases/xml/xml-schema-collections-sql-server.md)  
  
  
