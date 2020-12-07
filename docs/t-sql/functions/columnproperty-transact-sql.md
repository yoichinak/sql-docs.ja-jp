---
description: COLUMNPROPERTY (Transact-SQL)
title: COLUMNPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COLUMNPROPERTY
- COLUMNPROPERTY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column properties [SQL Server]
- parameters [SQL Server], properties
- COLUMNPROPERTY function
ms.assetid: 2408c264-6eca-4120-bb71-df043c7c2792
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a6cd108efb12e459c8114c6b65e344d06f403367
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128529"
---
# <a name="columnproperty-transact-sql"></a>COLUMNPROPERTY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

この関数は、列またはパラメーターの情報を返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```syntaxsql
COLUMNPROPERTY ( id , column , property )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
*id*  
テーブルまたはプロシージャの識別子 (ID) を含む[式](../../t-sql/language-elements/expressions-transact-sql.md)。
  
*column*  
列またはパラメーターの名前を含む式。
  
*property*  
*id* 引数の場合、*property* 引数は `COLUMNPROPERTY` 関数が返す情報の型を指定します。 *property* 引数は次のいずれかの値になります。
  
|値|説明|返される値|  
|---|---|---|
|**AllowsNull**|NULL 値を許可します。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**ColumnId**|**sys.columns.column_id** に対応する列の ID 値です。|列 ID<br /><br /> **注:** 複数の列に対してクエリを実行する場合、列の ID 値の順序にギャップが生じることがあります。|  
|**FullTextTypeColumn**|*column* のドキュメント型情報を保持する、テーブル内の TYPE COLUMN。|この関数の 2 番目のパラメーターとして渡される列名の式の、フルテキストの TYPE COLUMN の ID。|  
|**GeneratedAlwaysType**|システムによって生成された列の値です。 **sys.columns.generated_always_type** に対応します|**適用対象**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降。<br /><br /> 0: 常に生成されなかった<br /><br /> 1: 行の先頭として常に生成された<br /><br /> 2: 行の終わりに常に生成された|  
|**IsColumnSet**|列は列セットです。 詳細については、「 [列セットの使用](../../relational-databases/tables/use-column-sets.md)」を参照してください。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**IsComputed**|列は計算列です。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**IsCursorType**|プロシージャ パラメーターは CURSOR 型です。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**IsDeterministic**|列は決定的です。 このプロパティは、計算列およびビュー列にのみ適用されます。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力 (計算列またはビュー列ではありません)|  
|**IsFulltextIndexed**|列はフルテキスト インデックス作成用に登録されます。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**IsHidden**|システムによって生成された列の値です。 **sys.columns.is_hidden** に対応します|**適用対象**: [!INCLUDE[ssCurrentLong](../../includes/sscurrent-md.md)] 以降。<br /><br /> 0 = 非表示ではない<br /><br /> 1: 非表示|  
|**IsIdentity**|列で IDENTITY プロパティを使用します。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**IsIdNotForRepl**|列で IDENTITY_INSERT の設定が確認されます。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**IsIndexable**|列にインデックスを作成できます。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**IsOutParam**|プロシージャ パラメーターは出力パラメーターです。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**IsPrecise**|列は正確です。 このプロパティは、決定的な列に対してのみ適用されます。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力 (決定的な列ではありません)|  
|**IsRowGuidCol**|列は **uniqueidentifier** データ型であり、ROWGUIDCOL プロパティで定義されています。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**IsSparse**|列はスパース列です。 詳細については、「 [スパース列の使用](../../relational-databases/tables/use-sparse-columns.md)」を参照してください。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**IsSystemVerified**|[!INCLUDE[ssDE](../../includes/ssde-md.md)] では、列の決定性のプロパティと有効桁数のプロパティを確認できます。 このプロパティは、計算列およびビュー列にのみ適用されます。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**IsXmlIndexable**|XML 列は XML インデックスで使用できます。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**[精度]**|列またはパラメーターのデータ型の長さ。|指定した列のデータ型の長さ<br /><br /> -1: **xml** または大きい値の型<br /><br /> NULL: 無効な入力|  
|**スケール**|列またはパラメーターのデータ型のスケール。|スケール値<br /><br /> NULL: 無効な入力|  
|**StatisticalSemantics**|列でセマンティック インデックス作成が有効になっています。|1:TRUE<br /><br /> 0:FALSE|  
|**SystemDataAccess**|列は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のシステム カタログまたは仮想システム テーブルのデータにアクセスする関数から派生します。 このプロパティは、計算列およびビュー列にのみ適用されます。|1: TRUE (読み取り専用アクセス)<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**UserDataAccess**|列は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカル インスタンスに格納されている、ビュー テーブルおよび一時テーブルを含むユーザー テーブル内のデータにアクセスする関数から派生します。 このプロパティは、計算列およびビュー列にのみ適用されます。|1: TRUE (読み取り専用アクセス)<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
|**UsesAnsiTrim**|ANSI_PADDING はテーブルの作成時に ON に設定されました。 このプロパティは、**char** または **varchar** 型の列またはパラメーターにのみ適用されます。|1:TRUE<br /><br /> 0:FALSE<br /><br /> NULL: 無効な入力|  
  
## <a name="return-types"></a>戻り値の型
 **int**  
  
## <a name="exceptions"></a>例外  
エラーが発生した場合、または呼び出し元にオブジェクトの表示権限がない場合は、NULL が返されます。
  
ユーザーが所有しているか、または権限を与えられている、セキュリティ保護可能なリソースのメタデータのみを表示できます。 つまり、オブジェクトに対する適切な権限がユーザーに与えられていない場合、メタデータを生成する組み込み関数 (`COLUMNPROPERTY` など) が NULL を返す可能性があります。 詳細については、「[メタデータ表示の構成](../../relational-databases/security/metadata-visibility-configuration.md)」を参照してください。
  
## <a name="remarks"></a>解説  
列の決定的なプロパティを調べるときは、まず、その列が計算列であるかどうかをテストします。 計算列でない場合は、**IsDeterministic** 引数によって NULL が返されます。 計算列は、インデックス列として指定できます。
  
## <a name="examples"></a>例  
この例では、`LastName` 列の長さを返します。
  
```sql
USE AdventureWorks2012;  
GO  
SELECT COLUMNPROPERTY( OBJECT_ID('Person.Person'),'LastName','PRECISION')AS 'Column Length';  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
Column Length
-------------
50
```  
  
## <a name="see-also"></a>関連項目
[メタデータ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)  
[TYPEPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/typeproperty-transact-sql.md)
  
  
