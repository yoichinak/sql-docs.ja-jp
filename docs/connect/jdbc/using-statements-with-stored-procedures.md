---
title: ストアド プロシージャでのステートメントの使用
description: SQL Server 用 Microsoft JDBC Driver を使用してストアド プロシージャを実行する方法と、入力パラメーターと出力パラメーターを使用してストアド プロシージャとの間でデータをやりとりする方法について説明します。
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0041f9e1-09b6-4487-b052-afd636c8e89a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a4848a2b3ecf11699894cb7a8acdcbde39786e53
ms.sourcegitcommit: 620a868e623134ad6ced6728ce9d03d7d0038fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87411008"
---
# <a name="using-statements-with-stored-procedures"></a>ストアド プロシージャでのステートメントの使用

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

ストアド プロシージャは、データベースのプロシージャです。他のプログラミング言語のプロシージャと似ていますが、ストアド プロシージャはデータベースそのものに格納されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ストアド プロシージャは、[!INCLUDE[tsql](../../includes/tsql-md.md)] を使用するか、または共通言語ランタイム (CLR)、および Visual Studio のプログラミング言語の 1 つ (Visual Basic、C# など) を使用して作成できます。 通常、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャでは次のことが可能です。  
  
- 入力パラメーターを受け取り、呼び出し元のプロシージャまたはバッチに出力パラメーターの形式で複数の値を返す。  
  
- 他のプロシージャの呼び出しなど、データベース内での操作を実行するプログラミング ステートメントを含む。  
  
- 呼び出し元のプロシージャまたはバッチにステータス値を返し、成功、失敗、および失敗の原因を示す。  
  
> [!NOTE]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ストアド プロシージャの詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックの「ストアド プロシージャについて」を参照してください。  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース内のデータをストアド プロシージャで操作するために、[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] には、[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)、[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)、および [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) の各クラスが用意されています。 使用するクラスは、ストアド プロシージャで IN (入力) パラメーターと OUT (出力) パラメーターのどちらが必要かによって異なります。 ストアド プロシージャで IN パラメーターも OUT パラメーターも必要ない場合、SQLServerStatement クラスを使用できます。ストアド プロシージャが何度も呼び出される場合、または IN パラメーターのみを必要とする場合は、SQLServerPreparedStatement クラスを使用できます。 ストアド プロシージャで IN パラメーターと OUT パラメーターの両方が必要な場合、SQLServerCallableStatement クラスを使用する必要があります。 SQLServerCallableStatement クラスを使用するオーバーヘッドが必要なのは、ストアド プロシージャで OUT パラメーターが必要な場合だけです。  
  
> [!NOTE]  
> ストアド プロシージャは、更新数および複数の結果セットを返すこともできます。 詳細については、「[更新数があるストアド プロシージャの使用](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)」と「[複数の結果セットの使用](../../connect/jdbc/using-multiple-result-sets.md)」を参照してください。  
  
JDBC ドライバーを使用してパラメーターがあるストアド プロシージャを呼び出す場合は、`call` SQL エスケープ シーケンスを、[SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) クラスの [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) メソッドと一緒に使用する必要があります。 `call` エスケープ シーケンスの完全な構文は次のとおりです。  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
> `call` とその他の SQL エスケープ シーケンスの詳細については、「[SQL エスケープ シーケンスの使用](../../connect/jdbc/using-sql-escape-sequences.md)」を参照してください。  
  
このセクションのトピックでは、JDBC ドライバーおよび [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL エスケープ シーケンスを使用して、`call` ストアド プロシージャを呼び出す方法を説明します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[パラメーターのないストアド プロシージャの使用](../../connect/jdbc/using-a-stored-procedure-with-no-parameters.md)|JDBC ドライバーを使用して、入力または出力パラメーターのないストアド プロシージャを実行する方法を説明します。|  
|[入力パラメーターがあるストアド プロシージャの使用](../../connect/jdbc/using-a-stored-procedure-with-input-parameters.md)|JDBC ドライバーを使用して、入力パラメーターがあるストアド プロシージャを実行する方法を説明します。|  
|[出力パラメーターがあるストアド プロシージャの使用](../../connect/jdbc/using-a-stored-procedure-with-output-parameters.md)|JDBC ドライバーを使用して、出力パラメーターのないストアド プロシージャを実行する方法を説明します。|  
|[状態の戻り値があるストアド プロシージャの使用](../../connect/jdbc/using-a-stored-procedure-with-a-return-status.md)|JDBC ドライバーを使用して、状態の戻り値があるストアド プロシージャを実行する方法を説明します。|  
|[更新数があるストアド プロシージャの使用](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md)|JDBC ドライバーを使用して、更新数を返すストアド プロシージャを実行する方法を説明します。|  
  
## <a name="see-also"></a>関連項目

[JDBC ドライバーでのステートメントの使用](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
