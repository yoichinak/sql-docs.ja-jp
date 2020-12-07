---
title: 概要
description: SQL Server Native Client (SNAC) の機能について説明します。 SQL Server Native Client は SQL Server の ODBC および OLE DB ドライバーを参照します。
ms.date: 04/14/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: native-client
ms.topic: conceptual
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f62b0fa0d27ed5db06f85b2c77e1ab381534d731
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891112"
---
# <a name="sql-server-native-client"></a>SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

SNAC (SQL Server Native Client) は、SQL Server の ODBC および OLE DB ドライバーを参照するために使用されていた用語です。

> [!IMPORTANT] 
> SQL Server Native Client (SQLNCLI) は非推奨とされます。新しい開発作業には使用しないことをお勧めします。 代わりに、新しい [Microsoft OLE DB Driver for SQL Server](../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) を使用します。これは、最新のサーバー機能で更新されます。

> [!NOTE]
> SNAC または ODBC ドライバーの詳細とダウンロードについては、「 [SNAC ライフサイクル](/archive/blogs/sqlreleaseservices/snac-lifecycle-explained)」で説明されているブログ記事を参照してください。
> ODBC Driver for SQL Server の詳細については、「 [Microsoft ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)」を参照してください。  

 でリリースされた [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client の機能については [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 、SQL Server native client の最新バージョンを参照してください。

-   [SQL Server Native Client における LocalDB のサポート](../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  

-   [メタデータの検出](../../relational-databases/native-client/features/metadata-discovery.md)  

-   [SQL Server Native Client 11.0 での UTF-16 のサポート](../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  

-   [SQL Server Native Client の HADR サポート](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  

-   [拡張イベント ログの診断情報へのアクセス](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

Native Client の ODBC では [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、Windows 7 SDK の標準 odbc に追加された3つの機能をサポートしています。  

-   接続関連の操作での非同期実行。 詳細については、「 [非同期実行](../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)」を参照してください。  

-   C データ型の機能拡張。 詳細については、「 [ODBC の C データ型](../../odbc/reference/develop-app/c-data-types-in-odbc.md)」を参照してください。  

     Native Client でこの機能をサポートするために [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、アプリケーションで ODBC 3.8 が使用されている場合、SQLGetDescField は**SQL_C_BINARY**ではなく**SQL_C_SS_TIME2** ( **time**型の場合) または**SQL_C_SS_TIMESTAMPOFFSET** ( **datetimeoffset**の場合) を返すことができます。 詳細については、「 [ODBC の日付と時刻の機能強化に関するデータ型のサポート](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)」を参照してください。  

-   小さいバッファーを使用して **SQLGetData** を複数回呼び出して、大きなパラメーター値を取得します。 詳細については、「 [SQLGetData を使用した出力パラメーターの取得](../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)」を参照してください。  

 次のトピックでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] における [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client の動作の変更点について説明します。  

-   **ICommandWithParameters:: SetParameterInfo**を呼び出すときに、 *pwszName*パラメーターに渡される値は有効な識別子である必要があります。 詳細については、「 [ICommandWithParameters](../../relational-databases/native-client-ole-db-interfaces/icommandwithparameters.md)」を参照してください。  

-   **SQLDescribeParam** は、常に ODBC 仕様に準拠した値を返します。 詳細については、「 [SQLDescribeParam](../../relational-databases/native-client-odbc-api/sqldescribeparam.md)」を参照してください。  

-   [文字変換処理での ODBC ドライバーの動作の変更](../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  

## <a name="see-also"></a>関連項目  
[SQL Server Native Client のインストール](../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
 [SQL Server Native Client の機能](../../relational-databases/native-client/features/sql-server-native-client-features.md)