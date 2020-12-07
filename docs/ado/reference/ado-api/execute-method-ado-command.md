---
description: Execute メソッド (ADO Command)
title: Execute メソッド (ADO コマンド) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::Execute
- Command15::raw_Execute
helpviewer_keywords:
- Execute method [ADO]
ms.assetid: f84a5ff3-0528-4ad7-9bea-9a15103378dd
author: rothja
ms.author: jroth
ms.openlocfilehash: 5bd7e8d98f7d7ccecfce2ce66852f92efa1dae77
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973513"
---
# <a name="execute-method-ado-command"></a>Execute メソッド (ADO Command)
[Command オブジェクト](../../../ado/reference/ado-api/command-object-ado.md)の[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)または[commandstream](../../../ado/reference/ado-api/commandstream-property-ado.md)プロパティで指定されたクエリ、SQL ステートメント、またはストアドプロシージャを実行します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set recordset = command.Execute( RecordsAffected, Parameters, Options )  
```  
  
## <a name="return-value"></a>戻り値  
 [レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクト参照、ストリーム、または**Nothing**を返します。  
  
#### <a name="parameters"></a>パラメーター  
 *RecordsAffected*  
 省略可能。 操作によって影響を受けたレコードの数をプロバイダーが返す **長い** 変数。 *RecordsAffected*パラメーターは、アクションクエリまたはストアドプロシージャに対してのみ適用されます。 *RecordsAffected* は、結果を返すクエリまたはストアドプロシージャによって返されたレコードの数を返しません。 この情報を取得するには、 [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) プロパティを使用します。 **Execute**メソッドは、コマンドが非同期に実行されるときに、影響を受けたレコードの数がメソッドから返された時点でまだ知られていない可能性があるため、 **adasyncexecute**と共に使用しても正しい情報を返しません。  
  
 *パラメーター*  
 省略可能。 **CommandText**または**commandstream**で指定された入力文字列またはストリームと組み合わせて使用されるパラメーター値の**Variant**配列。 (この引数で渡された場合、出力パラメーターは正しい値を返しません)。  
  
 *Options*  
 省略可能。 プロバイダーが[コマンド](../../../ado/reference/ado-api/command-object-ado.md)オブジェクトの[CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md)または[commandstream](../../../ado/reference/ado-api/commandstream-property-ado.md)プロパティをどのように評価するかを示す**Long**値。 [Commandtypeenum](../../../ado/reference/ado-api/commandtypeenum.md)値または[executeoptionenum](../../../ado/reference/ado-api/executeoptionenum.md)値を使用して作成されたビットマスク値を指定できます。 たとえば、 **Adcmdtext** と **adExecuteNoRecords** を組み合わせて使用すると、 **ado.net プロパティの** 値をテキストとして評価し、コマンドテキストの実行時に生成される可能性のあるレコードがコマンドによって破棄され、返されないようにすることができます。  
  
> [!NOTE]
>  **Executeoptionenum**値**adExecuteNoRecords**を使用すると、内部処理を最小限に抑えてパフォーマンスを向上させることができます。 **AdExecuteStream**を指定した場合、 **adasyncfetch**と**adAsynchFetchNonBlocking**オプションは無視されます。 **Execute**を使用して**adcmdfile**または**Adcmdtabledirect**の**commandtypeenum**値を使用しないでください。 これらの値は、**レコードセット**の[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)メソッドおよび[Requery](../../../ado/reference/ado-api/requery-method.md)メソッドでオプションとしてのみ使用できます。  
  
## <a name="remarks"></a>解説  
 **Command**オブジェクトに対して**Execute**メソッドを使用すると、オブジェクトの**CommandText**プロパティまたは**commandstream**プロパティで指定されたクエリが実行されます。  
  
 結果は、 **レコードセット** (既定では) またはバイナリ情報のストリームとして返されます。 バイナリストリームを取得するには、 *Options*で**adExecuteStream**を指定してから、コマンドを設定してストリームを指定し**ます ("出力ストリーム")**。 結果を受け取るために ADO **ストリーム** オブジェクトを指定することも、IIS 応答オブジェクトなどの別のストリームオブジェクトを指定することもできます。 **AdExecuteStream**で**Execute**を呼び出す前にストリームが指定されなかった場合は、エラーが発生します。 **Execute**から戻るときのストリームの位置は、プロバイダー固有です。  
  
 コマンドが結果を返すことを意図していない場合 (SQL UPDATE クエリなど)、オプション**adExecuteNoRecords**が指定されていれば、プロバイダーは**何も**返しません。それ以外の場合は、終了した**レコードセット**が返されます。 アプリケーション言語によっては、 **レコードセット** が不要な場合にこの戻り値を無視することができます。  
  
 **CommandType**が**adCmdStoredProc**、 **adcmdtable**、または**adcmdtabledirect**の場合、ユーザーが**Commandstream**の値を指定すると、 **Execute**によってエラーが発生します。  
  
 クエリにパラメーターがある場合、 **Execute**呼び出しで渡されたパラメーター値を使用してこれらをオーバーライドしない限り、**コマンド**オブジェクトのパラメーターの現在の値が使用されます。 **Execute**メソッドを呼び出すときに、一部のパラメーターの新しい値を省略して、パラメーターのサブセットをオーバーライドできます。 パラメーターを指定する順序は、メソッドが渡す順序と同じです。 たとえば、4つ (以上) のパラメーターがあり、1番目と4番目のパラメーターに対してのみ新しい値を渡す場合は、 `Array(var1,,,var4)` *パラメーター* 引数としてを渡します。  
  
> [!NOTE]
>  *パラメーター*引数で渡された場合、出力パラメーターは正しい値を返しません。  
  
 この操作が終了すると、 [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md) イベントが発行されます。  
  
> [!NOTE]
>  Url を含むコマンドを発行する場合、http スキームを使用するコマンドは、 [インターネット公開のために Microsoft OLE DB プロバイダー](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)を自動的に呼び出します。 詳細については、「 [絶対 url と相対 url](../../../ado/guide/data/absolute-and-relative-urls.md)」を参照してください。  
  
## <a name="applies-to"></a>適用対象  
 [Command オブジェクト (ADO)](../../../ado/reference/ado-api/command-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Execute、Requery、および Clear メソッドの例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Execute、Requery、および Clear メソッドの例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Execute、Requery、および Clear メソッドの例 (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandStream プロパティ (ADO)](../../../ado/reference/ado-api/commandstream-property-ado.md)   
 [CommandText プロパティ (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)   
 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)   
 [Execute メソッド (ADO Connection)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [ExecuteComplete イベント (ADO)](../../../ado/reference/ado-api/executecomplete-event-ado.md)
