---
description: setBytes (long, byte) メソッド
title: setBytes メソッド (long, byte) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerBlob.setBytes (long.byte[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ffb8f107-0f9d-4410-957f-62b718e1e872
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2329bb9598c56ecabb7282faaf6b7b7f5565b068
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99173763"
---
# <a name="setbytes-method-long-byte"></a>setBytes (long, byte) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された byte 配列を、渡された位置から BLOB に書き込み、書き込んだバイト数を返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public int setBytes(long pos,  
                    byte[] bytes)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *pos*  
  
 データの書き込みを開始する BLOB 内の位置 (1 から開始) です。  
  
 *bytes*  
  
 BLOB に書き込む byte 配列です。  
  
## <a name="return-value"></a>戻り値  
 書き込んだバイト数を示す **long** 値です。  
  
## <a name="exceptions"></a>例外  
 java.sql.SQLException  
  
## <a name="remarks"></a>解説  
 この setBytes メソッドは、java.sql.Blob インターフェイスの setBytes メソッドで指定されています。  
  
 データは指定された開始位置から上書きされ、BLOB の初期データの長さをオーバーランすることができます。 開始位置に BLOB の長さ + 1 の値を指定すると、バイトが追加されます。 開始位置に BLOB の長さ + 2 以上 (または 0 以下) の値を渡すと、位置のエラーがスローされます。 長さ 0 の **byte** 配列を渡すと、0 が返されます。これはバイトが書き込まれなかったためです。  
  
## <a name="see-also"></a>参照  
 [setBytes メソッド &#40;SQLServerBlob&#41;](../../../connect/jdbc/reference/setbytes-method-sqlserverblob.md)   
 [SQLServerBlob のメソッド](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob のメンバー](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob クラス](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
