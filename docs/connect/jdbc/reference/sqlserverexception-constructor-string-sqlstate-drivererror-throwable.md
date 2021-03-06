---
description: SQLServerException コンストラクター (java.lang.String、SQLState、DriverError、java.lang.Throwable)
title: SQLServerException コンストラクター (java.lang.String、SQLState、DriverError、java.lang.Throwable) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bce4ace9692a7a94f2c828b18096ef558cc9efc3
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99176614"
---
# <a name="sqlserverexception-constructor-javalangstring-sqlstate-drivererror-javalangthrowable"></a>SQLServerException コンストラクター (java.lang.String、SQLState、DriverError、java.lang.Throwable)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  **string** オブジェクト、**sqlstate** オブジェクト、**drivererror** オブジェクト、および **throwable** オブジェクトが渡されたときに、[SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) クラスの新しいインスタンスが初期化されます。

## <a name="syntax"></a>構文  
  
```  
public SQLServerException(java.lang.String errText,
            SQLState sqlState,
            DriverError driverError,
            java.lang.Throwable cause)
            
```  
  
#### <a name="parameters"></a>パラメーター  
 *errText*  
  
 エラー テキストを保持する文字列。
  
 *sqlState*  
  
 SQL 状態を保持する列挙型オブジェクト。
 
 *driverError*  
  
 ドライバー エラーを保持する列挙型オブジェクト。
 
 *cause*  
  
 例外の原因を保持する throwable オブジェクト。
  
## <a name="see-also"></a>参照  
 [SQLServerException のコンストラクター](../../../connect/jdbc/reference/sqlserverexception-constructors.md)   
 [SQLServerException のメンバー](../../../connect/jdbc/reference/sqlserverexception-members.md)   
 [SQLServerException クラス](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
  
