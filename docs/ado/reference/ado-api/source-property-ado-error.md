---
description: Source プロパティ (ADO Error)
title: Source プロパティ (ADO Error) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::get_Source
- Error::Source
- Error::GetSource
helpviewer_keywords:
- Source property [ADO Error]
ms.assetid: 4044ba15-f013-4c4c-9fe1-b4410fe9a778
author: rothja
ms.author: jroth
ms.openlocfilehash: 117e6e1f16800daaf94cba6e4a7643d5aa1c8c1f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988983"
---
# <a name="source-property-ado-error"></a>Source プロパティ (ADO Error)
最初にエラーを生成したオブジェクトまたはアプリケーションの名前を示します。  
  
## <a name="return-value"></a>戻り値  
 オブジェクトまたはアプリケーションの名前を示す **文字列** 値を返します。  
  
## <a name="remarks"></a>解説  
 [エラーオブジェクトの](./error-object.md) **Source**プロパティを使用して、最初にエラーを生成したオブジェクトまたはアプリケーションの名前を確認します。 オブジェクトのクラス名またはプログラム ID を指定できます。 ADO のエラーの場合、プロパティ値は ADODB になり **ます。**_Objectname_。ここで、 *objectname* はエラーを発生させたオブジェクトの名前です。 ADOX と ADO MD の場合、この値は **adox になります。**_ObjectName_ と **ADOMD。**_ObjectName_。  
  
 **Error オブジェクトの** **Source**、 [Number](./number-property-ado.md)、 [Description](./description-property.md)プロパティからのエラードキュメントに基づいて、エラーを適切に処理するコードを記述できます。  
  
 **Source**プロパティは、**エラー**オブジェクトの場合は読み取り専用です。  
  
## <a name="applies-to"></a>適用対象  
 [Error オブジェクト](./error-object.md)  
  
## <a name="see-also"></a>参照  
 [Description、HelpContext、HelpFile、のエラー、Number、Source、および SQLState プロパティの例 (VB)](./description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpContext、HelpFile、のエラー、Number、Source、および SQLState プロパティの例 (VC + +)](./description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description プロパティ](./description-property.md)   
 [HelpContext、HelpFile プロパティ](./helpcontext-helpfile-properties.md)   
 [Number プロパティ (ADO)](./number-property-ado.md)   
 [Source プロパティ (ADO Record)](./source-property-ado-record.md)   
 [Source プロパティ (ADO Recordset)](./source-property-ado-recordset.md)