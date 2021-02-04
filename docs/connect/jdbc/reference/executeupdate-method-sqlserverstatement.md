---
description: executeUpdate メソッド (SQLServerStatement)
title: executeUpdate メソッド (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- SQLServerStatement.executeUpdate
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10ae662a-ce3c-4b24-875c-5c2df319d93b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8134bd0c4523da21bd46ebea7547c6ca85e978e7
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99168519"
---
# <a name="executeupdate-method-sqlserverstatement"></a>executeUpdate メソッド (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  渡された SQL ステートメントを実行します。ステートメントは INSERT、UPDATE、DELETE、または SQL DDL ステートメントのような何も返さない SQL ステートメントが可能です。 [!INCLUDE[msCoName](../../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0 以降、executeUpdate では、MERGE 操作で更新された行の正確な数が返されます。  
  
## <a name="overload-list"></a>オーバーロードの一覧  
  
|名前|説明|  
|----------|-----------------|  
|[executeUpdate (java.lang.String)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-sqlserverstatement.md)|渡された SQL ステートメントを実行します。ステートメントは INSERT、UPDATE、DELETE、MERGE、または SQL DDL ステートメントのような何も返さない SQL ステートメントが可能です。|  
|[executeUpdate (java.lang.String, int)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-int.md)|渡された SQL ステートメントを実行し、[SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) オブジェクトによって自動生成されたキーを検索可能にするかどうかについて、渡されたフラグを使用して [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] に通知します。|  
|[executeUpdate (java.lang.String, int&#91;&#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string.md)|渡された SQL ステートメントを実行し、渡された配列に示される自動生成キーを検索可能にするように、JDBC ドライバーに通知します。|  
|[executeUpdate (java.lang.String, java.lang.String&#91;&#93;)](../../../connect/jdbc/reference/executeupdate-method-java-lang-string-java-lang-string.md)|渡された SQL ステートメントを実行し、渡された配列に示される自動生成キーを検索可能にするように、JDBC ドライバーに通知します。|  
  
## <a name="see-also"></a>参照  
 [SQLServerStatement のメンバー](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [SQLServerStatement クラス](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
