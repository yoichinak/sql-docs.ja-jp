---
description: Field オブジェクト
title: Field オブジェクト |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field
helpviewer_keywords:
- Field object [ADO]
ms.assetid: b10a72fc-3c4b-4186-a70b-993dc9f7a092
author: rothja
ms.author: jroth
ms.openlocfilehash: 4768281228e39ed8eeb6ffc003e463bf8a53450d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973233"
---
# <a name="field-object"></a>Field オブジェクト
共通のデータ型のデータ列を表します。  
  
## <a name="remarks"></a>解説  
 各 **Field** オブジェクトは、 [レコードセット](../../../ado/reference/ado-api/recordset-object-ado.md)内の列に対応します。 現在のレコードのデータを設定または取得するには、 **Field**オブジェクトの[Value](../../../ado/reference/ado-api/value-property-ado.md)プロパティを使用します。 プロバイダーが公開する機能によっては、 **フィールド** オブジェクトの一部のコレクション、メソッド、またはプロパティが使用できないことがあります。  
  
 **Field**オブジェクトのコレクション、メソッド、およびプロパティを使用して、次の操作を実行できます。  
  
-   [Name](../../../ado/reference/ado-api/name-property-ado.md)プロパティを持つフィールドの名前を返します。  
  
-   " **値** " プロパティを使用して、フィールド内のデータを表示または変更します。 **Value** は、 **Field** オブジェクトの既定のプロパティです。  
  
-   [型](../../../ado/reference/ado-api/type-property-ado.md)、[有効桁数](../../../ado/reference/ado-api/precision-property-ado.md)、および[numericscale](../../../ado/reference/ado-api/numericscale-property-ado.md)プロパティを使用して、フィールドの基本的な特性を返します。  
  
-   定義済みの [size](../../../ado/reference/ado-api/definedsize-property.md) プロパティを使用して、フィールドの宣言されたサイズを返します。  
  
-   [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md)プロパティを使用して、指定されたフィールド内のデータの実際のサイズを返します。  
  
-   [属性](../../../ado/reference/ado-api/attributes-property-ado.md)プロパティと[プロパティ](../../../ado/reference/ado-api/properties-collection-ado.md)コレクションを使用して、特定のフィールドでサポートされる機能の種類を決定します。  
  
-   [Appendchunk](../../../ado/reference/ado-api/appendchunk-method-ado.md)および[GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md)メソッドを使用して、長いバイナリまたは長い文字データを含むフィールドの値を操作します。  
  
-   プロバイダーがバッチ更新をサポートしている場合は、 [Originalvalue](../../../ado/reference/ado-api/originalvalue-property-ado.md) プロパティと [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md) プロパティを使用して、バッチ更新中にフィールド値の不一致を解決します。  
  
 **フィールド**オブジェクトの**レコードセット**を開く前に、すべてのメタデータプロパティ (**名前**、**型**、指定された**サイズ**、**有効桁数**、および**numericscale**) を使用できます。 その時点で設定すると、フォームを動的に構築する場合に便利です。  
  
 ここでは、次のトピックについて説明します。  
  
-   [Field オブジェクトのプロパティ、メソッド、およびイベント](../../../ado/reference/ado-api/field-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>参照  
 [Fields コレクション (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Properties コレクション (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Recordset オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
