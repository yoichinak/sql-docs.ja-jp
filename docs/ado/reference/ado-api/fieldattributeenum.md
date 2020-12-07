---
description: FieldAttributeEnum
title: FieldAttributeEnum |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldAttributeEnum
helpviewer_keywords:
- FieldAttributeEnum enumeration [ADO]
ms.assetid: 6e34d886-005a-40dc-bd5c-6adcbf81e5cd
author: rothja
ms.author: jroth
ms.openlocfilehash: 4b218616ec1514ea8af1c160b155b63fb54c182c
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973173"
---
# <a name="fieldattributeenum"></a>FieldAttributeEnum
[Field](../../../ado/reference/ado-api/field-object.md)オブジェクトの1つまたは複数の属性を指定します。  
  
|定数|値|説明|  
|--------------|-----------|-----------------|  
|**adFldCacheDeferred**|0x1000|プロバイダーがフィールド値をキャッシュし、それ以降の読み取りがキャッシュから実行されることを示します。|  
|**adFldFixed**|0x10|フィールドに固定長のデータが含まれていることを示します。|  
|**adFldIsChapter**|0x2000|フィールドにチャプター値が含まれていることを示します。これは、この親フィールドに関連する特定の子レコードセットを指定します。 通常、チャプターフィールドはデータシェイプまたはフィルターで使用されます。|  
|**adFldIsCollection**|0x40000|フィールドが、レコードによって表されるリソースが、テキストファイルなどの単純なリソースではなく、フォルダーなどの他のリソースのコレクションであることを指定することを示します。|  
|**adFldKeyColumn**|0x8000|フィールドが列の主キーの一部またはすべてを指定することを示します。|  
|**adFldIsDefaultStream**|0x20000|レコードによって表されるリソースの既定のストリームがフィールドに格納されていることを示します。 たとえば、既定のストリームは、Web サイトのルートフォルダーの HTML コンテンツにすることができます。これは、ルート URL を指定したときに自動的に提供されます。|  
|**adFldIsNullable**|0x20|フィールドが null 値を許容することを示します。|  
|**adFldIsRowURL**|0x10000|レコードによって表されるデータストアからリソースに名前を指定する URL がフィールドに含まれていることを示します。|  
|**adFldLong**|0x80|フィールドが長いバイナリフィールドであることを示します。 また、 [Appendchunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) メソッドと [GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) メソッドも使用できることを示します。|  
|**adFldMayBeNull**|0x40|フィールドから null 値を読み取ることができることを示します。|  
|**Adfldon Defer**|0x2|フィールドが遅延していることを示します。つまり、フィールド値は、レコード全体ではなく、明示的にアクセスしたときにのみ、データソースから取得されません。|  
|**adFldNegativeScale**|0x4000|フィールドが負の小数点以下桁数の値をサポートする列の数値を表すことを示します。 小数点以下桁数は、 [numericscale](../../../ado/reference/ado-api/numericscale-property-ado.md) プロパティによって指定されます。|  
|**Adflが Wid**|0x100|フィールドには、に書き込むことができず、行 (レコード番号、一意識別子など) を識別する以外に意味のある値を持たない永続的な行識別子が含まれていることを示します。|  
|**adFldRowVersion**|0x200|更新を追跡するために使用される時間または日付スタンプがフィールドに含まれていることを示します。|  
|**adFldUnknownUpdatable**|0x8|フィールドに書き込むことができるかどうかをプロバイダーが判断できないことを示します。|  
|**adFldUnspecified**|-1 0xFFFFFFFF|プロバイダーでフィールド属性が指定されていないことを示します。|  
|**adFldUpdatable**|0x4|フィールドに書き込むことができることを示します。|  
  
## <a name="adowfc-equivalent"></a>同等の ADO/WFC  
 パッケージ: **com. ms. wfc. データ**  
  
|定数|  
|--------------|  
|AdoEnums FieldAttribute|  
|AdoEnums FieldAttribute|  
|AdoEnums FieldAttribute|  
|AdoEnums FieldAttribute|  
|AdoEnums.FieldAttribute.MAYBENULL|  
|AdoEnums FieldAttribute|  
|AdoEnums.FieldAttribute.NEGATIVESCALE|  
|AdoEnums FieldAttribute|  
|AdoEnums. FieldAttribute. ROWVERSION|  
|AdoEnums.FieldAttribute.UNKNOWNUPDATABLE|  
|AdoEnums. FieldAttribute|  
|AdoEnums FieldAttribute|  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Append メソッド (ADO)](../../../ado/reference/ado-api/append-method-ado.md)  
    :::column-end:::
    :::column:::
        [Attributes プロパティ (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)  
    :::column-end:::
:::row-end:::
