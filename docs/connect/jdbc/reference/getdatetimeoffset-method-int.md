---
description: getDateTimeOffset (int) メソッド
title: getDateTimeOffset (int) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 8bb00356-4d6e-4625-b924-67646930fdf2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e1c1132c0fd7d788636cedb8cdf5eb9f2ea55f0
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99163198"
---
# <a name="getdatetimeoffset-method-int"></a>getDateTimeOffset (int) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  このメソッドは [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 で追加されました。  
  
 パラメーターに渡されたインデックスを使用して、指定されたパラメーターの値が Java プログラミング言語の [DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)のオブジェクトとして取得されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(int index)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *インデックス*  
  
 1 から始まるパラメーターの序数。  
  
## <a name="return-value"></a>戻り値  
 [DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md) オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 [DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md) パラメーターは [SQLServerCallableStatement.setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlservercallablestatement.md) を使用して設定できます。  
  
## <a name="see-also"></a>参照  
 [getDateTimeOffset メソッド &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdatetimeoffset-method-sqlservercallablestatement.md)   
 [SQLServerCallableStatement のメンバー](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [SQLServerCallableStatement クラス](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
