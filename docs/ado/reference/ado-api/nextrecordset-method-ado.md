---
description: NextRecordset メソッド (ADO)
title: NextRecordset メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- NextRecordset
- Recordset15::NextRecordset
- Recordset15::raw_NextRecordset
helpviewer_keywords:
- NextRecordset method [ADO]
ms.assetid: ab1fa449-a695-4987-b1ee-bc68f89418dd
author: rothja
ms.author: jroth
ms.openlocfilehash: b73779dbca82df1d672a57aae667bc5a666a4945
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990463"
---
# <a name="nextrecordset-method-ado"></a>NextRecordset メソッド (ADO)
一連のコマンドを進めて、現在の [レコードセット](./recordset-object-ado.md) オブジェクトをクリアし、次の **レコードセット** を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Set recordset2 = recordset1.NextRecordset(RecordsAffected )  
```  
  
## <a name="return-value"></a>戻り値  
 **レコードセット**オブジェクトを返します。 構文モデルでは、 *recordset1* と *Recordset2* を同じ **レコードセット** オブジェクトにすることも、個別のオブジェクトを使用することもできます。 個別の**レコードセット**オブジェクトを使用する場合は、 **NextRecordset**が呼び出された後に元の**レコードセット**(*recordset1*) の**ActiveConnection**プロパティをリセットすると、エラーが発生します。  
  
#### <a name="parameters"></a>パラメーター  
 *RecordsAffected*  
 省略可能。 プロバイダーが、現在の操作によって影響を受けたレコードの数を返す **Long 型** の変数。  
  
> [!NOTE]
>  このパラメーターは、操作によって影響を受けたレコードの数のみを返します。レコード **セット**の生成に使用される select ステートメントからは、レコードの数は返されません。  
  
## <a name="remarks"></a>解説  
 **NextRecordset**メソッドを使用して、複合コマンドステートメントまたは複数の結果を返すストアドプロシージャで、次のコマンドの結果を返します。 複合コマンドステートメントに基づいて**レコードセット**オブジェクトを開く場合 (例: "SELECT \* FROM table1;"SELECT \* FROM table2 ")[コマンド](./command-object-ado.md)の[Execute](./execute-method-ado-command.md)メソッド、または**レコードセット**の[Open](./open-method-ado-recordset.md)メソッドを使用して、ADO は最初のコマンドのみを実行し、結果を*レコードセット*に返します。 ステートメント内の後続のコマンドの結果にアクセスするには、 **NextRecordset** メソッドを呼び出します。  
  
 追加の結果が存在し、複合ステートメントを含む **レコードセット** がプロセスの境界を越えて切断またはマーシャリングされていない限り、 **NextRecordset** メソッドは **レコードセット** オブジェクトを返し続けます。 行を返すコマンドが正常に実行されても、レコードが返されない場合、返された **レコードセット** オブジェクトは開かれますが、空になります。 このケースをテストするには、 [BOF](./bof-eof-properties-ado.md) プロパティと [EOF](./bof-eof-properties-ado.md) プロパティが両方とも **True**であることを確認します。 行を返さないコマンドが正常に実行されると、返された**レコードセット**オブジェクトは閉じられます。このオブジェクトは、**レコードセット**の[State](./state-property-ado.md)プロパティをテストすることで確認できます。 これ以上結果がない場合、 *レコードセット* は *Nothing*に設定されます。  
  
 **NextRecordset**メソッドは、接続されていない**レコードセット**オブジェクトでは使用できません。この場合、 [ActiveConnection](./activeconnection-property-ado.md)は**NOTHING** (Microsoft Visual Basic) または NULL (他の言語) に設定されています。  
  
 即時更新モードで編集が進行中の場合、 **NextRecordset** メソッドを呼び出すとエラーが発生します。 [Update](./update-method.md) または [CancelUpdate](./cancelupdate-method-ado.md) メソッドを最初に呼び出します。  
  
 [Parameters](./parameters-collection-ado.md)コレクションに入力するか、元の**Open**または**Execute**呼び出しを使用して配列を渡すことによって、複合ステートメント内の複数のコマンドのパラメーターを渡すには、コマンドシリーズの各コマンドと同じ順序で、コレクションまたは配列内のパラメーターを指定する必要があります。 出力パラメーターの値を読み取る前に、すべての結果の読み取りを完了する必要があります。  
  
 OLE DB プロバイダーは、複合ステートメント内の各コマンドが実行されるタイミングを決定します。 たとえば、 [SQL Server の Microsoft OLE DB Provider](../../guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)は、複合ステートメントの受信時にバッチ内のすべてのコマンドを実行します。 **NextRecordset**を呼び出すと、結果として得られる**レコードセット**が返されます。  
  
 ただし、他のプロバイダーは、NextRecordset が呼び出された後にのみ、ステートメント内で次のコマンドを実行できます。 これらのプロバイダーでは、コマンドステートメント全体をステップ実行する前に **レコードセット** オブジェクトを明示的に閉じても、残りのコマンドは実行されません。  
  
## <a name="applies-to"></a>適用対象  
 [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [NextRecordset メソッドの例 (VB)](./nextrecordset-method-example-vb.md)   
 [NextRecordset メソッドの例 (VC++)](./nextrecordset-method-example-vc.md)