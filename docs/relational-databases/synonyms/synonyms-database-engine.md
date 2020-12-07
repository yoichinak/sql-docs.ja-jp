---
description: シノニム (データベース エンジン)
title: シノニム (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- synonyms [SQL Server], about synonyms
ms.assetid: 6210e1d5-075f-47e4-ac8d-f84bcf26fbc0
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 74f5c5dcf2f2e1891daca22d70ebb9d9f1d9119f
ms.sourcegitcommit: a49a66dbda0cb16049e092b49c8318ac3865af3c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94983116"
---
# <a name="synonyms-database-engine"></a>シノニム (データベース エンジン)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  シノニムは、次の目的で機能するデータベース オブジェクトです。  
  
-   ベース オブジェクトと呼ばれる別のデータベース オブジェクトの代替名を提供します。ベース オブジェクトは、ローカル サーバーまたはリモート サーバーに配置できます。  
  
-   ベース オブジェクトの名前や場所に加えられた変更からクライアント アプリケーションを保護する抽象層を提供します。  
  
たとえば、 **Server1** という名前のサーバーに [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]の **Employee** テーブルがあるとします。 クライアント アプリケーションで、このテーブルを別のサーバー ( **Server2**) から参照するには、 **Server1.AdventureWorks.Person.Employee** という 4 部構成の名前を使用する必要があります。 また、テーブルの場所を別のサーバーなどに変更する場合は、その変更内容を反映してクライアント アプリケーションを変更する必要があります。  
  
このような問題の両方に対処するには、 **Server1** の **Employee** テーブルに対して、 **Server2** に **EmpTable** というシノニムを作成できます。 これで、クライアント アプリケーションから **Employee** テーブルを参照するときに、 **EmpTable** という 1 部構成の名前を使用するだけで済みます。 また、 **Employee** テーブルの場所が変更された場合は、 **Employee** テーブルの新しい場所を指すように、シノニムである **EmpTable** を変更する必要があります。 ALTER SYNONYM というステートメントは存在しないので、 **EmpTable** というシノニムをいったん削除してから、 **Employee** の新しい場所を指す同じ名前のシノニムを作成する必要があります。  
  
シノニムはスキーマに属しています。したがって、スキーマ内の他のオブジェクトと同様に、シノニムの名前は一意にする必要があります。 シノニムは、次のデータベース オブジェクトに対して作成できます。  

:::row:::
    :::column:::
        アセンブリ (CLR) ストアド プロシージャ

        アセンブリ (CLR) スカラー関数

        レプリケーション フィルター プロシージャ

        SQL スカラー関数

        SQL インライン テーブル値関数

        表示
    :::column-end:::
    :::column:::
        アセンブリ (CLR) テーブル値関数

        アセンブリ (CLR) 集計関数

        SQL テーブル値関数

        SQL ストアド プロシージャ

        テーブル* (ユーザー定義)
    :::column-end:::
:::row-end:::

*ローカル一時テーブルとグローバル一時テーブルが含まれます。  
  
> [!NOTE]  
> 4 部構成の関数ベース オブジェクト名はサポートされません。  
  
あるシノニムを別のシノニムのベース オブジェクトにすることはできません。また、シノニムからユーザー定義集計関数を参照することもできません。  
  
シノニムとベース オブジェクトとのバインドは、名前だけで行われます。 ベース オブジェクトの存在、種類、および権限のチェックは、すべて実行時まで行われません。 このため、ベース オブジェクトの変更や削除を行うことも、または削除してから元のベース オブジェクトと同じ名前の別のオブジェクトに置換することもできます。 たとえば、 **の** Person.Contact **テーブルを参照する** MyContacts [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]というシノニムがあるとします。 **Contact** テーブルを削除し、 **Person.Contact** というビューに置き換えると、 **MyContacts** は **Person.Contact** ビューを参照するようになります。  
  
シノニムへの参照は、スキーマにはバインドされていません。 したがって、シノニムはいつでも削除できます。 ただし、シノニムを削除することにより、削除されたシノニムへの参照が未解決の状態になる可能性があります。 このような参照は、実行時まで見つかりません。  
  
## <a name="synonyms-and-schemas"></a>シノニムとスキーマ  
所有者が自分ではない既定のスキーマのシノニムを作成する場合は、自分が所有しているスキーマ名でシノニム名を修飾する必要があります。 たとえば、 **x** というスキーマを所有していて、既定のスキーマが **y** だとします。この状況で CREATE SYNONYM ステートメントを使用する場合は、1 部構成の名前を使用してシノニムに名前を付けるのではなく、スキーマ **x** をシノニム名のプレフィックスにする必要があります。 シノニムの作成方法の詳細については、「 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)テーブルがあるとします。  
  
