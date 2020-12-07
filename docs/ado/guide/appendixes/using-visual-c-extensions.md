---
description: Visual C++ Extensions を使用する
title: Visual C++ 拡張機能の使用 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ [ADO], using VC++ extensions
- ADO, Visual C++
ms.assetid: ff759185-df41-4507-8d12-0921894ffbd9
author: rothja
ms.author: jroth
ms.openlocfilehash: 0419311c4d8e952a5212f60dee055c7b37aed5f4
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990933"
---
# <a name="visual-c-extensions"></a>Visual C++ 拡張機能
## <a name="the-iadorecordbinding-interface"></a>IADORecordBinding インターフェイス
 Microsoft Visual C++ Extensions for ADO は、 [レコードセット](../../reference/ado-api/recordset-object-ado.md) オブジェクトのフィールドを C/c + + 変数に関連付けたり、バインドしたりします。 バインドされた **レコードセット** の現在の行が変更されるたびに、 **レコードセット** 内のすべてのバインドフィールドが C/c + + 変数にコピーされます。 必要に応じて、コピーされたデータは C/c + + 変数の宣言データ型に変換されます。

 **IADORecordBinding**インターフェイスの**BindToRecordset**メソッドは、フィールドを C/c + + 変数にバインドします。 **AddNew**メソッドは、バインドされた**レコードセット**に新しい行を追加します。 **Update**メソッドは、**レコードセット**の新しい行にフィールドを追加したり、既存の行のフィールドを C/c + + 変数の値で更新したりします。

 **IADORecordBinding**インターフェイスは、**レコードセット**オブジェクトによって実装されます。 実装を自分でコーディングすることはありません。

