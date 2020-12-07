---
description: SaveToFile メソッド
title: SaveToFile メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SaveToFile
- _Stream::SaveToFile
helpviewer_keywords:
- SaveToFile method [ADO]
ms.assetid: 8a8594f2-422b-4d2e-94f8-7fe337445900
author: rothja
ms.author: jroth
ms.openlocfilehash: 6aa3269e73f9823eb47dddeb039b62e3affdd3c6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88989293"
---
# <a name="savetofile-method"></a>SaveToFile メソッド
[ストリーム](./stream-object-ado.md)のバイナリコンテンツをファイルに保存します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>パラメーター  
 *FileName*  
 **ストリーム**の内容の保存先となるファイルの完全修飾名を含む**文字列**値です。 任意の有効なローカルの場所、または UNC 値を使用してアクセスできる任意の場所に保存できます。  
  
 *System.xml.linq.saveoptions>*  
 新しいファイルがまだ存在しない場合に、新しいファイルを**SaveToFile**によって作成するかどうかを指定する[Saveoptionsenum](./saveoptionsenum.md)値。 既定値は **adSaveCreateNotExists**です。 これらのオプションを使用すると、指定したファイルが存在しない場合にエラーが発生するように指定できます。 また、 **SaveToFile** が既存のファイルの現在の内容を上書きするように指定することもできます。  
  
> [!NOTE]
>  既存のファイルを上書きする場合 ( **adSaveCreateOverwrite** が設定されている場合)、 **SaveToFile** は新しい [EOS](./eos-property.md)の後にある元の既存のファイルからすべてのバイトを切り捨てます。  
  
## <a name="remarks"></a>解説  
 **SaveToFile** は、 **ストリーム** オブジェクトの内容をローカルファイルにコピーするために使用できます。 **ストリーム**オブジェクトの内容またはプロパティに変更はありません。 **ストリーム**オブジェクトは、 **SaveToFile**を呼び出す前に開いている必要があります。  
  
 このメソッドは、 **ストリーム** オブジェクトと基になるソースとの関連付けを変更しません。 **ストリーム**オブジェクトは、開いたときにソースであった元の URL または**レコード**と関連付けられたままになります。  
  
 **SaveToFile**操作の後、ストリーム内の現在位置 ([位置](./position-property-ado.md)) がストリームの先頭 (0) に設定されます。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)  
  
## <a name="see-also"></a>参照  
 [Open メソッド (ADO Stream)](./open-method-ado-stream.md)   
 [Save メソッド](./save-method.md)