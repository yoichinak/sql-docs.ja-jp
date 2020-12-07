---
description: CommandType プロパティ (ADO)
title: CommandType プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Command15::CommandType
helpviewer_keywords:
- CommandType property [ADO]
ms.assetid: ca44809c-8647-48b6-a7fb-0be70a02f53e
author: rothja
ms.author: jroth
ms.openlocfilehash: a8d92e54d88ede66f5c5f6c3c2a74bd5f0b66af0
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975113"
---
# <a name="commandtype-property-ado"></a>CommandType プロパティ (ADO)
[Command](./command-object-ado.md)オブジェクトの種類を示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 1つ以上の [Commandtypeenum](./commandtypeenum.md) 値を設定または返します。  
  
> [!NOTE]
>  **Adcmdfile**の**commandtypeenum**値、または**CommandType**と共に**adcmdtabledirect**を使用しないでください。 これらの値は、[レコードセット](./recordset-object-ado.md)の[Open](./open-method-ado-recordset.md)メソッドおよび[Requery](./requery-method.md)メソッドでオプションとしてのみ使用できます。  
  
## <a name="remarks"></a>解説  
 **CommandType**プロパティを使用して、 [CommandText](./commandtext-property-ado.md)プロパティの評価を最適化します。  
  
 **CommandType**プロパティ値が既定値の**adcmdunknown**に設定されている場合、 **ado.net プロパティが**SQL ステートメント、ストアドプロシージャ、またはテーブル名であるかどうかを確認するために ADO がプロバイダーの呼び出しを行う必要があるため、パフォーマンスが低下する可能性があります。 使用しているコマンドの種類がわかっている場合は、 **CommandType** プロパティを設定することによって、関連するコードに直接アクセスするように ADO に指示します。 **CommandType**プロパティが**CommandText**プロパティ内のコマンドの型と一致しない場合、 [Execute](./execute-method-ado-command.md)メソッドを呼び出すとエラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Command オブジェクト (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (VB)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (VC + +)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (JScript)](./activeconnection-commandtext-timeout-type-size-example-jscript.md)