---
description: Append メソッド (ADO)
title: Append メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _DynaCollection::Append
helpviewer_keywords:
- Append method [ADO]
ms.assetid: f8a9bbed-ba9c-4698-945d-317ad22d2e92
author: rothja
ms.author: jroth
ms.openlocfilehash: 84969b95751726579bdc7d4a61aee311b95b6108
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976083"
---
# <a name="append-method-ado"></a>Append メソッド (ADO)
オブジェクトをコレクションに追加します。 コレクションが [フィールド](./fields-collection-ado.md)の場合は、コレクションに追加する前に新しい [Field](./field-object.md) オブジェクトを作成できます。  
  
## <a name="syntax"></a>構文  
  
```  
  
collection.Append object  
fields.Append Name, Type, DefinedSize, Attrib, FieldValue  
```  
  
#### <a name="parameters"></a>パラメーター  
 *表す*  
 コレクションオブジェクト。  
  
 *fields*  
 **フィールド**コレクション。  
  
 *object*  
 追加するオブジェクトを表すオブジェクト変数。  
  
 *名前*  
 新しい**フィールド**オブジェクトの名前を含む**文字列**値。*フィールド*内の他のオブジェクトと同じ名前にすることはできません。  
  
 *Type*  
 新しいフィールドのデータ型を指定する [DataTypeEnum](./datatypeenum.md) 値 (既定値は **adEmpty**)。 次のデータ型は ADO ではサポートされていません。また、[レコードセットオブジェクト (ADO)](./recordset-object-ado.md)に新しいフィールドを追加するときには使用しないでください。この**ようなデータ**型は、実行**ディスパッチ**、指定されていない、 **advariant**です。  
  
 *DefinedSize*  
 省略可能。 新しいフィールドの定義されたサイズ (文字数またはバイト数) を表す **Long 型** の値。 このパラメーターの既定値は、 *型*から派生します。 255 *バイトを超える値が* 設定されているフィールドは、可変長列として扱われます。 既定値は、 *指定されてい* ません。  
  
 *Attrib*  
 省略可能。 新しいフィールドの属性を指定する [FieldAttributeEnum](./fieldattributeenum.md) 値 (既定値は **Adflddefault**)。 この値が指定されていない場合、フィールドには *型*から派生した属性が格納されます。  
  
 *FieldValue*  
 省略可能。 新しいフィールドの値を表す **バリアント** 。 指定しない場合、フィールドには null 値が付加されます。  
  
## <a name="remarks"></a>解説  
  
## <a name="parameters-collection"></a>Parameters コレクション  
 [Parameters](./parameters-collection-ado.md)コレクションに追加する前に、 [Parameter](./parameter-object.md)オブジェクトの[Type](./type-property-ado.md)プロパティを設定する必要があります。 可変長データ型を選択する場合は、 [Size](./size-property-ado-parameter.md) プロパティも0より大きい値に設定する必要があります。  
  
 パラメーターの記述によってプロバイダーの呼び出しが最小化されるため、ストアドプロシージャまたはパラメーター化クエリを使用すると、パフォーマンスが向上します。 ただし、呼び出すストアドプロシージャまたはパラメーター化クエリに関連付けられているパラメーターのプロパティを把握しておく必要があります。  
  
 [Createparameter](./createparameter-method-ado.md)メソッドを使用して、適切なプロパティ設定を持つ**パラメーター**オブジェクトを作成し、 **Append**メソッドを使用して[Parameters](./parameters-collection-ado.md)コレクションに追加します。 これにより、パラメーター情報のプロバイダーを呼び出さなくても、パラメーター値を設定して返すことができます。 パラメーター情報を提供しないプロバイダーに書き込む場合は、パラメーターを使用するために、このメソッドを使用して **パラメーター** コレクションを手動で設定する必要があります。  
  
## <a name="fields-collection"></a>Fields コレクション  
 *FieldValue*パラメーターが有効なのは、レコード**セット**オブジェクトではなく、[レコード](./record-object-ado.md)オブジェクトに**フィールド**オブジェクトを追加する場合のみです。 **レコード**オブジェクトを使用すると、フィールドを追加し、同時に値を指定できます。 **レコード**セットオブジェクトを使用する場合は、**レコードセット**が閉じられている間にフィールドを作成し、**レコードセット**を開き、フィールドに値を割り当てる必要があります。  
  
