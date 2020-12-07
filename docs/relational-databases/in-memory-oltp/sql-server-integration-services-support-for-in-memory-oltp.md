---
title: SSIS によるインメモリ OLTP のサポート
description: ネイティブ コンパイル ストアド プロシージャを SQL Server Integration Services パッケージのソースおよび変換先コンポーネントとして使用する方法について説明します。
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ea82a9b9-e9ed-4d6f-b3fd-917f6c687ae3
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a2e755e50bc48e418ceabd0b2334746dc6e7885d
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867516"
---
# <a name="sql-server-integration-services-support-for-in-memory-oltp"></a>SQL Server Integration Services によるインメモリ OLTP のサポート
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) パッケージの送信元または送信先として、メモリ最適化テーブル、メモリ最適化テーブルを参照するビュー、またはネイティブ コンパイル ストアド プロシージャを使用できます。 SSIS パッケージのデータ フロー内の [ADO NET ソース](../../integration-services/data-flow/ado-net-source.md)、 [OLE DB ソース](../../integration-services/data-flow/ole-db-source.md)、または [ODBC ソース](../../integration-services/data-flow/odbc-source.md) を使用してソース コンポーネントを構成することで、メモリ最適化テーブルまたはビューからデータを取得したり、ネイティブ コンパイル ストアド プロシージャを実行する SQL ステートメントを指定できます。 同様に、 [ADO NET 変換先](../../integration-services/data-flow/ado-net-destination.md)、 [OLE DB 変換先](../../integration-services/data-flow/ole-db-destination.md)、または [ODBC 変換先](../../integration-services/data-flow/odbc-destination.md) を使用して、メモリ最適化テーブルまたはビューにデータを読み込んだり、ネイティブ コンパイル ストアド プロシージャを実行する SQL ステートメントを指定できます。  
  
 SSIS パッケージ内で上記の送信元および送信先コンポーネントを構成して、他の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] テーブルおよびビューと同じように、メモリ最適化テーブルおよびビューから読み取りや書き込みを行うことができます。 ただし、ネイティブ コンパイル ストアド プロシージャを使用する場合は、次のセクションで説明する重要なポイントについて注意する必要があります。  
  
## <a name="invoking-a-natively-compiled-stored-procedure-from-an-ssis-package"></a>SSIS パッケージからのネイティブ コンパイル ストアド プロシージャの呼び出し  
 SSIS パッケージからネイティブ コンパイル ストアド プロシージャを呼び出すには、**EXEC** キーワードなしの **\<procedure name>** という形式の SQL ステートメントを使用して ODBC ソースまたは ODBC 変換先を使用することをお勧めします。 SQL ステートメントで EXEC キーワードを使用する場合は、ODBC 接続マネージャーは SQL コマンド テキストをストアド プロシージャではなく [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントとして解釈し、カーソルを使用するため、エラー メッセージが表示されます。これはネイティブ コンパイル ストアド プロシージャの実行に対してはサポートされません。 接続マネージャーは、ストアド プロシージャの呼び出しとして EXEC キーワードを使用せずに SQL ステートメントを処理し、カーソルは使用されません。  
  
 ADO .NET ソースと OLE DB ソースを使用してネイティブ コンパイル ストアド プロシージャを呼び出すこともできますが、ODBC 入力元を使用することをお勧めします。 ネイティブ コンパイル ストアド プロシージャを実行するように ADO .NET ソースを構成すると、エラー メッセージが表示されます。これは、ADO .NET ソースが既定で使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient) のデータ プロバイダーが、ネイティブ コンパイル ストアド プロシージャの実行をサポートしていないためです。 ADO .NET ソースは、ODBC Data Provider、OLE DB Provider for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、または [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client を使用するように構成できます。 ただし、ODBC Data Provider と ADO .NET ソースを使用するよりも ODBC 入力元を使用した方がパフォーマンスが高いことに注意してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server によるインメモリ OLTP のサポート](./transact-sql-support-for-in-memory-oltp.md)  
  
