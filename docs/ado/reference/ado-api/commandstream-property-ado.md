---
description: CommandStream プロパティ (ADO)
title: CommandStream プロパティ (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Command::CommandStream
helpviewer_keywords:
- CommandStream property [ADO]
ms.assetid: f78f61b6-87e0-48dc-961e-83d0e20da58e
author: rothja
ms.author: jroth
ms.openlocfilehash: 463468f8e39d1187a36ac6fa1279e8a2aeb3a73b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975203"
---
# <a name="commandstream-property-ado"></a>CommandStream プロパティ (ADO)
[Command](./command-object-ado.md)オブジェクトの入力として使用されるストリームを示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 **Command**オブジェクトの入力として使用されるストリームを設定または返します。 このストリームの形式はプロバイダー固有です。詳細については、プロバイダーのドキュメントを参照してください。 このプロパティは、**コマンド**の入力の文字列を指定するために使用される[CommandText](./commandtext-property-ado.md)プロパティに似ています。  
  
## <a name="remarks"></a>解説  
 **Commandstream** と **CommandText** は相互に排他的です。 ユーザーが **Commandstream** プロパティを設定すると、 **CommandText** プロパティが空の文字列 ("") に設定されます。 ユーザーが **CommandText** プロパティを設定した場合、 **Commandstream** プロパティは **Nothing**に設定されます。  
  
 コマンドの動作。 **パラメーターの更新** とコマンドの **Prepare** メソッドは、プロバイダーによって定義されます。 ストリーム内のパラメーターの値は更新できません。  
  
 入力ストリームは、 **コマンド**のソースを返す他の ADO オブジェクトでは使用できません。 たとえば、[レコード](./recordset-object-ado.md)セットの[ソース](./source-property-ado-recordset.md)が、入力としてストリームを持つ**コマンド**オブジェクトに設定されている場合、 **commandstream**プロパティのストリームコンテンツではなく、空の文字列 ("") を含む**CommandText**プロパティが返されます **。**  
  
 コマンドストリーム ( **commandstream**で指定) を使用する場合、 [CommandType](./commandtype-property-ado.md)プロパティに有効な[Commandtypeenum](./commandtypeenum.md)値は**adcmdtext**と**adcmdtext**だけです。 それ以外の値を指定すると、エラーが発生します。  
  
## <a name="applies-to"></a>適用対象  
 [Command オブジェクト (ADO)](./command-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [CommandText プロパティ (ADO)](./commandtext-property-ado.md)   
 [言語プロパティ](./dialect-property.md)   
 [CommandTypeEnum](./commandtypeenum.md)