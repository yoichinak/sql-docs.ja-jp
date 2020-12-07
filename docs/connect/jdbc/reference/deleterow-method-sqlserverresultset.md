---
description: deleteRow メソッド (SQLServerResultSet)
title: deleteRow メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.deleteRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aa04a644-c7c2-4738-8b6e-7fea566d2c16
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9302a3ee26137c693f4711fc5501c5b715b16a71
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437844"
---
# <a name="deleterow-method-sqlserverresultset"></a>deleteRow メソッド (SQLServerResultSet)

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトから、および基になるデータベースから、現在の行を削除します。  
  
## <a name="syntax"></a>構文  
  
```cpp
public void deleteRow()  
```  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この deleteRow メソッドは、java.sql.ResultSet インターフェイスの deleteRow メソッドで規定されています。  
  
 カーソルが挿入行にあるときは、このメソッドを呼び出すことができません。  
  
 キーセット カーソルを使っている場合、このメソッドにより結果セットに空白が残されます。 [rowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) メソッドを使用すると、この空白を検出できます。 結果セット内の行の行番号は変更されません。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
