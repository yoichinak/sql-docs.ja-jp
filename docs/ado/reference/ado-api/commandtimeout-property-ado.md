---
description: CommandTimeout プロパティ (ADO)
title: CommandTimeout プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandTimeout
helpviewer_keywords:
- CommandTimeout property [ADO]
ms.assetid: c611f857-d6b0-4dca-8925-f4a02e769eb0
author: rothja
ms.author: jroth
ms.openlocfilehash: 280e454291ebbf656b177c4a2be2773a7057f312
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975153"
---
# <a name="commandtimeout-property-ado"></a>CommandTimeout プロパティ (ADO)
コマンドの実行中に、試行を終了してエラーを生成するまでの待機時間を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 コマンドの実行を待機する時間を秒単位で示す **Long 型** の値を設定または返します。 既定値は 30 です。  
  
## <a name="remarks"></a>解説  
 [接続](./connection-object-ado.md)オブジェクトまたは[コマンド](./command-object-ado.md)オブジェクトの**CommandTimeout**プロパティを使用して、ネットワークトラフィックまたはサーバーの使用量の遅延が原因で[Execute](./execute-method-ado-command.md)メソッド呼び出しをキャンセルできるようにします。 コマンドの実行が完了する前に、 **CommandTimeout** プロパティに設定された間隔が経過すると、エラーが発生し、ADO によってコマンドがキャンセルされます。 このプロパティを0に設定すると、ADO は実行が完了するまで無制限に待機します。 コードを記述しているプロバイダーとデータソースで、 **CommandTimeout** 機能がサポートされていることを確認します。  
  
 **接続**オブジェクトの**CommandTimeout**設定は、同じ**接続**上の**Command**オブジェクトの**CommandTimeout**設定には影響しません。つまり、 **Command**オブジェクトの**CommandTimeout**プロパティは、 **Connection**オブジェクトの**CommandTimeout**値の値を継承しません。  
  
 **接続オブジェクトで**は、**接続**が開かれると、 **CommandTimeout**プロパティは読み取り/書き込みのままになります。  
  
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