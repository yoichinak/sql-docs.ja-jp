---
description: getMaxFieldSize メソッド (SQLServerStatement)
title: getMaxFieldSize メソッド (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerStatement.getMaxFieldSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ed7bbcb8-660b-4e9b-8241-e216c42826f9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b1cbb5bb3cb35b4286a0b822168c9991c228576
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99162803"
---
# <a name="getmaxfieldsize-method-sqlserverstatement"></a>getMaxFieldSize メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトによって生成される [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの文字列やバイナリ列の値に対して返すことができる最大バイト数を取得します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public final int getMaxFieldSize()  
```  
  
## <a name="return-value"></a>戻り値  
 列に格納できる最大バイト数を示す **int** です。制限しない場合は 0 です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getMaxFieldSize メソッドは、java.sql.Statement インターフェイスの getMaxFieldSize メソッドで指定されています。  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメソッド](../../../connect/jdbc/reference/sqlserverstatement-methods.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
