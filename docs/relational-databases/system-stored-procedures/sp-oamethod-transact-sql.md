---
description: sp_OAMethod (Transact-SQL)
title: sp_OAMethod (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAMethod
- sp_OAMethod_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAMethod
ms.assetid: 1dfaebe2-c7cf-4041-a586-5d04faf2e25e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7442e3af4bf0233e51f32d7c8e6f034d69598046
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89526961"
---
# <a name="sp_oamethod-transact-sql"></a>sp_OAMethod (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  OLE オブジェクトのメソッドを呼び出します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_OAMethod objecttoken , methodname  
    [ , returnvalue OUTPUT ]   
    [ , [ @parametername = ] parameter [ OUTPUT ] [ ...n ] ]   
```  
  
## <a name="arguments"></a>引数  
 *objecttoken*  
 以前に **sp_OACreate**を使用して作成された OLE オブジェクトのオブジェクトトークンです。  
  
 *methodname*  
 呼び出す OLE オブジェクトのメソッド名を指定します。  
  
 _戻り_  **結果の出力**  
 OLE オブジェクトのメソッドの戻り値です。 指定する場合は、適切なデータ型のローカル変数でなければなりません。  
  
 メソッドが単一の値を返す場合は、戻り *値のローカル*変数を指定します。これにより、ローカル変数のメソッドの戻り値が返されます。または、メソッドの戻り値を単一列の単一行の結果セットとしてクライアントに *返す戻り値を指定しない*でください。  
  
 メソッドの戻り値が OLE オブジェクトの場合、戻り値は、データ型が**int**のローカル変数で*ある必要が*あります。オブジェクトトークンはローカル変数に格納され、このオブジェクトトークンを他の OLE オートメーションストアドプロシージャと共に使用できます。  
  
 メソッドの戻り値が配列の場合、戻り値が指定され *ている場合* は NULL に設定されます。  
  
 次のいずれかが発生すると、エラーが発生します。  
  
-   *戻り値が指定* されていますが、メソッドは値を返しません。  
  
-   メソッドは、3次元以上の配列を返します。  
  
-   メソッドが出力パラメーターとして配列を返す場合  
  
`[ _@parametername = ] parameter[ OUTPUT ]` はメソッドパラメーターです。 指定する場合、 *パラメーター* は、適切なデータ型の値である必要があります。  
  
 出力パラメーターの戻り値を取得するには、 *パラメーター* を適切なデータ型のローカル変数にする必要があり、 **出力** を指定する必要があります。 定数パラメーターが指定されている場合、または **output** が指定されていない場合、出力パラメーターからの戻り値は無視されます。  
  
 指定する場合、 *parametername* は [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 名前付きパラメーターの名前である必要があります。 **@**_Parametername_is ローカル変数ではないことに注意 [!INCLUDE[tsql](../../includes/tsql-md.md)] してください。 アットマーク ( **@** ) は削除され、 *parametername*はパラメーター名として OLE オブジェクトに渡されます。 すべての位置指定パラメーターを指定した後に、すべての名前付きパラメーターを指定する必要があります。  
  
 *n*  
 複数のパラメーターを指定できることを示すプレースホルダーです。  
  
> [!NOTE]
>  * \@ parametername*は、指定されたメソッドの一部であり、オブジェクトに渡されるため、名前付きパラメーターにすることができます。 このストアドプロシージャの他のパラメーターは、名前ではなく位置によって指定されます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または0以外の数 (失敗)。これは、OLE オートメーションオブジェクトによって返される HRESULT の整数値です。  
  
 HRESULT リターンコード、 [OLE オートメーションのリターンコード、およびエラー情報](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)の詳細については、「」を参照してください。  
  
## <a name="result-sets"></a>結果セット  
 メソッドの戻り値が 1 次元または 2 次元の配列である場合、配列は結果セットとしてクライアントに返されます。  
  
-   1 次元の配列の場合は、配列内の要素数と同数の列を持つ 1 行の結果セットとしてクライアントに返されます。 つまり、配列は (列数) として返されます。  
  
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
  
### <a name="a-calling-a-method"></a>A. メソッドを呼び出す  
 次の例では、 `Connect` 以前に作成した **SQLServer** オブジェクトのメソッドを呼び出します。  
  
```  
EXEC @hr = sp_OAMethod @object, 'Connect', NULL, 'my_server',  
    'my_login', 'my_password';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
### <a name="b-getting-a-property"></a>B. プロパティを取得する  
 次の例では、 `HostName` (以前に作成した **SQLServer** オブジェクトの) プロパティを取得し、ローカル変数に格納します。  
  
```  
DECLARE @property varchar(255);  
EXEC @hr = sp_OAMethod @object, 'HostName', @property OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
PRINT @property;  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;の OLE オートメーションストアドプロシージャ ](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE オートメーションのサンプル スクリプト](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
