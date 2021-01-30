---
description: LoadFromFile メソッド (ADO)
title: LoadFromFile メソッド (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: reference
apitype: COM
f1_keywords:
- _Stream::raw_LoadFromFile
helpviewer_keywords:
- LoadFromFile method [ADO]
ms.assetid: b18d8d38-7354-4a94-b637-6ac035faa433
author: rothja
ms.author: jroth
ms.openlocfilehash: ec0b77ba5588ffb13420970a41036e40757af51e
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99167170"
---
# <a name="loadfromfile-method-ado"></a>LoadFromFile メソッド (ADO)
既存のファイルの内容を [ストリーム](./stream-object-ado.md)に読み込みます。  
  
## <a name="syntax"></a>構文  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>パラメーター  
 *FileName*  
 **ストリーム** に読み込むファイルの名前を含む **文字列** 値です。 *FileName* には、任意の有効なパスと名前を UNC 形式で含めることができます。 指定したファイルが存在しない場合は、実行時エラーが発生します。  
  
## <a name="remarks"></a>コメント  
 このメソッドを使用すると、ローカルファイルの内容を **ストリーム** オブジェクトに読み込むことができます。 これは、ローカルファイルの内容をサーバーにアップロードするために使用できます。  
  
 **LoadFromFile** を呼び出す前に、**ストリーム** オブジェクトが既に開かれている必要があります。 このメソッドは、**ストリーム** オブジェクトのバインディングを変更しません。それでも、**ストリーム** が最初に開かれた URL または **レコード** で指定されたオブジェクトにバインドされます。  
  
 **LoadFromFile** は、ファイルから読み取ったデータを使用して、 **ストリーム** オブジェクトの現在の内容を上書きします。 **ストリーム** 内の既存のバイトは、ファイルの内容によって上書きされます。 **LoadFromFile** によって作成された [EOS](./eos-property.md)の後にある既存のバイトと残りのバイトは、切り捨てられます。  
  
 **LoadFromFile** の呼び出しの後、現在の位置は **ストリーム** の先頭に設定されます ([position](./position-property-ado.md)は 0)。  
  
 エンコードのためにストリームの先頭に2バイトが追加される可能性があるため、ストリームのサイズが、読み込み元のファイルのサイズと完全に一致しない場合があります。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)