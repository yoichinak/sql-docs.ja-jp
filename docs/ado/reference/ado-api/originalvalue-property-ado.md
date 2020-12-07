---
description: OriginalValue プロパティ (ADO)
title: OriginalValue プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::OriginalValue
helpviewer_keywords:
- OriginalValue property [ADO]
ms.assetid: 6e33c6ec-14d9-4b1d-ba9b-cb99862e7bac
author: rothja
ms.author: jroth
ms.openlocfilehash: ab73e79f86ac1e504322a0606ee3839997ce5811
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990213"
---
# <a name="originalvalue-property-ado"></a>OriginalValue プロパティ (ADO)
変更が行われる前にレコード内に存在していた [フィールド](./field-object.md) の値を示します。  
  
## <a name="return-value"></a>戻り値  
 変更前のフィールドの値を表す **バリアント** 値を返します。  
  
## <a name="remarks"></a>解説  
 現在のレコードからフィールドの元のフィールド値を返すには、 **Originalvalue** プロパティを使用します。  
  
 *即時更新モード*( [update](./update-method.md)メソッドを呼び出した後に、プロバイダーが基になるデータソースに変更を書き込む) では、 **originalvalue**プロパティは、変更前 (つまり、最後の**更新**メソッドの呼び出し以降) に存在していたフィールド値を返します。 これは、 [CancelUpdate](./cancelupdate-method-ado.md) メソッドが [value](./value-property-ado.md) プロパティを置き換えるために使用するのと同じ値です。  
  
 *バッチ更新モード*(プロバイダーによって複数の変更がキャッシュされ、 [updatebatch](./updatebatch-method.md)メソッドを呼び出したときに基になるデータソースに書き込まれる) では、 **originalvalue**プロパティは、変更前 (つまり、最後の**updatebatch**メソッド呼び出し以降) に存在していたフィールド値を返します。 これは、 [CancelBatch](./cancelbatch-method-ado.md) メソッドが **value** プロパティを置き換えるために使用するのと同じ値です。 このプロパティを [UnderlyingValue](./underlyingvalue-property.md) プロパティと共に使用すると、バッチ更新で発生した競合を解決できます。  
  
## <a name="record"></a>Record  
 [レコード](./record-object-ado.md)オブジェクトの場合、 [Update](./update-method.md)が呼び出される前に追加されたフィールドの**originalvalue**プロパティは空になります。  
  
## <a name="applies-to"></a>適用対象  
 [Field オブジェクト](./field-object.md)  
  
## <a name="see-also"></a>参照  
 [OriginalValue プロパティと UnderlyingValue プロパティの例 (VB)](./originalvalue-and-underlyingvalue-properties-example-vb.md)   
 [OriginalValue プロパティと UnderlyingValue プロパティの例 (VC + +)](./originalvalue-and-underlyingvalue-properties-example-vc.md)   
 [UnderlyingValue プロパティ](./underlyingvalue-property.md)