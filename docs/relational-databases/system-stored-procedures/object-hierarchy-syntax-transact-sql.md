---
description: オブジェクト階層の構文 (Transact-sql)
title: オブジェクト階層の構文 (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- objects [SQL Server], hierarchy syntax
ms.assetid: 7ed8df86-9fd2-4e09-96bc-5381fec85f65
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 81db44bae57dec8bb0298e872221998ac45e0a3a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542072"
---
# <a name="object-hierarchy-syntax-transact-sql"></a>オブジェクト階層の構文 (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Sp_OAGetProperty および sp_OASetProperty の *propertyname* パラメーターと、sp_OAMethod の *methodname* パラメーターでは、のオブジェクト階層構文がサポートされて [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] います。 この特別な構文を使用する場合、これらのパラメーターの一般的な形式は次のとおりです。  
  
## <a name="syntax"></a>構文  
  
```  
  
'TraversedObject.PropertyOrMethod'  
```  
  
## <a name="arguments"></a>引数  
 *TraversedObject*  
 は、ストアドプロシージャで指定された *objecttoken* の下にある、階層内の OLE オブジェクトです。 一連のコレクション、オブジェクト プロパティ、およびオブジェクトを返すメソッドを指定するには、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 構文を使用します。 系列内の各オブジェクト指定子は、ピリオド (.) で区切る必要があります。  
  
 一連の指定子の項目には、コレクション名を指定できます。 コレクションを指定するには、次の構文を使用します。  
  
 Collection ("*item*")  
  
 二重引用符 (") が必要です。 コレクションに [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 感嘆符 (!) 構文を使用することはできません。  
  
 *PropertyOrMethod*  
 *TraversedObject*のプロパティまたはメソッドの名前を指定します。  
  
 sp_OAGetProperty、sp_OASetProperty、または sp_OAMethod パラメーター (sp_OAMethod 出力パラメーターのサポートを含む) を使用して、すべてのインデックスまたはメソッド パラメーターを指定するには、次の構文を使用します。  
  
 *PropertyOrMethod*  
  
 すべてのインデックスまたはメソッド パラメーターをかっこで囲んで指定するには、次の構文を使用します。この場合、sp_OAGetProperty、sp_OASetProperty、または sp_OAMethod のすべてのインデックスまたはメソッド パラメーターは無視されます。  
  
 *Propertyormethod*([ *ParameterName*: =] "*パラメーター*" [,...])  
  
 二重引用符 (") が必要です。 すべての位置指定パラメーターを指定した後に、すべての名前付きパラメーターを指定する必要があります。  
  
## <a name="remarks"></a>解説  
 *TraversedObject*が指定されていない場合は、 *propertyormethod*が必要です。  
  
 *Propertyormethod*が指定されていない場合、 *TraversedObject*は OLE オートメーションストアドプロシージャからのオブジェクトトークン出力パラメーターとして返されます。 *Propertyormethod*が指定されている場合は、 *TraversedObject*のプロパティまたはメソッドが呼び出され、プロパティ値またはメソッドの戻り値が OLE オートメーションストアドプロシージャからの出力パラメーターとして返されます。  
  
 *TraversedObject*リスト内のいずれかの項目が OLE オブジェクトを返さない場合は、エラーが発生します。  
  
 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] OLE オブジェクト構文の詳細については、[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] のマニュアルを参照してください。  
  
 HRESULT のリターンコードの詳細については、「 [sp_OACreate &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-oacreate-transact-sql.md)」を参照してください。  
  
## <a name="examples"></a>例  
 SQL-DMO SQLServer オブジェクトを使用するオブジェクト階層構文の例を次に示します。  
  
```  
-- Get the AdventureWorks2012 Person.Address Table object.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address")',  
   @table OUT  
  
-- Get the Rows property of the AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAGetProperty @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").Rows',  
   @rows OUT  
  
-- Call the CheckTable method to validate the   
-- AdventureWorks2012 Person.Address table.  
EXEC @hr = sp_OAMethod @object,  
   'Databases("AdventureWorks2012").Tables("Person.Address").CheckTable',  
   @checkoutput OUT  
```  
  
## <a name="see-also"></a>参照  
 [OLE オートメーションのサンプルスクリプト](../../relational-databases/stored-procedures/ole-automation-sample-script.md)   
 [OLE オートメーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
  
  
