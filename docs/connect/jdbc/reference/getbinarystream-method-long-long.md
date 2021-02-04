---
description: getBinaryStream (long, long) メソッド
title: getBinaryStream メソッド (long, long) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 30bc8882-04b4-4efd-95e4-7d3a2a8c1d47
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da3fcf0ab4e97c19458981feea8f7e2af4c5a133
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99168223"
---
# <a name="getbinarystream-method-long-long"></a>getBinaryStream (long, long) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定された開始位置と長さを使用して、部分的な BLOB 値を含む入力ストリーム オブジェクトを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.io.InputStream getBinaryStream(long pos, long length)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *pos*  
  
 取得する部分的な値の最初のバイトへのオフセットです。  
  
 *length*  
  
 取得する部分的な値の長さ (バイト単位) です。  
  
## <a name="return-value"></a>戻り値  
 BLOB データを格納している入力ストリームです。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getBinaryStream メソッドは、java.sql.Blob インターフェイスの getBinaryStream メソッドで規定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerBlob のメソッド](../../../connect/jdbc/reference/sqlserverblob-methods.md)   
 [SQLServerBlob のメンバー](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [SQLServerBlob クラス](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
