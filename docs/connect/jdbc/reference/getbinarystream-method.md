---
description: getBinaryStream () メソッド
title: getBinaryStream メソッド () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerBlob.getBinaryStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0c8f7741-daba-4c04-adc0-8d76345a899a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b78ce33cb395b4d55cc71559a4a3859a85b17200
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99168217"
---
# <a name="getbinarystream-method-"></a>getBinaryStream () メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  BLOB からデータを読み取る入力ストリームを返します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.io.InputStream getBinaryStream()  
```  
  
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
  
  
