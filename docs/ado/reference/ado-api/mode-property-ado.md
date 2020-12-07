---
description: Mode プロパティ (ADO)
title: Mode プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::Mode
- _Stream::Mode
- _Record::Mode
helpviewer_keywords:
- Mode property [ADO]
ms.assetid: 808661eb-0d7c-4e6d-8e40-9dc3bef3d77a
author: rothja
ms.author: jroth
ms.openlocfilehash: eab9f3db1bfe9417411dc832cfa24e3d4496257b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990603"
---
# <a name="mode-property-ado"></a>Mode プロパティ (ADO)
[接続](./connection-object-ado.md)、[レコード](./record-object-ado.md)、または[ストリーム](./stream-object-ado.md)オブジェクトのデータを変更するために使用できるアクセス許可を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 [Connectmodeenum](./connectmodeenum.md)値を設定または返します。 **接続**の既定値は**admodeunknown**です。 **レコード**オブジェクトの既定値は**adModeRead**です。 基になるソースに関連付けられている**ストリーム**の既定値 (ソースとして URL を使用して開かれるか、**レコード**の既定の**ストリーム**として開かれる) は、 **adModeRead**です。 基になるソース (メモリ内でインスタンス化) に関連付けられていない **ストリーム** の既定値は **admodeunknown**です。  
  
## <a name="remarks"></a>解説  
 **Mode**プロパティを使用して、現在の接続でプロバイダーによって使用されているアクセス許可を設定または取得します。 **Mode**プロパティを設定できるのは、**接続**オブジェクトが閉じている場合のみです。  
  
 **ストリーム**オブジェクトの場合、アクセスモードが指定されていない場合は、**ストリーム**オブジェクトを開くために使用されるソースから継承されます。 たとえば、**レコード**オブジェクトから**ストリーム**が開かれている場合、既定では、**レコード**と同じモードで開かれます。  
  
 オブジェクトが開いている間は、オブジェクトが閉じられ、読み取り専用になっている間、このプロパティは読み取り/書き込み可能です。  
  
> [!NOTE]
>  **リモートデータサービスの使用状況** クライアント側の **接続** オブジェクトで使用する場合、 **Mode** プロパティは **admodeunknown**にのみ設定できます。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Connection オブジェクト (ADO)](./connection-object-ado.md)  
    :::column-end:::
    :::column:::
        [Record オブジェクト (ADO)](./record-object-ado.md)  
    :::column-end:::
    :::column:::
        [Stream オブジェクト (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [IsolationLevel と Mode プロパティの例 (VB)](./isolationlevel-and-mode-properties-example-vb.md)   
 [IsolationLevel と Mode プロパティの例 (VC + +)](./isolationlevel-and-mode-properties-example-vc.md)