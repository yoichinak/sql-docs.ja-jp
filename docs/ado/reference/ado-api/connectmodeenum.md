---
description: ConnectModeEnum
title: ConnectModeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectModeEnum
helpviewer_keywords:
- ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
author: rothja
ms.author: jroth
ms.openlocfilehash: 704e4e78c47744fbdf2288800353fbbd33d8b090
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974713"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
[接続](./connection-object-ado.md)のデータを変更したり、[レコード](./record-object-ado.md)を開いたり、**レコード**および[ストリーム](./stream-object-ado.md)オブジェクトの[Mode](./mode-property-ado.md)プロパティの値を指定したりするために使用できるアクセス許可を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|読み取り専用のアクセス許可を示します。|  
|**adModeReadWrite**|3|読み取り/書き込みアクセス許可を示します。|  
|**adModeRecursive**|0x400000|他の共有* \* 拒否 \* *値 (**adModeShareDenyNone**、 **adModeShareDenyWrite**、または**adModeShareDenyRead**) と共に使用して、現在の**レコード**のすべてのサブレコードに共有の制限を伝達します。 **レコード**に子がない場合、影響はありません。 実行時エラーは、 **adModeShareDenyNone** でのみ使用される場合に生成されます。 ただし、他の値と組み合わせた場合は、 **adModeShareDenyNone** と共に使用できます。 たとえば、"**adModeRead** or **adModeShareDenyNone** or **adModeRecursive**" を使用できます。|  
|**adModeShareDenyNone**|16|他のユーザーが任意のアクセス許可で接続を開くことを許可します。 他のユーザーに対して、読み取りアクセスも書き込みアクセスも拒否できません。|  
|**adModeShareDenyRead**|4|他のユーザーが読み取りアクセス許可で接続を開けないようにします。|  
|**adModeShareDenyWrite**|8|書き込みアクセス許可を持つ接続を他のユーザーが開けないようにします。|  
|**adModeShareExclusive**|12|他のユーザーが接続を開けないようにします。|  
|**adModeUnknown**|0|既定値。 アクセス許可がまだ設定されていないか、または確認できないことを示します。|  
|**adModeWrite**|2|書き込み専用のアクセス許可を示します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums を参照してください。|  
|AdoEnums (ConnectMode)|  
|(AdoEnums に相当するものはありません)|  
|AdoEnums を行います。|  
|AdoEnums を読み取ります。|  
|AdoEnums を作成します。|  
|AdoEnums./EXCLUSIVE|  
|AdoEnums。不明|  
|AdoEnums を作成します。|  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Mode プロパティ (ADO)](./mode-property-ado.md)  
        [Open メソッド (ADO Record)](./open-method-ado-record.md)  
    :::column-end:::
    :::column:::
        [Open メソッド (ADO Stream)](./open-method-ado-stream.md)  
        [Stream オブジェクト (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::