## <a name="granting-permissions-on-a-synonym"></a>シノニムに対する権限の許可  
シノニムに対する権限を許可できるのは、シノニムの所有者、 **db_owner**、または **db_ddladmin** のみです。  
  
次に示すシノニムに対する権限は、すべてまたはいくつかに `GRANT`、`DENY`、および `REVOKE` を行うことができます。  

:::row:::
    :::column:::
      CONTROL

      EXECUTE

      SELECT

      UPDATE
    :::column-end:::
    :::column:::
      DELETE

      INSERT

      TAKE OWNERSHIP

      VIEW DEFINITION
    :::column-end:::
:::row-end:::

## <a name="using-synonyms"></a>シノニムの使用  
 いくつかの SQL ステートメントや式のコンテキストでは、参照先のベース オブジェクトの代わりにシノニムを使用できます。 次の列に、これに該当するステートメントや式のコンテキストを示します。  

:::row:::
    :::column:::
        SELECT

        UPDATE

        EXECUTE
    :::column-end:::
    :::column:::
        INSERT

        DELETE

        副選択式
    :::column-end:::
:::row-end:::
 
 前に示したコンテキストでシノニムを扱っているときは、ベース オブジェクトが影響を受けます。 たとえば、シノニムが参照するベース オブジェクトがテーブルの場合に、シノニムに行を挿入すると、実際に参照先のテーブルに行が挿入されます。  
  
> [!NOTE]  
> リンク サーバー上のシノニムを参照することはできません。  
  
 OBJECT_ID 関数のパラメーターとしてシノニムを使用できます。ただし、この関数はベース オブジェクトではなく、シノニムのオブジェクト ID を返します。  
  
 DDL ステートメントでシノニムを参照することはできません。 たとえば、 `dbo.MyProduct`という名前のシノニムを参照する次のステートメントでは、エラーが生成されます。  
  
```sql  
ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null;  
EXEC ('ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null');  
```  
  
次の権限ステートメントは、シノニムのみに関連付けられ、ベース オブジェクトには影響しません。  

:::row:::
    :::column:::
        GRANT

        REVOKE
    :::column-end:::
    :::column:::
        DENY
    :::column-end:::
:::row-end:::

シノニムはスキーマ バインド オブジェクトではないので、次のスキーマ バインド式コンテキストからは参照できません。  

:::row:::
    :::column:::
        CHECK 制約

        既定式

        スキーマ バインド ビュー
    :::column-end:::
    :::column:::
        計算列

        ルール式

        スキーマ バインド関数
    :::column-end:::
:::row-end:::
  
スキーマ バインド関数の詳細については、「[ユーザー定義関数の作成 &#40;データベース エンジン&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)」を参照してください。  
  
## <a name="getting-information-about-synonyms"></a>シノニムに関する情報の取得  
`sys.synonyms` カタログ ビューには、特定のデータベースの各シノニムを表すエントリが含まれています。 シノニム名やベース オブジェクト名など、シノニムのメタデータがこのカタログ ビューに表示されます。 詳細については、「[sys.synonyms &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md)」を参照してください。  
  
拡張プロパティを使用すれば、説明用テキスト、指示テキスト、定型入力、および表記規則をシノニムのプロパティとして追加できます。 プロパティはデータベースに格納されるので、プロパティを読み取るアプリケーションはすべて、同じ方法でオブジェクトを評価できます。 詳細については、「[sp_addextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)」を参照してください。  
  
シノニムのベース オブジェクトの基本データ型を調べるには、OBJECTPROPERTYEX 関数を使用します。 詳細については、「[OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)」を参照してください。  
  
### <a name="examples"></a>例  
次の例は、ローカル オブジェクトであるシノニムのベース オブジェクトの基本データ型を返します。  
  
```sql  
USE tempdb;  
GO  
CREATE SYNONYM MyEmployee   
FOR AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyEmployee'), 'BaseType') AS BaseType;  
```  
  
次の例は、 `Server1`というサーバー上のリモート オブジェクトであるシノニムのベース オブジェクトの基本データ型を返します。  
  
```sql  
EXECUTE sp_addlinkedserver Server1;  
GO  
CREATE SYNONYM MyRemoteEmployee  
FOR Server1.AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyRemoteEmployee'), 'BaseType') AS BaseType;  
GO  
```  
  
## <a name="related-content"></a>関連コンテンツ  
 [シノニムの作成](../../relational-databases/synonyms/create-synonyms.md)    
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)    
 [DROP SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/drop-synonym-transact-sql.md)    
  
