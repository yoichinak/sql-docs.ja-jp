---
description: SCOPE_IDENTITY (Transact-SQL)
title: SCOPE_IDENTITY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SCOPE_IDENTITY
- SCOPE_IDENTITY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identity columns [SQL Server], SCOPE_IDENTITY function
- SCOPE_IDENTITY function
- last-inserted identity values
- identity values [SQL Server], last-inserted
ms.assetid: eef24670-059b-4f10-91d4-a67bc1ed12ab
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: db39f526499581d105176fa7df6092b7b2edd567
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "91379937"
---
# <a name="scope_identity-transact-sql"></a>SCOPE_IDENTITY (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  同じスコープ内の ID 列に挿入された最後の ID 値を返します。 スコープは、ストアド プロシージャ、トリガー、関数、バッチのいずれかのモジュールです。 したがって、2 つのステートメントが同じストアド プロシージャ、関数、またはバッチ内にある場合、これらのステートメントのスコープは同じになります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql  
SCOPE_IDENTITY()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>戻り値の型
 **numeric(38,0)**  
  
## <a name="remarks"></a>解説  
 SCOPE_IDENTITY、IDENT_CURRENT、および @@IDENTITY は、ID 列に挿入された値を返すという点で似ています。  
  
 IDENT_CURRENT はスコープとセッションには限定されませんが、特定のテーブルに限定されます。 IDENT_CURRENT では、任意のセッションとスコープ内の特定のテーブルに対して生成された値が返されます。 詳しくは、「[IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)」をご覧ください。  
  
 SCOPE_IDENTITY と @@IDENTITY では、現在のセッション内の任意のテーブルで生成された最後の ID 値が返されます。 ただし、SCOPE_IDENTITY で返される値は、現在のスコープ内で挿入された値に限られます。@@IDENTITY の場合は、特定のスコープに限定されません。  
  
 たとえば、T1 と T2 の 2 つのテーブルがあるとし、INSERT トリガーが T1 で定義されているとします。 T1 に行が挿入されると、トリガーが起動し、T2 に行を挿入します。 このシナリオでは、T1 上での挿入と、トリガーの結果として得られる T2 上での挿入という、2 つのスコープがあります。  
  
 T1 と T2 の両方に ID 列がある場合、T1 上で INSERT ステートメントが終了すると、@@IDENTITY と SCOPE_IDENTITY によってそれぞれ異なる値が返されます。 @@IDENTITY では、現在のセッションの任意のスコープにおいて挿入された最後の ID 列の値が返されます。 これは、T2 で挿入された値です。 SCOPE_IDENTITY() では、T1 に挿入された IDENTITY 値が返されます。 これは、同じスコープ内で発生した最後の挿入です。 ID 列への INSERT ステートメントがスコープ内で発生する前に SCOPE_IDENTITY() 関数が呼び出された場合、この関数では NULL 値が返されます。  
  
 失敗したステートメントとトランザクションによって、テーブルに対する現在の ID が変更され、ID 列値に差異が生じる可能性があります。 ID 値がロールバックされることはありません。これは、テーブルに値を挿入するトランザクションがコミットされない場合でも同じです。 たとえば、INSERT ステートメントが IGNORE_DUP_KEY 違反のために失敗しても、テーブルの現在の ID 値は増分されます。  
  
## <a name="examples"></a>例  
  
### <a name="a-using-identity-and-scope_identity-with-triggers"></a>A. @@IDENTITY および SCOPE_IDENTITY をトリガーで使用する  
 次の例では、`TZ` と `TY` の 2 つのテーブルを作成し、`TZ` に INSERT トリガーを作成します。 テーブル `TZ` に行が挿入されると、トリガー (`Ztrig`) が起動し、`TY` に行が挿入されます。  
  
