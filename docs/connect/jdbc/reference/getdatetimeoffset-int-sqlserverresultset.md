---
description: getDateTimeOffset(int) (SQLServerResultSet)
title: getDateTimeOffset(int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.assetid: 60abf83d-6f97-4e47-b9d3-5072bd09d869
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 180cb9907d011eed7fb4054f4d5dbe6221882fd6
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99163174"
---
# <a name="getdatetimeoffsetint-sqlserverresultset"></a>getDateTimeOffset(int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  このメソッドは [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 で追加されました。  
  
 パラメーターに渡されたインデックスを使用して、指定された列の値が Java プログラミング言語の [DateTimeOffset Class](../../../connect/jdbc/reference/datetimeoffset-class.md) オブジェクトとして取得されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public microsoft.sql.DateTimeOffset getDateTimeOffset(int columnIndex)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnIndex*  
  
 列の序数。  
  
## <a name="return-value"></a>戻り値  
 [DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md) オブジェクト。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 [DateTimeOffset クラス](../../../connect/jdbc/reference/datetimeoffset-class.md)値は [SQLServerResultSet.updateDateTimeOffset](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md) を使用して取得できます。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
