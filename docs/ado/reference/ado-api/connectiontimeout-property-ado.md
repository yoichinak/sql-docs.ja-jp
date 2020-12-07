---
description: ConnectionTimeout プロパティ (ADO)
title: ConnectionTimeout プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Connection15::ConnectionTimeout
helpviewer_keywords:
- ConnectionTimeout property [ADO]
ms.assetid: 8904a403-1383-4b4b-b53d-5c01d6f5deac
author: rothja
ms.author: jroth
ms.openlocfilehash: bd8fd11c017583ef49981021688210245589e971
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88974743"
---
# <a name="connectiontimeout-property-ado"></a>ConnectionTimeout プロパティ (ADO)
接続の確立中に、試行を終了してエラーを生成するまでの待機時間を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 接続を開くまでの待機時間を秒単位で示す **Long 型** の値を設定または返します。 既定値は 15 です。  
  
## <a name="remarks"></a>解説  
 ネットワークトラフィックまたはサーバーが過負荷になっている場合[は、接続オブジェクトの](./connection-object-ado.md) **ConnectionTimeout**プロパティを使用して、接続試行を破棄する必要があります。 接続を開始する前に **ConnectionTimeout** プロパティの設定から経過した時間が経過すると、エラーが発生し、ADO は試行をキャンセルします。 このプロパティを0に設定した場合、ADO は接続が開かれるまで無制限に待機します。 コードを記述しているプロバイダーで、 **ConnectionTimeout** 機能がサポートされていることを確認します。  
  
 **ConnectionTimeout**プロパティは、接続が閉じられている場合は読み取り/書き込みが、開いている場合は読み取り専用になります。  
  
## <a name="applies-to"></a>適用対象  
 [Connection オブジェクト (ADO)](./connection-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [ConnectionString、ConnectionTimeout、State プロパティの例 (VB)](./connectionstring-connectiontimeout-and-state-properties-example-vb.md)   
 [ConnectionString、ConnectionTimeout、State プロパティの例 (VC + +)](./connectionstring-connectiontimeout-and-state-properties-example-vc.md)   
 [CommandTimeout プロパティ (ADO)](./commandtimeout-property-ado.md)