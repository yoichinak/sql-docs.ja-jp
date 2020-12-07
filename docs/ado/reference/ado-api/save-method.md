---
description: Save メソッド
title: Save メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Recordset::Save
- _Recordset::raw_Save
helpviewer_keywords:
- Save method [ADO]
ms.assetid: ed3d9678-5c28-4e61-8bb3-7dfb66d99cf5
author: rothja
ms.author: jroth
ms.openlocfilehash: 4ffd13c07fad10d4b0386d342a6ddcbec37256da
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989333"
---
# <a name="save-method"></a>Save メソッド
ファイルまたは[ストリーム](./stream-object-ado.md)オブジェクトに[レコードセット](./recordset-object-ado.md)を保存します。  
  
## <a name="syntax"></a>構文  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>パラメーター  
 *宛先*  
 省略可能。 **レコードセット**を保存するファイルの完全なパス名、または**ストリーム**オブジェクトへの参照を表す**バリアント**。  
  
 *PersistFormat*  
 省略可能。 **レコードセット**を保存する形式を指定する[persistformatenum](./persistformatenum.md)値 (XML または ADTG)。 既定値は **adPersistADTG**です。  
  
## <a name="remarks"></a>解説  
 [Save メソッド]()メソッドは、開いている**レコードセット**でのみ呼び出すことができます。 [Open メソッド (ADO recordset)](./open-method-ado-recordset.md)メソッドを使用して、後で*変換先*から**レコードセット**を復元します。  
  
 [フィルタープロパティ](./filter-property.md)プロパティが**レコードセット**に対して有効になっている場合は、フィルターでアクセスできる行だけが保存されます。 **レコードセット**が階層化されている場合、現在の子**レコードセット**とその子が保存されます (親**レコード**セットを含む)。 子 **レコードセット** の Save メソッドが呼び出されると、子とそのすべての子が保存されますが、親は保存されません。  
  
 **レコードセット**を初めて保存するときは、*変換先*を指定することはできません。 *Destination*を省略した場合は、**レコードセット**の Source プロパティの値に設定された名前で新しいファイルが作成されます。  
  
 最初の保存後に [**保存**] を後で呼び出すときに、 *destination*を省略するか、実行時エラーが発生します。 その後、新しい*変換先*で [**保存**] を呼び出すと、**レコードセット**が新しい変換先に保存されます。 ただし、新しい変換先と元の転送先は両方とも開いています。  
  
 [**保存**] では、**レコードセット**または*変換先*が閉じられないため、**レコードセット**を引き続き使用して、最新の変更を保存することができます。 *変換先* は、 **レコードセット** が閉じられるまで開いたままです。  
  
 セキュリティの理由により、 **Save** メソッドでは、Microsoft Internet Explorer によって実行されるスクリプトの低レベルおよびカスタムセキュリティ設定の使用のみが許可されます。  
  
 非同期の**レコードセット**のフェッチ、実行、または更新操作の実行中に**save**メソッドが呼び出された場合は、非同期操作が完了する**まで待機し**ます。  
  
 レコードは、レコード **セット**の最初の行から保存されます。 **Save**メソッドが終了すると、現在の行の位置が**レコードセット**の最初の行に移動します。  
  
 最適な結果を得るには、[[カーソルの場所] プロパティ (ADO)](./cursorlocation-property-ado.md)プロパティを**adUseClient**に設定し**ます。** プロバイダーが、 **レコードセット** オブジェクトを保存するために必要なすべての機能をサポートしていない場合は、カーソルサービスによってその機能が提供されます。  
  
 [**カーソルの場所**] プロパティを**aduseserver**に設定して**レコードセット**を永続化すると、**レコードセット**の更新機能が制限されます。 通常、単一テーブルの更新、挿入、削除のみが許可されます (プロバイダーの機能によって異なります)。 この構成では、再 [同期メソッド](./resync-method.md) メソッドも使用できません。  
  
> [!NOTE]
>  **Advariant****型、のフィールド、また**は "**不明**" 型の**フィールド**を含む**レコードセット**の保存は ADO ではサポートされていないため、予期しない結果が発生する可能性があります。  
  
 条件文字列の形式のフィルター (OrderDate > ' 12/31/1999 ' など) だけが、永続化された **レコードセット**の内容に影響します。 **ブックマーク**の配列、または[filtergroupenum](./filtergroupenum.md)の値を使用して作成されたフィルターは、永続化された**レコードセット**の内容には影響しません。 これらのルールは、クライアント側のカーソルまたはサーバー側のカーソルを使用して作成された **レコードセット**に適用されます。  
  
 *Destination*パラメーターは OLE DB IStream インターフェイスをサポートする任意のオブジェクトを受け入れることができるため、**レコードセット**を ASP 応答オブジェクトに直接保存できます。 詳細については、「 **XML レコードセットの永続化シナリオ**」を参照してください。  
  
 次の Visual Basic コードに示すように、 **レコードセット** を XML 形式で MSXML DOM オブジェクトのインスタンスに保存することもできます。  
  
```  
Dim xDOM As New MSXML.DOMDocument  
Dim rsXML As New ADODB.Recordset  
Dim sSQL As String, sConn As String  
  
sSQL = "SELECT customerid, companyname, contactname FROM customers"  
sConn="Provider=Microsoft.Jet.OLEDB.4.0;Data Source=Northwind.mdb"  
rsXML.Open sSQL, sConn  
rsXML.Save xDOM, adPersistXML   'Save Recordset directly into a DOM tree.  
...  
```  
  
> [!NOTE]
>  階層レコードセット (データ図形) を XML 形式で保存する場合は、2つの制限が適用されます。 階層 **レコードセット** に保留中の更新が含まれている場合は XML に保存できません。また、パラメーター化された階層 **レコードセット**を保存することもできません。  
  
 XML 形式で保存された **レコードセット** は、utf-8 形式を使用して保存されます。 このようなファイルが ADO ストリームに読み込まれた場合、ストリームの Charset プロパティが UTF-8 形式の適切な値に設定されていない限り、stream オブジェクトはストリームから **レコードセット** を開こうとしません。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Recordset オブジェクト (ADO)](./recordset-object-ado.md)  
    :::column-end:::
    :::column:::
        [Stream オブジェクト (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [Save および Open メソッドの例 (VB)](./save-and-open-methods-example-vb.md)   
 [Save および Open メソッドの例 (VC + +)](./save-and-open-methods-example-vc.md)   
 [Open メソッド (ADO Recordset)](./open-method-ado-recordset.md)   
 [Open メソッド (ADO Stream)](./open-method-ado-stream.md)   
 [SaveToFile メソッド](./savetofile-method.md)