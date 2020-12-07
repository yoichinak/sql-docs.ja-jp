---
description: sp_OAGetProperty (Transact-SQL)
title: sp_OAGetProperty (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAGetProperty_TSQL
- sp_OAGetProperty
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAGetProperty
ms.assetid: 240eeeb9-6d8b-4930-b912-1d273ca0ab38
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ad769910b74dafd2727719980c6070d9487094da
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545995"
---
# <a name="sp_oagetproperty-transact-sql"></a>sp_OAGetProperty (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  OLE オブジェクトのプロパティ値を取得します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_OAGetProperty objecttoken , propertyname   
    [ , propertyvalue OUTPUT ]  
    [ , index...]   
```  
  
## <a name="arguments"></a>引数  
 *objecttoken*  
 以前に **sp_OACreate**を使用して作成された OLE オブジェクトのオブジェクトトークンです。  
  
 *propertyname*  
 返される OLE オブジェクトのプロパティ名を指定します。  
  
 *propertyvalue*の **出力**  
 返されるプロパティ値を指定します。 指定する場合は、適切なデータ型のローカル変数でなければなりません。  
  
 プロパティが OLE オブジェクトを返す場合、 *propertyvalue* は、データ型が **int**のローカル変数である必要があります。オブジェクトトークンはローカル変数に格納され、このオブジェクトトークンを他の OLE オートメーションストアドプロシージャと共に使用できます。  
  
 プロパティが単一の値を返す場合は、 *propertyvalue*のローカル変数を指定します。これにより、ローカル変数のプロパティ値が返されます。または、 *propertyvalue*を指定せずに、単一列の単一行の結果セットとしてクライアントにプロパティ値を返します。  
  
 プロパティが配列を返す場合、 *propertyvalue* を指定すると、NULL に設定されます。  
  
 *Propertyvalue*が指定されていても、プロパティが値を返さない場合は、エラーが発生します。 プロパティが3次元以上の配列を返す場合、エラーが発生します。  
  
 *インデックス*  
 はインデックスパラメーターです。 指定する場合、 *インデックス* は、適切なデータ型の値である必要があります。  
  
 一部のプロパティにはパラメーターがあります。 これらのプロパティはインデックス付きプロパティと呼ばれ、パラメーターはインデックスパラメーターと呼ばれます。 プロパティは、複数のインデックスパラメーターを持つことができます。  
  
> [!NOTE]  
>  このストアドプロシージャのパラメーターは、名前ではなく位置によって指定されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または0以外の数 (失敗)。これは、OLE オートメーションオブジェクトによって返される HRESULT の整数値です。  
  
 HRESULT のリターンコードの詳細については、「 [OLE オートメーションのリターンコードとエラー情報](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)」を参照してください。  
  
## <a name="result-sets"></a>結果セット  
 プロパティが 1 次元または 2 次元の配列を返す場合、配列は結果セットとしてクライアントに返されます。  
  
-   1 次元の配列の場合は、配列内の要素数と同数の列を持つ 1 行の結果セットとしてクライアントに返されます。 つまり、配列は列数として返されます。  
  
-   2 次元の配列の場合は、最初の次元の配列の要素数を列数とし、2 番目の次元の配列の要素数を行数とした結果セットとしてクライアントに返します。 つまり、配列は (columns, rows) として返されます。  
  
 プロパティの戻り値またはメソッドの戻り値が配列の場合、 **sp_OAGetProperty** または **sp_OAMethod** によって結果セットがクライアントに返されます。 メソッドの出力パラメーターを配列にすることはできません。これらのプロシージャは、配列内のすべてのデータ値をスキャンし、結果セットのそれぞれの列に使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の適切なデータ型とデータ長を決定します。 これらのプロシージャは必要なデータ型とデータ長を使用して、特定の列内のすべてのデータ値を表現します。  
  
 列内のすべてのデータ値が同じデータ型を共有する場合は、そのデータ型を列全体で使用します。 列のデータ値のデータ型が異なる場合、列全体のデータ型が次のグラフに基づいて選択されます。  
  
||INT|float|money|DATETIME|varchar|nvarchar|  
|------|---------|-----------|-----------|--------------|-------------|--------------|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="remarks"></a>解説  
 また、 **sp_OAMethod** を使用してプロパティ値を取得することもできます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールのメンバーシップ、またはこのストアドプロシージャに対して直接実行権限が必要です。 `Ole Automation Procedures` OLE オートメーションに関連するシステムプロシージャを使用するには、構成を **有効** にする必要があります。  
  
## <a name="examples"></a>例  
  
### <a name="a-using-a-local-variable"></a>A. ローカル変数を使用する  
 次の例では、 `HostName` (以前に作成した **SQLServer** オブジェクトの) プロパティを取得し、ローカル変数に格納します。  
  
```  
DECLARE @property varchar(255);  
EXEC @hr = sp_OAGetProperty @object, 'HostName', @property OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END  
PRINT @property;  
```  
  
### <a name="b-using-a-result-set"></a>B. 結果セットの使用  
 次の例では、 `HostName` (以前に作成した **SQLServer** オブジェクトの) プロパティを取得し、結果セットとしてクライアントに返します。  
  
```  
EXEC @hr = sp_OAGetProperty @object, 'HostName';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;の OLE オートメーションストアドプロシージャ ](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE オートメーションのサンプル スクリプト](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
