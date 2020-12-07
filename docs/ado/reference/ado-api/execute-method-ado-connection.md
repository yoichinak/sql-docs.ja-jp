---
description: Execute メソッド (ADO Connection)
title: Execute メソッド (ADO Connection) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Execute
- Connection15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: 03c69320-96b2-4d85-8d49-a13b13e31578
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d5f0c63773a0eb07233ffff0eb74f39e45baf33
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973553"
---
# <a name="execute-method-ado-connection"></a>Execute メソッド (ADO Connection)
指定されたクエリ、SQL ステートメント、ストアドプロシージャ、またはプロバイダー固有のテキストを実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
Set recordset = connection.Execute (CommandText, RecordsAffected, Options)  
```  
  
## <a name="return-value"></a>戻り値  
 [レコードセットオブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト参照を返します。  
  
#### <a name="parameters"></a>パラメーター  
 *CommandText*  
 実行する SQL ステートメント、ストアドプロシージャ、URL、またはプロバイダー固有のテキストを含む **文字列** 値です。 **必要に応じ**て、プロバイダーが SQL 対応である場合にのみ、テーブル名を使用できます。 たとえば、"Customers" という名前のテーブルが使用されている場合、ADO は自動的に標準の SQL Select 構文を先頭に付加し、"SELECT * FROM Customers" をステートメントとして [!INCLUDE[tsql](../../../includes/tsql-md.md)] プロバイダーに渡します。  
  
 *RecordsAffected*  
 省略可能。 操作によって影響を受けたレコードの数をプロバイダーが返す **長い** 変数。  
  
 *Options*  
 省略可能。 プロバイダーが CommandText 引数を評価する方法を示す **Long** 値。 1つ以上の [Commandtypeenum](../../../ado/reference/ado-api/commandtypeenum.md) 値または [executeoptionenum](../../../ado/reference/ado-api/executeoptionenum.md) 値のビットマスクを指定できます。  
  
 **メモ****Executeoptionenum**値**adExecuteNoRecords**を使用すると、内部処理を最小限に抑え、Visual Basic 6.0 から移植するアプリケーションに対して、パフォーマンスを向上させることができます。  
  
 **Connection**オブジェクトの**Execute**メソッドで**adExecuteStream**を使用しないでください。  
  
 Execute を使用して adCmdFile または adCmdTableDirect の CommandTypeEnum 値を使用しないでください。 これらの値は、**レコードセット**の[OPEN メソッド (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)および[Requery メソッド](../../../ado/reference/ado-api/requery-method.md)メソッドを使用したオプションとしてのみ使用できます。  
  
## <a name="remarks"></a>解説  
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクトに対して**Execute**メソッドを使用すると、指定された接続の CommandText 引数でメソッドに渡す任意のクエリが実行されます。 CommandText 引数で行を返すクエリが指定されている場合、実行によって生成される結果は、新しい **レコードセット** オブジェクトに格納されます。 コマンドが結果を返すことを意図していない場合 (SQL UPDATE クエリなど)、オプション**adExecuteNoRecords**が指定されていれば、プロバイダーは**何も**返しません。それ以外の場合は、終了した**レコードセット**が返されます。  
  
 返される **レコードセット** オブジェクトは、常に読み取り専用の順方向専用カーソルです。 より多くの機能を持つ **レコードセット** オブジェクトが必要な場合は、まず、必要なプロパティ設定を使用して **レコードセット** オブジェクトを作成し、次に **レコードセット** オブジェクトの [Open メソッド (ADO recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) メソッドを使用してクエリを実行し、目的のカーソルの種類を返します。  
  
 *CommandText*引数の内容はプロバイダーに固有であり、標準の SQL 構文、またはプロバイダーがサポートする特殊なコマンド形式にすることができます。  
  
 この操作が終了すると、ExecuteComplete イベントが発行されます。  
  
> [!NOTE]
>  Http スキームを使用する Url は、 [インターネット公開のために Microsoft OLE DB プロバイダー](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)を自動的に呼び出します。 詳細については、「 [絶対 url と相対 url](../../../ado/guide/data/absolute-and-relative-urls.md)」を参照してください。  
  
## <a name="applies-to"></a>適用対象  
 [Connection オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
