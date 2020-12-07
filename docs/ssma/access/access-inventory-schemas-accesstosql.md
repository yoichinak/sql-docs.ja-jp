---
description: インベントリスキーマへのアクセス (アクセスアクセス Sql)
title: インベントリスキーマにアクセスする (アクセス可能 Sql) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- columns table
- databases table
- exported metadata
- exporting, schemas of exported metadata
- foreign keys table
- forms table
- indexes, table
- inventory schemas
- macros table
- modules table
- queries table
- reference, inventory schemas
- reports table
- schemas of exported metadata
- schemas, exported metadata
- SSMA_Access_InventoryColumns
- SSMA_Access_InventoryDatabases
- SSMA_Access_InventoryForeignKeys
- SSMA_Access_InventoryForms
- SSMA_Access_InventoryIndexes
- SSMA_Access_InventoryMacros
- SSMA_Access_InventoryModules
- SSMA_Access_InventoryQueries
- SSMA_Access_InventoryReports
- SSMA_Access_InventoryTables
- tables, inventory
ms.assetid: fdd3cff2-4d62-4395-8acf-71ea8f17f524
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 593c36c193b95d1484f3d478018992ea130d5417
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418638"
---
# <a name="access-inventory-schemas-accesstosql"></a>インベントリスキーマへのアクセス (アクセスアクセス Sql)
次のセクションでは、にアクセススキーマをエクスポートするときに SSMA によって作成されるテーブルについて説明し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="databases"></a>データベース  
データベースメタデータは **SSMA_Access_InventoryDatabases** テーブルにエクスポートされます。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|各データベースを一意に識別する GUID。 この列は、テーブルの主キーでもあります。|  
|**DatabaseName**|**nvarchar (4000)**|Access データベースの名前。|  
|**ExportTime**|**datetime**|このメタデータが SSMA によって作成された日付と時刻。|  
|**FilePath**|**nvarchar (4000)**|Access データベースの完全なパスとファイル名です。|  
|**FileSize**|**bigint**|Access データベースのサイズ (KB 単位)。|  
|**FileOwner**|**nvarchar (4000)**|Access データベースの所有者として指定されている Windows アカウント。|  
|**DateCreated**|**datetime**|Access データベースが作成された日付と時刻。|  
|**DateModified**|**datetime**|Access データベースが最後に変更された日付と時刻。|  
|**各行数**|**int**|Access データベース内のテーブルの数。|  
|**QueriesCount**|**int**|Access データベース内のクエリの数。|  
|**フォーム数**|**int**|Access データベース内のフォームの数。|  
|**モジュール数**|**int**|Access データベース内のモジュールの数。|  
|**レポート数**|**int**|Access データベース内のレポートの数。|  
|**MacrosCount**|**int**|Access データベース内のマクロの数。|  
|**AccessVersion**|**nvarchar (4000)**|データベースのアクセスバージョン。|  
|**Collation**|**nvarchar (4000)**|Access データベースの照合順序です。 照合順序は、データベースが文字列の並べ替えと比較を行う方法を決定します。|  
|**JetVersion**|**nvarchar (4000)**|Jet データベースエンジンのバージョンです。 データベースにアクセスするには、基になる Jet データベースエンジンを使用します。|  
|**Isupable**|**bit**|データベースを更新できるかどうかを示します。 値が1の場合、データベースは更新可能です。 値が0の場合、データベースは読み取り専用です。|  
|**QueryTimeout**|**int**|データベースの構成済み ODBC クエリタイムアウト値 (秒単位)。 既定値は 60 秒です。|  
  
## <a name="tables"></a>テーブル  
テーブルのメタデータが **SSMA_Access_InventoryTables** テーブルにエクスポートされます。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|このテーブルを含むデータベースを識別します。|  
|**TableId**|**uniqueidentifier**|テーブルを一意に識別する GUID。 この列は、テーブルの主キーでもあります。|  
|**TableName**|**nvarchar (4000)**|テーブルの名前。|  
|**RowsCount**|**int**|表の行数。|  
|**ValidationRule**|**nvarchar (4000)**|テーブルの有効な入力を定義するルール。 検証規則が存在しない場合、フィールドには空の文字列が含まれます。|  
|**LinkedTable**|**nvarchar (4000)**|テーブルにリンクされている別のテーブル (存在する場合)。 テーブルをリンクすると、このテーブルを使用して、他のテーブルの追加、削除、および更新を行うことができます。|  
|**ExternalSource**|**nvarchar (4000)**|テーブルに関連付けられているデータソース (存在する場合)。 テーブルがリンクされている場合、このフィールドには外部データソースが指定されています。|  
  
## <a name="columns"></a>[列]  
列のメタデータが **SSMA_Access_InventoryColumns** テーブルにエクスポートされます。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|この列を含むデータベースを識別します。|  
|**TableId**|**uniqueidentifier**|この列を含むテーブルを識別します。|  
|**ColumnId**|**int**|列を識別するインクリメント整数。 **ColumnId** は、テーブルの主キーです。|  
|**[ColumnName]**|**nvarchar (4000)**|列の名前。|  
|**IsNullable**|**bit**|列に null 値を含めることができるかどうかを指定します。 値が1の場合、列に null 値を含めることができます。 値が0の場合、列に null 値を含めることはできません。 検証規則は、null 値を防ぐためにも使用できます。|  
|**DataType**|**nvarchar (4000)**|**Text**や**Long**など、列のアクセスデータ型。|  
|**IsAutoIncrement**|**bit**|列が自動的に整数値をインクリメントするかどうかを指定します。 値が1の場合、整数は自動的にインクリメントされます。|  
|**Ordinal**|**smallint**|テーブル内の列の順序。0から始まります。|  
|**既定**|**nvarchar (4000)**|列の既定値。|  
|**ValidationRule**|**nvarchar (4000)**|列に追加または更新されたデータの検証に使用されるルール。|  
  