> [!NOTE]
>  **レコード**オブジェクトの**Fields**コレクションに追加された新しい**Field**オブジェクトの場合は、他の**フィールド**プロパティを指定する前に、 [Value](./value-property-ado.md)プロパティを設定する必要があります。 最初に、**値**プロパティの特定の値が割り当てられており、という**フィールド**コレクションで[更新](./update-method.md)されている必要があります。 その後、 [型](./type-property-ado.md) や [属性](./attributes-property-ado.md) などの他のプロパティにアクセスできます。 次のデータ型 (**DataTypeEnum**) の**フィールド**オブジェクトを**フィールド**コレクションに追加することはできません。エラーが発生します: **adarray**、 **adarray**、 **adEmpty**、 **adpropvariant**、および**adarray**。 また、ADO で**は、次**のデータ型はサポートされていません: の形式で**は、実行****できません。** これらの型では、追加されてもエラーは発生しませんが、メモリリークなどの予期しない結果が発生する可能性があります。  
  
## <a name="recordset"></a>レコードセット  
 **追加**メソッドを呼び出す前に[[カーソルの場所](./cursorlocation-property-ado.md)] プロパティを設定しなかった場合、[レコードセット](./recordset-object-ado.md)オブジェクトの[Open](./open-method-ado-recordset.md)メソッドが呼び出されると、**カーソル位置**は**adUseClient** ([カーソル位置列挙](./cursorlocationenum.md)値) に自動的に設定されます。  
  
 開いている**レコードセット**の**Fields**コレクションまたは[ActiveConnection](./activeconnection-property-ado.md)プロパティが設定されている**レコードセット**で**Append**メソッドが呼び出されると、実行時エラーが発生します。 フィールドを追加できるのは、開かれておらず、まだデータソースに接続されていない **レコードセット** だけです。 これは、通常、 **レコードセット** オブジェクトが [CreateRecordset](../rds-api/createrecordset-method-rds.md) メソッドを使用して、またはオブジェクト変数に割り当てられている場合に当てはまります。  
  
## <a name="record"></a>Record  
 開いている**レコード**の**フィールド**コレクションで**Append**メソッドが呼び出された場合、実行時エラーは発生しません。 新しいフィールドが**レコード**オブジェクトの**フィールド**コレクションに追加されます。 **レコード**がレコード**セット**から派生した場合、新しいフィールドは**レコードセット**オブジェクトの**フィールド**コレクションに表示されません。  
  
 存在しないフィールドは、コレクションに既に存在しているかのように、フィールドオブジェクトに値を割り当てることによって作成し、 **フィールド** コレクションに追加できます。 割り当てによって、 **Field** オブジェクトの自動作成と追加がトリガーされ、割り当てが完了します。  
  
 **レコード**オブジェクトの**Fields**コレクションに**フィールド**を追加した後、 **fields**コレクションの**Update**メソッドを呼び出して変更を保存します。  
  
## <a name="applies-to"></a>適用対象  
  
- [Fields コレクション (ADO)](./fields-collection-ado.md)  
- [Parameters コレクション (ADO)](./parameters-collection-ado.md)  
  
## <a name="see-also"></a>参照  
 [Append および CreateParameter メソッドの例 (VB)](./append-and-createparameter-methods-example-vb.md)   
 [Append および CreateParameter メソッドの例 (VC + +)](./append-and-createparameter-methods-example-vc.md)   
 [CreateParameter メソッド (ADO)](./createparameter-method-ado.md)   
 [Delete メソッド (ADO Fields コレクション)](./delete-method-ado-fields-collection.md)   
 [Delete メソッド (ADO Parameters コレクション)](./delete-method-ado-parameters-collection.md)   
 [Delete メソッド (ADO Recordset)](./delete-method-ado-recordset.md)   
 [Update メソッド](./update-method.md)