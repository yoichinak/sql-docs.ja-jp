---
title: setAutoCommit メソッド (SQLServerConnection)
description: JDBC Driver for SQL Server の SQLServerConnection クラスでの setAutoCommit メソッドのパブリック API 詳細について説明します。
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setAutoCommit
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: db1e22d2-e53f-474e-8c99-cb1fff7f491a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 117fa85e5ec6bdd7d0d37de9fc057dd8127cf42a
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435376"
---
# <a name="setautocommit-method-sqlserverconnection"></a>setAutoCommit メソッド (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) オブジェクトの自動コミット モードを、渡された状態に設定します。  
  
## <a name="syntax"></a>構文  
  
```  
  
public void setAutoCommit(boolean value)  
```  
  
#### <a name="parameters"></a>パラメーター  
 *value*  
  
 接続に対して自動コミット モードを有効にする場合は **true**、無効にする場合は **false** です。  
  
## <a name="exceptions"></a>例外  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>解説  
 この setAutoCommit メソッドは、java.sql.Connection インターフェイスの setAutoCommit メソッドで指定されています。  
  
 接続が自動コミット モードの場合、SQL ステートメントはすべて個別のトランザクションとして実行され、コミットされます。 それ以外の場合、SQL ステートメントは、[commit](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md) メソッドの呼び出しで終了するトランザクションか、[rollback](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md) メソッドの呼び出しで終了するトランザクションのどちらかにグループ化されます。 既定では、新しい接続は自動コミット モードとなります。  
  
 コミットは、ステートメントの実行が終了するか、次のステートメントの実行が開始されると発生します。 [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) オブジェクトを返すステートメントが終了するのは、結果セットの最終行が取得されたとき、または結果セットが閉じたときです。 高度なケースでは、単一のステートメントが、出力パラメーターの値以外に複数の結果を返すことがあります。 このような場合、コミットは、すべての結果および出力パラメーターの値が取得されると発生します。  
  
 自動コミット モードが **false** の場合、JDBC ドライバーによって、各コミットの後に新しいトランザクションが暗黙的に開始されます。  
  
> [!NOTE]  
> トランザクションの実行中にこのメソッドが呼び出された場合、トランザクションはコミットされます。  
  
## <a name="see-also"></a>参照  
 [SQLServerConnection のメンバー](../../../connect/jdbc/reference/sqlserverconnection-members.md)  
 [SQLServerConnection クラス](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