## <a name="binding-entries"></a>バインドエントリ
 Visual C++ の拡張機能は、 [レコードセット](../../reference/ado-api/recordset-object-ado.md) オブジェクトのフィールドを C/c + + 変数にマップします。 フィールドと変数の間のマッピングの定義は、 *バインドエントリ*と呼ばれます。 マクロは、数値、固定長、可変長データのバインドエントリを提供します。 バインドエントリと C/c + + 変数は、Visual C++ Extensions クラス **CADORecordBinding**から派生したクラスで宣言されます。 **CADORecordBinding**クラスは、バインドエントリマクロによって内部的に定義されます。

 ADO は、これらのマクロのパラメーターを内部で OLE DB **DBBINDING** 構造体にマップし、フィールドと変数間のデータの移動と変換を管理するための OLE DB **Accessor** オブジェクトを作成します。 OLE DB は、データが格納される *バッファー* である3つの部分で構成されるデータを定義します。フィールドがバッファーに正常に格納されたかどうか、または変数をフィールドに復元する方法を示す *状態* 。データの *長さ* 。 (詳細については、OLE DB プログラマーリファレンスの「 [データの取得と設定 (OLE DB)](/previous-versions/windows/desktop/ms713700(v=vs.85))」を参照してください。

## <a name="header-file"></a>ヘッダー ファイル
 ADO の Visual C++ 拡張機能を使用するには、アプリケーションに次のファイルを含めます。

```cpp
#include <icrsint.h>
```

## <a name="binding-recordset-fields"></a>レコードセットフィールドのバインド

#### <a name="to-bind-recordset-fields-to-cc-variables"></a>レコードセットフィールドを C/c + + 変数にバインドするには

1.  **CADORecordBinding**クラスから派生したクラスを作成します。

2.  派生クラスでバインドエントリおよび対応する C/c + + 変数を指定します。 **BEGIN_ADO_BINDING**と**END_ADO_BINDING**マクロ間のバインドエントリをかっこで囲みます。 マクロは、コンマまたはセミコロンで終了しないでください。 適切な区切り記号は、各マクロによって自動的に指定されます。

     C/c + + 変数にマップする各フィールドのバインドエントリを1つ指定します。 **ADO_FIXED_LENGTH_ENTRY**、 **ADO_NUMERIC_ENTRY**、または**ADO_VARIABLE_LENGTH_ENTRY**のマクロファミリから適切なメンバーを使用します。

3.  アプリケーションで、 **CADORecordBinding**から派生したクラスのインスタンスを作成します。 **レコードセット**から**IADORecordBinding**インターフェイスを取得します。 次に、 **BindToRecordset** メソッドを呼び出して、 **レコードセット** フィールドを C/c + + 変数にバインドします。

 詳細については、 [Visual C++ 拡張機能の例](./visual-c-extensions-example.md)を参照してください。

## <a name="interface-methods"></a>インターフェイス メソッド
 **IADORecordBinding**インターフェイスには、 **BindToRecordset**、 **AddNew**、 **Update**という3つのメソッドがあります。 各メソッドの唯一の引数は、 **CADORecordBinding**から派生したクラスのインスタンスへのポインターです。 そのため、 **AddNew** メソッドと **Update** メソッドでは、ADO メソッド namesakes のパラメーターを指定できません。

## <a name="syntax"></a>構文
 **BindToRecordset**メソッドは、**レコードセット**フィールドを C/c + + 変数に関連付けます。

```cpp
BindToRecordset(CADORecordBinding *binding)
```

 **AddNew**メソッドは、ADO [addnew](../../reference/ado-api/addnew-method-ado.md)メソッド名前を呼び出して、**レコードセット**に新しい行を追加します。

```cpp
AddNew(CADORecordBinding *binding)
```

 **Update**メソッドは、ADO [update](../../reference/ado-api/update-method.md)メソッドである名前を呼び出して、**レコードセット**を更新します。

```cpp
Update(CADORecordBinding *binding)
```

## <a name="binding-entry-macros"></a>バインドエントリマクロ
 バインドエントリマクロは、 **レコードセット** フィールドと変数の関連付けを定義します。 先頭と末尾のマクロは、一連のバインドエントリを区切ります。

 **Addate**や**addate**などの固定長データには、マクロファミリが用意されています。数値データ ( **Adtinyint**、 **Adtinyint**、 **addouble**など)および可変長データ ( **Adchar**、 **adVarChar** 、 **adVarBinary**など)。 **AdVarNumeric**を除くすべての数値型も固定長型です。 各ファミリには、対象にならないバインド情報を除外できるように、さまざまなパラメーターのセットがあります。

 詳細については、「 [付録 a: データ型](/previous-versions/windows/desktop/ms723969(v=vs.85))」を参照して OLE DB プログラマーリファレンスを参照してください。

### <a name="begin-binding-entries"></a>バインドエントリの開始
 **BEGIN_ADO_BINDING**(*クラス*)

### <a name="fixed-length-data"></a>固定長データ
 **ADO_FIXED_LENGTH_ENTRY**(*序数、データ型、バッファー、状態、変更*)

 **ADO_FIXED_LENGTH_ENTRY2**(*序数、データ型、バッファー、変更*)

### <a name="numeric-data"></a>数値データ
 **ADO_NUMERIC_ENTRY**(*序数、データ型、バッファー、有効桁数、小数点以下桁数、状態、変更*)

 **ADO_NUMERIC_ENTRY2**(*序数、データ型、バッファー、有効桁数、小数点以下桁数、変更*)

### <a name="variable-length-data"></a>可変長データ
 **ADO_VARIABLE_LENGTH_ENTRY**(*序数、データ型、バッファー、サイズ、状態、長さ、変更*)

 **ADO_VARIABLE_LENGTH_ENTRY2**(*序数、データ型、バッファー、サイズ、状態、変更*)

 **ADO_VARIABLE_LENGTH_ENTRY3**(*序数、データ型、バッファー、サイズ、長さ、変更*)

 **ADO_VARIABLE_LENGTH_ENTRY4**(*序数、データ型、バッファー、サイズ、変更*)

### <a name="end-binding-entries"></a>バインドエントリの終了
 **END_ADO_BINDING**()

|パラメーター|説明|
|---------------|-----------------|
|*クラス*|バインドエントリおよび C/c + + 変数が定義されているクラス。|
|*Ordinal*|C/c + + 変数に対応する **レコードセット** フィールドの1から数えた序数。|
|*DataType*|C/c + + 変数の同等の ADO データ型 (有効なデータ型の一覧については、「 [DataTypeEnum](../../reference/ado-api/datatypeenum.md) 」を参照してください)。 必要に応じて、 **レコードセット** フィールドの値がこのデータ型に変換されます。|
|*バッファー*|**レコードセット**フィールドが格納される C/c + + 変数の名前。|
|*[サイズ]*|*バッファー*の最大サイズ (バイト単位)。 *Buffer*に可変長文字列が含まれている場合は、終了ゼロに対してスペースを許可します。|
|*状態*|*バッファー*の内容が有効かどうか、およびフィールドから*データ型*への変換が成功したかどうかを示す変数の名前。<br /><br /> この変数の最も重要な2つの値は **Adfldok**です。これは、変換が成功したことを意味します。と **Adfldnull**。これは、フィールドの値が VT_NULL 型のバリアントであり、単に空ではないことを意味します。<br /><br /> *状態*に使用できる値は、次の表「状態の値」に記載されています。|
|*Modify*|ブール型のフラグ。TRUE の場合、ADO は、対応する **レコードセット** フィールドを *Buffer*に含まれる値で更新することが許可されていることを示します。<br /><br /> ブール型の *modify* パラメーターを TRUE に設定して、ADO でバインドされたフィールドを更新できるようにします。また、フィールドを確認し、変更しない場合は FALSE に設定します。|
|*[精度]*|数値変数で表すことができる桁数。|
|*スケール*|数値変数の小数点以下の桁数。|
|*[データ型]*|*バッファー*内のデータの実際の長さを格納する4バイト変数の名前。|

## <a name="status-values"></a>状態値
 *Status*変数の値は、フィールドが変数に正常にコピーされたかどうかを示します。

 データを設定するときに、 *状態* を **Adfldnull** に設定して、 **レコードセット** フィールドを null に設定する必要があることを示すことができます。

|定数|値|説明|
|--------------|-----------|-----------------|
|**adFldOK**|0|Null 以外のフィールド値が返されました。|
|**adFldBadAccessor**|1|バインドが無効です。|
|**adFldCantConvertValue**|2|符号の不一致またはデータのオーバーフロー以外の理由により、値を変換できませんでした。|
|**adFldNull**|3|フィールドを取得するときに、null 値が返されたことを示します。<br /><br /> フィールドを設定するときに、フィールドが**null**自体 (文字配列や整数など) をエンコードできない場合は、フィールドを**null**に設定する必要があることを示します。|
|**adFldTruncated**|4|可変長データまたは数字が切り捨てられました。|
|**adFldSignMismatch**|5|値が符号付きで、変数のデータ型が符号なしです。|
|**adFldDataOverFlow**|6|値が変数のデータ型に格納できる数を超えています。|
|**adFldCantCreate**|7|不明な列の型とフィールドが既に開いています。|
|**adFldUnavailable 使用できません**|8|フィールドの値を特定できませんでした。たとえば、新しい未割り当てフィールドで既定値が指定されていない場合などです。|
|**adFldPermissionDenied**|9|更新するときに、データを書き込むアクセス許可がありません。|
|**adFldIntegrityViolation**|10|更新すると、フィールドの値が列の整合性に違反することになります。|
|**adFldSchemaViolation**|11|更新すると、フィールドの値が列のスキーマに違反します。|
|**adFldBadStatus**|12|更新するときに、状態パラメーターが無効です。|
|**adFldDefault**|13|更新時に既定値が使用されました。|

## <a name="see-also"></a>参照
 [Visual C++ 拡張機能の例](./visual-c-extensions-example.md) [Visual C++ extensions ヘッダー](./visual-c-extensions-header.md)