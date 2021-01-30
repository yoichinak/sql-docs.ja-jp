---
description: CommandTimeout プロパティ (ADO)
title: CommandTimeout プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- Command15::CommandTimeout
helpviewer_keywords:
- CommandTimeout property [ADO]
ms.assetid: c611f857-d6b0-4dca-8925-f4a02e769eb0
author: rothja
ms.author: jroth
ms.openlocfilehash: aa12f6e7c6e2451f6323f4d25dfed6894d7b5c26
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99171465"
---
# <a name="commandtimeout-property-ado"></a>CommandTimeout プロパティ (ADO)
コマンドの実行中に、試行を終了してエラーを生成するまでの待機時間を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 コマンドの実行を待機する時間を秒単位で示す **Long 型** の値を設定または返します。 既定値は 30 です。  
  
## <a name="remarks"></a>コメント  
 [接続](./connection-object-ado.md)オブジェクトまたは [コマンド](./command-object-ado.md)オブジェクトの **CommandTimeout** プロパティを使用して、ネットワークトラフィックまたはサーバーの使用量の遅延が原因で [Execute](./execute-method-ado-command.md)メソッド呼び出しをキャンセルできるようにします。 コマンドの実行が完了する前に、 **CommandTimeout** プロパティに設定された間隔が経過すると、エラーが発生し、ADO によってコマンドがキャンセルされます。 このプロパティを0に設定すると、ADO は実行が完了するまで無制限に待機します。 コードを記述しているプロバイダーとデータソースで、 **CommandTimeout** 機能がサポートされていることを確認します。  
  
 **接続** オブジェクトの **CommandTimeout** 設定は、同じ **接続** 上の **Command** オブジェクトの **CommandTimeout** 設定には影響しません。つまり、 **Command** オブジェクトの **CommandTimeout** プロパティは、 **Connection** オブジェクトの **CommandTimeout** 値の値を継承しません。  
  
 **接続オブジェクトで** は、**接続** が開かれると、 **CommandTimeout** プロパティは読み取り/書き込みのままになります。  
  
## <a name="applies-to"></a>適用対象  

:::row:::
    :::column:::
        [Command オブジェクト (ADO)](./command-object-ado.md)  
    :::column-end:::
    :::column:::
        [Connection オブジェクト (ADO)](./connection-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>参照  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (VB)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (VC + +)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (JScript)](./activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [ConnectionTimeout プロパティ (ADO)](./connectiontimeout-property-ado.md)