```sql  
USE tempdb;  
GO  
CREATE TABLE TZ (  
   Z_id  INT IDENTITY(1,1)PRIMARY KEY,  
   Z_name VARCHAR(20) NOT NULL);  
  
INSERT TZ  
   VALUES ('Lisa'),('Mike'),('Carla');  
  
SELECT * FROM TZ;  
```     
結果セット: 次に示すのはテーブル TZ の内容です。  
  
```  
Z_id   Z_name  
-------------  
1      Lisa  
2      Mike  
3      Carla  
```  
```sql 
CREATE TABLE TY (  
   Y_id  INT IDENTITY(100,5)PRIMARY KEY,  
   Y_name VARCHAR(20) NULL);  
  
INSERT TY (Y_name)  
   VALUES ('boathouse'), ('rocks'), ('elevator');  
  
SELECT * FROM TY;  
```   
結果セット: 次に示すのは TY の内容です。  
```  
Y_id  Y_name  
---------------  
100   boathouse  
105   rocks  
110   elevator  
```  

行がテーブル TZ に挿入されるとテーブル TY に行を挿入するトリガーを作成します。  
```sql  
CREATE TRIGGER Ztrig  
ON TZ  
FOR INSERT AS   
   BEGIN  
   INSERT TY VALUES ('')  
   END;  
```  
トリガーを起動し、@@IDENTITY および SCOPE_IDENTITY 関数で取得した ID 値を確認します。   
```sql
INSERT TZ VALUES ('Rosalie');  
  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```
/*SCOPE_IDENTITY returns the last identity value in the same scope. This was the insert on table TZ.*/`  
SCOPE_IDENTITY  
4  

/*@@IDENTITY returns the last identity value inserted to TY by the trigger. 
  This fired because of an earlier insert on TZ.*/
@@IDENTITY  
115  
```  
  
### <a name="b-using-identity-and-scope_identity-with-replication"></a>B. @@IDENTITY および SCOPE_IDENTITY() をレプリケーションで使用する  
 次の例は、マージ レプリケーション用にパブリッシュされたデータベースへの挿入で、`@@IDENTITY` および `SCOPE_IDENTITY()` を使用する方法を示しています。 例のテーブルは両方とも [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] サンプル データベースにあります。`Person.ContactType` はパブリッシュされておらず、`Sales.Customer` はパブリッシュされています。 マージ レプリケーションでは、パブリッシュされたテーブルにトリガーを追加します。 このため、`@@IDENTITY` では、値をユーザー テーブルに挿入する代わりにレプリケーション システム テーブルに挿入して返すことができます。  
  
 `Person.ContactType` テーブルの ID の最大値は 20 です。 このテーブルに行を挿入する場合、`@@IDENTITY` と `SCOPE_IDENTITY()` は同じ値を返します。  
  
```sql  
USE AdventureWorks2012;  
GO  
INSERT INTO Person.ContactType ([Name]) VALUES ('Assistant to the Manager');  
GO  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
```  
SCOPE_IDENTITY  
21  
@@IDENTITY  
21
```  
  
 `Sales.Customer` テーブルの ID の最大値は 29483 です。 このテーブルに行を挿入する場合、`@@IDENTITY` と `SCOPE_IDENTITY()` は異なる値を返します。 `SCOPE_IDENTITY()` は値をユーザー テーブルに挿入して返すのに対し、`@@IDENTITY` は値をレプリケーション システム テーブルに挿入して返します。 挿入した ID 値にアクセスする必要があるアプリケーションには、`SCOPE_IDENTITY()` を使用してください。  
  
```sql  
INSERT INTO Sales.Customer ([TerritoryID],[PersonID]) VALUES (8,NULL);  
GO  
SELECT SCOPE_IDENTITY() AS [SCOPE_IDENTITY];  
GO  
SELECT @@IDENTITY AS [@@IDENTITY];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
 ```
 SCOPE_IDENTITY  
 29484  
 @@IDENTITY  
 89
 ```  
  
## <a name="see-also"></a>参照  
 [@@IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)  
  
  
