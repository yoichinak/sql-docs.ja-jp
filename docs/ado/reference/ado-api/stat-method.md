---
description: Stat メソッド
title: Stat メソッド |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Stat
helpviewer_keywords:
- Stat method [ADO]
ms.assetid: 99a2b2d4-e6b1-4205-b011-72d024ea7240
author: rothja
ms.author: jroth
ms.openlocfilehash: db386d8e39c57883c7e456962d57e884383d62ff
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988853"
---
# <a name="stat-method"></a>Stat メソッド
[ストリーム](./stream-object-ado.md)オブジェクトに関する情報を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>戻り値  
 操作の状態を示す **Long 型** の値。  
  
#### <a name="parameters"></a>パラメーター  
 *StatStg*  
 ストリームに関する情報が格納される STATSTG 構造体。 ADO ストリームオブジェクトによって使用される **Stat** メソッドの実装では、構造体のすべてのフィールドが格納されるわけではありません。  
  
 *StatFlag*  
 このメソッドが STATSTG 構造体の一部のメンバーを返さないことを指定します。これにより、メモリ割り当て操作が保存されます。 値は STATFLAG 列挙体から取得されます。 STATFLAG 列挙体には2つの値があります  
  
|定数|値|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>解説  
 ADO Stream オブジェクトに実装されている Stat メソッドのバージョンは、STATSTG 構造体の次のフィールドに入力します。  
  
 *pwcsName*  
 ストリームの名前が含まれていて、StatFlag 値 STATFLAG_NONAME が指定されていない場合は、その名前を格納している文字列。  
  
 *cbSize*  
 ストリームまたはバイト配列のサイズをバイト単位で指定します。  
  
 *mtime*  
 ストレージ、ストリーム、またはバイト配列に対する最後の変更時刻を示します。  
  
 *ctime*  
 ストレージ、ストリーム、またはバイト配列の作成時刻を示します。  
  
 *atime*  
 ストレージ、ストリーム、またはバイト配列に対する最後のアクセス時刻を示します。  
  
 StatFlag パラメーターに STATFLAG_NONAME が指定されている場合、ストリームの名前は返されません。  
  
 StatFlag パラメーターに STATFLAG_NONAME が指定されておらず、現在のストリームに使用できる名前がない場合、この値は E_NOTIMPL になります。  
  
## <a name="applies-to"></a>適用対象  
 [Stream オブジェクト (ADO)](./stream-object-ado.md)