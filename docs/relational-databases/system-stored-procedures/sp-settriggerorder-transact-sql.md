---
description: sp_settriggerorder (Transact-sql)
title: sp_settriggerorder (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_settriggerorder
- sp_settriggerorder_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_settriggerorder
ms.assetid: 8b75c906-7315-486c-bc59-293ef12078e8
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: da6cb44163370332968c32324086b27f673b3f69
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543066"
---
# <a name="sp_settriggerorder-transact-sql"></a>sp_settriggerorder (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  最初または最後に起動される AFTER トリガーを指定します。 最初と最後のトリガーの間で起動される AFTER トリガーは、任意の順序で実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_settriggerorder [ @triggername = ] '[ triggerschema. ] triggername'   
    , [ @order = ] 'value'   
    , [ @stmttype = ] 'statement_type'   
    [ , [ @namespace = ] { 'DATABASE' | 'SERVER' | NULL } ]  
```  
  
## <a name="arguments"></a>引数  
`[ @triggername = ] '[ _triggerschema.] _triggername'` 順序を設定または変更するトリガーの名前と、それが属するスキーマ (該当する場合) を指定します。 [_triggerschema_**.**]*トリガー* は **sysname**です。 名前がトリガーに対応していない場合、または名前が INSTEAD OF トリガーに対応している場合、プロシージャはエラーを返します。 *triggerschema* を DDL トリガーまたはログオントリガーに対して指定することはできません。  
  
`[ @order = ] 'value'` トリガーの新しい順序の設定です。 *値* は **varchar (10)** で、次のいずれかの値を指定できます。  
  
> [!IMPORTANT]  
>  **最初**のトリガーと**最後**のトリガーは、2つの異なるトリガーである必要があります。  
  
|[値]|説明|  
|-----------|-----------------|  
|**First**|トリガーは最初に起動されます。|  
|**Last**|最後にトリガーが起動されます。|  
|**なし**|トリガーは、定義されていない順序で発生します。|  
  
`[ @stmttype = ] 'statement_type'` トリガーを起動する SQL ステートメントを指定します。 *statement_type* は **varchar (50)** で、INSERT、UPDATE、DELETE、LOGON、または [!INCLUDE[tsql](../../includes/tsql-md.md)] [DDL イベント](../../relational-databases/triggers/ddl-events.md)に記載されている任意のステートメントイベントを指定できます。 イベントグループを指定することはできません。  
  
 トリガーは、そのステートメントの種類のトリガーとして定義されている場合にのみ、ステートメントの種類の **最初** のトリガーまたは **最後** のトリガーとして指定できます。 たとえば、 **tr1**が insert トリガーとして定義されている場合、トリガー **Tr1**をテーブル**T1**の insert に対して**最初**に指定できます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]INSERT トリガーとしてのみ定義されている**TR1**が UPDATE ステートメントの**最初**のトリガーまたは**最後**のトリガーとして設定されている場合、はエラーを返します。 詳細については、「解説」を参照してください。  
  
 ** \@ 名前空間 =** { **' データベース '**  |  **' サーバー '** |空白  
 *トリガー*が DDL トリガーである場合、 ** \@ 名前空間**は、*トリガー*がデータベーススコープとサーバースコープのどちらで作成されたかを指定します。 *トリガー*が logon トリガーの場合は、SERVER を指定する必要があります。 DDL トリガーのスコープの詳細については、「 [Ddl Triggers](../../relational-databases/triggers/ddl-triggers.md)」を参照してください。 指定されていない場合、または NULL が指定されている場合、 *トリガー* は DML トリガーです。  
  
* サーバーは、以降に適用さ [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] れます。
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) と 1 (失敗)  
  
## <a name="remarks"></a>解説  
  
## <a name="dml-triggers"></a>DML トリガー  
 1つのテーブルに対して、ステートメントごとに1つの **最初** と **最後** のトリガーを1つだけ指定できます。  
  
 テーブル、データベース、またはサーバーで**最初**のトリガーが既に定義されている場合は、同じ*statement_type*に対して同じテーブル、データベース、またはサーバーに対して新しいトリガーを**最初**に指定することはできません。 この制限は、 **最後** のトリガーにも適用されます。  
  
 レプリケーションは、テーブルが即時更新サブスクリプションまたはキュー更新サブスクリプションに含まれる場合、自動的に最初のトリガーを生成します。 レプリケーションのトリガーは最初のトリガーであることが必要です。 レプリケーションでは、最初のトリガーを持つテーブルを即時更新サブスクリプションまたはキュー更新サブスクリプションに含めるよう設定すると、エラーが発生します。 テーブルをサブスクリプションに含めた後、トリガーを最初のトリガーに設定すると、 **sp_settriggerorder** はエラーを返します。 レプリケーショントリガーで ALTER TRIGGER を使用した場合、または **sp_settriggerorder** を使用してレプリケーショントリガーを **最後** のトリガーまたは **なし** のトリガーに変更した場合、サブスクリプションは正しく機能しません。  
  
## <a name="ddl-triggers"></a>DDL トリガー  
 データベーススコープの DDL トリガーとサーバースコープを持つ DDL トリガーが同じイベントに存在する場合は、両方のトリガーを **最初** のトリガーまたは **最後** のトリガーとして指定できます。 ただし、サーバースコープのトリガーは常に最初に起動します。 一般に、同じイベントに存在する DDL トリガーの実行順序は次のとおりです。  
  
1.  **最初**にマークされたサーバーレベルのトリガー。  
  
2.  その他のサーバー レベル トリガー。  
  
3.  **Last**とマークされたサーバーレベルのトリガー。  
  
4.  **最初**にマークが付けられたデータベースレベルのトリガー。  
  
5.  その他のデータベース レベル トリガー。  
  
6.  **Last**とマークされたデータベースレベルのトリガー。  
  
## <a name="general-trigger-considerations"></a>トリガーについての留意事項  
 ALTER TRIGGER ステートメントによって最初または最後のトリガーが変更されると、トリガーに対して最初に設定された**属性または****最後**の属性が削除され、値は**None**に置き換えられます。 順序の値は **sp_settriggerorder**を使用してリセットする必要があります。  
  
 複数のステートメントの種類に対して、同じトリガーを最初または最後の順序として指定する必要がある場合は、ステートメントの種類ごとに **sp_settriggerorder** を実行する必要があります。 また、トリガーは、そのステートメントの種類に対して起動する **最初** または **最後** のトリガーとして指定する前に、ステートメントの種類に対して最初に定義する必要があります。  
  
## <a name="permissions"></a>アクセス許可  
 サーバースコープ (すべてのサーバーで作成) またはログオントリガーの DDL トリガーの順序を設定するには、CONTROL SERVER 権限が必要です。  
  
 (データベースで作成された) データベーススコープを持つ DDL トリガーの順序を設定するには、ALTER ANY DATABASE DDL TRIGGER 権限が必要です。  
  
 DML トリガーの順序を設定するには、そのトリガーが定義されているテーブルまたはビューに対する ALTER 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-setting-the-firing-order-for-a-dml-trigger"></a>A. DML トリガーの起動順序を設定する  
 次の例では、 `uSalesOrderHeader` テーブルで操作が行われた後に起動される最初のトリガーとして、トリガーを指定し `UPDATE` `Sales.SalesOrderHeader` ます。  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'Sales.uSalesOrderHeader', @order='First', @stmttype = 'UPDATE';  
```  
  
### <a name="b-setting-the-firing-order-for-a-ddl-trigger"></a>B. DDL トリガーの起動順序を設定する  
 次の例では、トリガー `ddlDatabaseTriggerLog` が、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースで `ALTER_TABLE` イベントの発生後、最初に起動されるトリガーとなるよう指定します。  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'ddlDatabaseTriggerLog', @order='First', @stmttype = 'ALTER_TABLE', @namespace = 'DATABASE';  
```  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
  
