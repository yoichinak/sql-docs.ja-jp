---
title: SQL でのステートメントの使用
description: SQL Server 用 Microsoft JDBC Driver でさまざまな種類の SQL ステートメントを使用する方法の概要を説明します。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fe28f48a-e1bc-48ff-a5e7-c24cd6e5ecc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 49ab0f6367353847bdf3a9e0a7aff13975b4d711
ms.sourcegitcommit: 129f8574eba201eb6ade1f1620c6b80dfe63b331
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/30/2020
ms.locfileid: "87435280"
---
# <a name="using-statements-with-sql"></a>SQL でのステートメントの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] およびインライン SQL ステートメントを使用して [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] データベースのデータを操作する場合は、さまざまなクラスを使用できます。 使用するクラスは、実行する SQL ステートメントの種類によって異なります。  
  
SQL ステートメントに IN パラメーターが含まれない場合は、[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) クラスを使用しますが、IN パラメーターが含まれる場合は [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) クラスを使用します。  
  
> [!NOTE]  
> IN パラメーターと OUT パラメーターの両方を含む SQL ステートメントを使用する必要がある場合は、それらをストアド プロシージャとして実装し、[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) クラスを使用して呼び出す必要があります。 ストアド プロシージャの使用の詳細については、「[ストアド プロシージャでのステートメントの使用](../../connect/jdbc/using-statements-with-stored-procedures.md)」を参照してください。  
  
以下のセクションでは、SQL ステートメントを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースのデータを処理するさまざまなシナリオについて説明します。  

## <a name="in-this-section"></a>このセクションの内容  

| トピック                                                                                                                        | 説明                                                       |
| ---------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| [パラメーターのない SQL ステートメントの使用](../../connect/jdbc/using-an-sql-statement-with-no-parameters.md)                 | パラメーターを含まない SQL ステートメントの使用方法について説明します。   |
| [パラメーターがある SQL ステートメントの使用](../../connect/jdbc/using-an-sql-statement-with-parameters.md)                       | パラメーターを含む SQL ステートメントの使用方法について説明します。      |
| [SQL ステートメントを使用したデータベース オブジェクトの変更](../../connect/jdbc/using-an-sql-statement-to-modify-database-objects.md) | SQL ステートメントを使用してデータベース オブジェクトを変更する方法について説明します。   |
| [SQL ステートメントを使用したデータの変更](../../connect/jdbc/using-an-sql-statement-to-modify-data.md)                         | SQL ステートメントを使用してデータベースのデータを変更する方法について説明します。 |
  
## <a name="see-also"></a>関連項目

[JDBC ドライバーでのステートメントの使用](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
