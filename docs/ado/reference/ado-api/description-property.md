---
title: Description プロパティ |Microsoft Docs
description: エラーの説明を含む文字列値を返す ADO の Error オブジェクトの description プロパティについて説明します。
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Description
- Error::GetDescription
- Error::get_Description
helpviewer_keywords:
- Description property
ms.assetid: 4b5d6790-6c29-42aa-bf78-d9cfb8ad7965
author: rothja
ms.author: jroth
ms.openlocfilehash: 7060810eba49ad5e1b9385a090788690b43e07eb
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973913"
---
# <a name="description-property"></a>Description プロパティ
[エラー](../../../ado/reference/ado-api/error-object.md)オブジェクトについて説明します。  
  
## <a name="return-value"></a>戻り値  
 エラーの説明を含む **文字列** 値を返します。  
  
## <a name="remarks"></a>解説  
 **Description**プロパティを使用して、エラーの簡単な説明を取得します。 このプロパティを表示して、処理できない、または処理したくないエラーをユーザーに通知します。 文字列は、ADO またはプロバイダーから取得されます。  
  
 プロバイダーは、ADO に特定のエラーテキストを渡す役割を担います。 ADO は、受信したプロバイダーエラーまたは警告ごとに [エラー](../../../ado/reference/ado-api/error-object.md) オブジェクトを **エラーコレクションに** 追加します。 **エラー**コレクションを列挙して、プロバイダーが成功したエラーをトレースします。  
  
## <a name="applies-to"></a>適用対象  
 [Error オブジェクト](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>参照  
 [Description、HelpContext、HelpFile、のエラー、Number、Source、および SQLState プロパティの例 (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description、HelpContext、HelpFile、のエラー、Number、Source、および SQLState プロパティの例 (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [HelpContext、HelpFile プロパティ](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Number プロパティ (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source プロパティ (ADO Error)](../../../ado/reference/ado-api/source-property-ado-error.md)
