---
description: updateTimestamp (int, java.sql.Timestamp) メソッド
title: updateTimestamp (int, java.sql.Timestamp) メソッド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerResultSet.updateTimestamp (int, java.sql.Timestamp)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db83d9d7-137b-4a28-a2ca-d4782e0a256e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22b49a0b3196dae702515aaa456ad4fb89bb7fa2
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99195698"
---
# <a name="updatetimestamp-method-int-javasqltimestamp"></a>updateTimestamp (int, java.sql.Timestamp) メソッド
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された列インデックスを使用して、指定された列をタイムスタンプ値で更新します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void updateTimestamp(int index,  
                            java.sql.Timestamp x)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *インデックス*  
  
 列インデックスを示す **int** です。  
  
 *x*  
  
 タイムスタンプ値です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この updateTimestamp メソッドは、java.sql.ResultSet インターフェイスの updateTimestamp メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [updateTimestamp メソッド (SQLServerResultSet)](../../../connect/jdbc/reference/updatetimestamp-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
