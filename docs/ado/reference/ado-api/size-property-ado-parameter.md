---
description: Size プロパティ (ADO Parameter)
title: Size プロパティ (ADO Parameter) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::Size
helpviewer_keywords:
- Size property [ADO Parameter]
ms.assetid: e6bad449-ebdb-4dd3-886a-9e6f1e7ee5d2
author: rothja
ms.author: jroth
ms.openlocfilehash: 914f751c4bfd48755470ce3da9e994dae4a33477
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989123"
---
# <a name="size-property-ado-parameter"></a>Size プロパティ (ADO Parameter)
[パラメーター](./parameter-object.md)オブジェクトの最大サイズをバイト数または文字数で示します。  
  
## <a name="settings-and-return-values"></a>設定と戻り値  
 **パラメーター**オブジェクトの値の最大サイズをバイトまたは文字単位で示す**Long 型**の値を設定または返します。  
  
## <a name="remarks"></a>解説  
 **Size**プロパティを使用して、**パラメーター**オブジェクトの[Value](./value-property-ado.md)プロパティに対して書き込みまたは読み取りを行う値の最大サイズを決定します。  
  
 **パラメーター**オブジェクトに可変長データ型 (たとえば、 **adVarChar**などの任意の**文字列**型) を指定する場合は、[パラメーター](./parameters-collection-ado.md)コレクションに追加する前に、オブジェクトの**Size**プロパティを設定する必要があります。それ以外の場合は、エラーが発生します。  
  
 **Parameter**オブジェクトを[Command](./command-object-ado.md)オブジェクトの**Parameters**コレクションに既に追加していて、その型を可変長データ型に変更した場合は、 **command**オブジェクトを実行する前に、**パラメーター**オブジェクトの**Size**プロパティを設定する必要があります。それ以外の場合は、エラーが発生します。  
  
 [Refresh](./refresh-method-ado.md)メソッドを使用してプロバイダーからパラメーター情報を取得し、1つまたは複数の可変長データ型**パラメーター**オブジェクトを返す場合、ADO では、可能な最大サイズに基づいてパラメーターにメモリが割り当てられるため、実行中にエラーが発生する可能性があります。 エラーを回避するには、コマンドを実行する前に、これらのパラメーターの **Size** プロパティを明示的に設定する必要があります。  
  
 **Size**プロパティは読み取り/書き込み可能です。  
  
## <a name="applies-to"></a>適用対象  
 [Parameter オブジェクト](./parameter-object.md)  
  
## <a name="see-also"></a>参照  
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (VB)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vb.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (VC + +)](./activeconnection-commandtext-commandtimeout-commandtype-size-example-vc.md)   
 [ActiveConnection、CommandText、CommandTimeout、CommandType、Size、Direction プロパティの例 (JScript)](./activeconnection-commandtext-timeout-type-size-example-jscript.md)   
 [Size プロパティ (ADO Stream)](./size-property-ado-stream.md)