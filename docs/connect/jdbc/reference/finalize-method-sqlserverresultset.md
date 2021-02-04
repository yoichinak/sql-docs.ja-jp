---
description: finalize メソッド (SQLServerResultSet)
title: finalize メソッド (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerResultSet.finalize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 49bc879d-822b-42da-bc20-2394865f1f0f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 71dc58e3172657a480aa5465e48010953c32fc83
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99168442"
---
# <a name="finalize-method-sqlserverresultset"></a>finalize メソッド (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトを明示的に閉じます。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void finalize()  
```  
  
## <a name="remarks"></a>解説  
 アプリケーションが閉じていない場合は、結果セットを閉じます。 このメソッドは JDBC 仕様に準拠するためにだけ存在します。 Java 仮想マシン (JVM) ではファイナライザーがいつ実行されるかが保証されないため、明示的に結果セットを閉じてないアプリケーションは、別のステートメント (同じ接続を使用し、行ロックなどの共通のサーバー リソースでブロックされているステートメント) でもデッドロックする可能性があります。  
  
## <a name="see-also"></a>参照  
 [SQLServerResultSet のメンバー](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [SQLServerResultSet クラス](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
