---
description: getString (int) メソッド (SQLServerResultSet)
title: getString メソッド (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerResultSet.getString (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bfa493c4-fe07-449b-b4d0-384e1a1fce48
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d679ea82b07c7df4aef09b47c7cc74e537a94070
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99174968"
---
# <a name="getstring-method-int-sqlserverresultset"></a>getString (int) メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトの現在の行にある指定された列インデックスの値が、Java プログラミング言語の **String** として取得されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public java.lang.String getString(int columnIndex)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *columnIndex*  
  
 列インデックスを示す **int** です。  
  
## <a name="return-value"></a>戻り値  
 **文字列** 値です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この getString メソッドは、java.sql.ResultSet インターフェイスの getString メソッドで規定されています。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 内のすべての列を文字列として返すことができます。 つまり、数値ベースと文字ベースのすべての型の **String** 表現、および binary、varbinary、varbinary(max)、image、timestamp、uniqueidentifier などのバイナリ列の 16 進形式の文字列表現を返すことができます。  
  
 money、smallmoney、datetime、smalldatetime、float、real、decimal、numeric などの地域依存の型では、その型の基になる値に対する標準の toString() 形式が返されます。  
  
 ユーザー定義型は、16 進形式の **String** 値として返されます。  
  
## <a name="see-also"></a>参照  
 [getString メソッド &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)   
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
