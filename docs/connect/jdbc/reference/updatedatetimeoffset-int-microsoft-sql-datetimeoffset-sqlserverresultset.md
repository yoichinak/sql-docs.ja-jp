---
description: updateDateTimeOffset(int, microsoft.sql.DateTimeOffset) (SQLServerResultSet)
title: updateDateTimeOffset(int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 21ec0054-c808-4e88-9c8d-c71b696ce658
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 121dd26097d657cad2fa1ba71ec17a42b27cb87c
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99188132"
---
# <a name="updatedatetimeoffsetint-microsoftsqldatetimeoffset-sqlserverresultset"></a>updateDateTimeOffset(int, microsoft.sql.DateTimeOffset) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  このメソッドは [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 で追加されました。  
  
 0 から始まる列の序数を使用して、指定された列の値を [DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)値に更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateDateTimeOffset(int index, microsoft.sql.DateTimeOffset x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *インデックス*  
  
 列の 0 から始まる序数です。  
  
 *x*  
  
 [DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md) オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 [DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)値は [SQLServerResultSet.getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md) を使用して取得できます。  
  
## <a name="see-also"></a>参照  
 [updateDateTimeOffset &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
