---
description: setAsciiStream (int, java.io.InputStream) メソッド
title: setAsciiStream メソッド (int, java.io.InputStream) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 02c2443d-44e1-4f16-a0d5-08d197838214
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 34d525f1141764ae07dcd28cf78776e05b967b6e
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99174041"
---
# <a name="setasciistream-method-int-javaioinputstream"></a>setAsciiStream (int, java.io.InputStream) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  指定されたパラメーターの番号を、渡された java.io.InputStream オブジェクトに設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final void setAsciiStream(int parameterIndex,  
                                 java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *parameterIndex*  
  
 パラメーターの番号を示す **int** です。  
  
 *x*  
  
 java.io.InputStream オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setAsciiStream メソッドは、java.sql.PreparedStatement インターフェイスの setAsciiStream メソッドによって指定されます。  
  
## <a name="see-also"></a>参照  
 [setAsciiStream メソッド &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)   
 [SQLServerPreparedStatement のメンバー](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  