## <a name="indexes"></a>インデックス  
インデックスメタデータは **SSMA_Access_InventoryIndexes** テーブルにエクスポートされます。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|このインデックスを含むデータベースを識別します。|  
|**TableId**|**uniqueidentifier**|このインデックスを含むテーブルを識別します。|  
|**IndexId**|**int**|インデックスを識別するインクリメント整数。 この列は、テーブルの主キーです。|  
|**IndexName**|**nvarchar (4000)**|インデックスの名前です。|  
|**含まれるコラム**|**nvarchar (4000)**|インデックスに含まれる列を一覧表示します。 列名はセミコロンで区切られます。|  
|**IsUnique**|**bit**|インデックス内の各項目が一意である必要があるかどうかを指定します。 複数列のインデックスでは、値の組み合わせは一意である必要があります。 値が1の場合、インデックスによって一意の値が適用されます。|  
|**IsPK**|**bit**|主キーの定義の一部として、インデックスが自動的に作成されたかどうかを指定します。|  
|**IsClustered**|**bit**|インデックスがクラスター化されているかどうかを指定します。 クラスター化インデックスは、データの物理ストレージを並べ替えます。 テーブルにはクラスター化インデックスを1つだけ含めることができます。|  
  
## <a name="foreign-keys"></a>外部キー  
外部キーのメタデータが **SSMA_Access_InventoryForeignKeys** テーブルにエクスポートされます。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|この外部キーを含むデータベースを識別します。|  
|**TableId**|**uniqueidentifier**|この外部キーを含むテーブルを識別します。|  
|**ForeignKeyId**|**int**|外部キーを識別するインクリメント整数。 この列は、テーブルの主キーです。|  
|**ForeignKeyName**|**nvarchar (4000)**|インデックスの名前です。|  
|**ReferencedTableId**|**uniqueidentifier**|ソース列を含むテーブルを識別します。|  
|**SourceColumns**|**nvarchar (4000)**|外部キー列の一覧を表示します。|  
|**ReferencedColumns**|**nvarchar (4000)**|外部キーによって参照される主キー列を一覧表示します。|  
|**IsCascadeForUpdate**|**bit**|主キーの値が更新された場合に、そのキー値を参照するすべての行も更新されることを指定します。|  
|**IsCascadeForDelete**|**bit**|主キーの値を削除すると、そのキー値を参照するすべての行も削除されることを指定します。|  
|**IsEnforced**|**bit**|Foreign key 制約を適用することを指定します。|  
  
## <a name="queries"></a>クエリ  
クエリメタデータは **SSMA_Access_InventoryQueries** テーブルにエクスポートされます。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|このクエリを含むデータベースを識別します。|  
|**QueryId**|**int**|クエリを識別するインクリメント整数。 この列は、テーブルの主キーです。|  
|**QueryName**|**nvarchar (4000)**|クエリ名を返します。|  
|**QueryText**|**nvarchar (4000)**|SQL クエリコード (SELECT ステートメントなど)。|  
|**IsUpdateable シリアライズ)**|**bit**|クエリを更新可能にするか、読み取り専用にするかを指定します。|  
|**QueryType**|**nvarchar (4000)**|**Select**や**SetOperation**など、クエリの種類を指定します。|  
|**ExternalSource**|**nvarchar (4000)**|クエリが外部データソースを参照している場合は、クエリによって使用される接続文字列です。|  
  
## <a name="forms"></a>フォーム  
フォームメタデータは **SSMA_Access_InventoryForms** テーブルにエクスポートされます。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|このフォームが格納されているデータベースを識別します。|  
|**FormId**|**int**|フォームを識別するインクリメント整数。 この列は、テーブルの主キーです。|  
|**FormName**|**nvarchar (4000)**|フォームの名前。|  
  
## <a name="macros"></a>[マクロ]  
マクロのメタデータが **SSMA_Access_InventoryMacros** テーブルにエクスポートされます。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|マクロを含むデータベースを識別します。|  
|**マクロ Id**|**int**|マクロを識別するインクリメント整数。 この列は、テーブルの主キーです。|  
|**マクロ**|**nvarchar (4000)**|マクロの名前。|  
  
## <a name="reports"></a>レポート  
レポートのメタデータが **SSMA_Access_InventoryReports** テーブルにエクスポートされます。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|レポートが格納されているデータベースを識別します。|  
|**ReportId**|**int**|レポートを識別するインクリメント整数。 この列は、テーブルの主キーです。|  
|**ReportName**|**nvarchar (4000)**|レポートの名前です。|  
  
## <a name="modules"></a>モジュール  
モジュールのメタデータは **SSMA_Access_InventoryModules** テーブルにエクスポートされます。 このテーブルには、次の列が含まれています。  
  
|列名|データ型|説明|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|モジュールを含むデータベースを識別します。|  
|**ModuleId**|**int**|モジュールを識別するインクリメント整数。 この列は、テーブルの主キーです。|  
|**ModuleName**|**nvarchar (4000)**|モジュールの名前です。|  
  
## <a name="see-also"></a>参照  
[Access インベントリのエクスポート](exporting-an-access-inventory-accesstosql.md)  
  
