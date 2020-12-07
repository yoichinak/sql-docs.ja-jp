---
description: SQLServerXADataSource クラス
title: SQLServerXADataSource クラス | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 95fc7b07-2498-4a7e-8f7f-ee0d86b598b4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 775768de5cd833a6fdc9d496c5d94653bcf4ef09
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88462601"
---
# <a name="sqlserverxadatasource-class"></a>SQLServerXADataSource クラス
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  内部で使用されている [SQLServerXAConnection](../../../connect/jdbc/reference/sqlserverxaconnection-class.md) オブジェクトのファクトリを表します。  
  
 **パッケージ:** com.microsoft.sqlserver.jdbc  
  
 **拡張:** [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
 **実装**: javax.sql.XADataSource  
  
## <a name="syntax"></a>構文  
  
```  
  
public class SQLServerXADataSource  
```  
  
## <a name="remarks"></a>解説  
 SQLServerXADataSource インターフェイスを実装するオブジェクトは、通常、JNDI (Java Naming and Directory Interface) を使用するネーム サービスに登録されます。  
  
 SQLServerXADataSource クラスでは、分散 (XA) トランザクションで使用するデータベース接続が提供されます。 SQLServerXADataSource クラスでは、物理的な接続の接続プールもサポートされています。 javax.sql パッケージで定義されている SQLServerXADataSource および SQLServerXAConnection インターフェイスは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって実装されます。  
  
 SQLServerXAConnection オブジェクトは、分散トランザクションに参加できるプール接続です。 具体的には、SQLServerXAConnection により [getXAResource](../../../connect/jdbc/reference/getxaresource-method-sqlserverxaconnection.md) メソッドが追加されることで、SQLServerPooledConnection インターフェイスが拡張されます。 このメソッドでは、[SQLServerXAResource](../../../connect/jdbc/reference/sqlserverxaresource-class.md) オブジェクトが生成されます。トランザクション マネージャーでは、このオブジェクトを使用して、該当する接続で行われる処理を分散トランザクションの他の参加要素と調整できます。 SQLServerXAConnection オブジェクトは SQLServerPooledConnection インターフェイスを拡張するものであるため、SQLServerPooledConnection オブジェクトのすべてのメソッドがサポートされます。 これらは基になるデータ ソースへの再利用可能な物理的接続であり、JDBC アプリケーションに返される論理接続ハンドルを生成します。  
  
 SQLServerXAConnection オブジェクトは、SQLServerXADataSource オブジェクトによって生成されます。 SQLServerConnectionPoolDataSource オブジェクトおよび SQLServerXADataSource オブジェクトは、いずれも JDBC アプリケーションから参照できるデータ ソース層の下に実装されるため、類似しています。 このアーキテクチャでは、アプリケーションに対して透過的な方法で分散トランザクションが [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によってサポートされます。 [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 分散トランザクション コーディネーター (DTC) と統合して、真の分散トランザクション サポートが提供されるように、SQLServerXADataSource を構成することができます。  
  
## <a name="see-also"></a>参照  
 [SQLServerXADataSource のメンバー](../../../connect/jdbc/reference/sqlserverxadatasource-members.md)   
 [JDBC Driver API リファレンス](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
