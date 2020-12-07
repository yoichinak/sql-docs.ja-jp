---
title: ドライバー機能のサポート マトリックス
description: SQL Server のドライバーでサポートされている一般的な機能と、それらに関する情報の入手先について説明します。
ms.custom: ''
ms.date: 11/30/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-daenge
ms.openlocfilehash: ac2f39826768cf7fe2948a4168bd93187a93ea3c
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/01/2020
ms.locfileid: "96419674"
---
# <a name="driver-feature-support-matrix-for-microsoft-sql-server"></a>Microsoft SQL Server のドライバー機能のサポート マトリックス

Microsoft SQL Server の機能を使用する予定がある場合、すべてのドライバーで使用できるとは限りません。 特定のドライバーに機能がない理由としては、次のようなものがあります。

- この機能は、ドライバー テクノロジには適用されません。
- この機能は新しく、まだすべてのドライバーに実装されていません。
- この機能は、特定のドライバーでは必要ありません。
- 他の機能が先に実装されています。

Microsoft では、すべてのドライバーですべての機能がサポートされ、ドライバー間で機能の同等性が確保されるように努めています。 しかし、それが常に可能であるとは限りません。 ニーズに合った適切なドライバーを選択できるように、人気のある機能とそれらを実装するドライバーの一覧を以下に示します。

- [.NET](#table1)
- [ODBC](#table2)
- [OLE DB](#table2)
- [JDBC](#table2)
- [PHP](#table3)
- [Node.js と JavaScript](#table3)
- [Python](#table3)

| <a id="table1"></a>機能 | [Microsoft.<wbr>Data.<wbr>SqlClient (.NET Core)](ado-net/microsoft-ado-net-sql-server.md) | [Microsoft.<wbr>Data.<wbr>SqlClient (.NET Framework)](ado-net/microsoft-ado-net-sql-server.md) | System.<wbr>Data.<wbr>SqlClient (.NET Core) | [System.<wbr>Data.<wbr>SqlClient (.NET Framework)](/dotnet/framework/data/adonet/sql/) |
| :-- | :-- | :-- | :-- | :-- |
| [常に暗号化](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [あり](ado-net/sql/sqlclient-support-always-encrypted.md) | [あり](ado-net/sql/sqlclient-support-always-encrypted.md) | | [あり](ado-net/sql/sqlclient-support-always-encrypted.md) |
| [セキュリティで保護されたエンクレーブが設定された Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [あり](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) | [あり](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) | | [あり](ado-net/sql/sqlclient-support-always-encrypted.md#enabling-always-encrypted-with-secure-enclaves) |
| [Azure Active Directory アクセス トークン認証](/azure/active-directory/develop/access-tokens) | [あり](/dotnet/api/system.data.sqlclient.sqlconnection.accesstoken) | [あり](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) | [あり](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) | [あり](/dotnet/api/microsoft.data.sqlclient.sqlconnection.accesstoken) |
| [Azure Active Directory パスワード認証](/azure/sql-database/sql-database-aad-authentication) | ○ | ○ | | はい |
| [Azure Active Directory 統合認証](/azure/sql-database/sql-database-aad-authentication) | ○ | ○ | | はい |
| [Azure Active Directory (MFA) 対話型認証](/azure/sql-database/sql-database-aad-authentication) | ○ | ○ | | はい |
| [Azure Active Directory マネージド ID 認証](/azure/active-directory/managed-identities-azure-resources/overview) | はい | ○ | | |
| [Azure Active Directory サービス プリンシパル認証](/azure/active-directory/develop/app-objects-and-service-principals) | ○ | はい | | |
| [Windows 統合認証](/windows-server/security/windows-authentication/windows-authentication-overview) | [あり](ado-net/sql/authentication-sql-server.md) | [あり](ado-net/sql/authentication-sql-server.md) | [はい](/dotnet/framework/data/adonet/sql/authentication-in-sql-server) | [あり](/dotnet/framework/data/adonet/sql/authentication-in-sql-server) |
| [一括コピー](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | [あり](ado-net/sql/bulk-copy-operations-sql-server.md) | [あり](ado-net/sql/bulk-copy-operations-sql-server.md) | [はい](/dotnet/framework/data/adonet/sql/bulk-copy-operations-in-sql-server) | [あり](/dotnet/framework/data/adonet/sql/bulk-copy-operations-in-sql-server) |
| [データの感度と分類のメタデータ](../relational-databases/security/sql-data-discovery-and-classification.md) | ○ | はい | はい | はい |
| [複数のアクティブな結果セット (MARS)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [あり](ado-net/sql/multiple-active-result-sets-mars.md) | [あり](ado-net/sql/multiple-active-result-sets-mars.md) | [はい](/dotnet/framework/data/adonet/sql/multiple-active-result-sets-mars) | [あり](/dotnet/framework/data/adonet/sql/multiple-active-result-sets-mars) |
| [空間データ型](../relational-databases/spatial/spatial-data-sql-server.md) | | ○ | | はい |
| [テーブル値パラメーター (TVP)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | [あり](ado-net/sql/table-valued-parameters.md) | [あり](ado-net/sql/table-valued-parameters.md) | [はい](/dotnet/framework/data/adonet/sql/table-valued-parameters) | [あり](/dotnet/framework/data/adonet/sql/table-valued-parameters) |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [あり](ado-net/sql/sqlclient-support-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [あり](ado-net/sql/sqlclient-support-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [はい](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.multisubnetfailover?view=netcore-1.0&preserve-view=true) | [あり](/dotnet/api/system.data.sqlclient.sqlconnectionstringbuilder.multisubnetfailover?view=netframework-4.8&preserve-view=true) |
| [透過的なネットワーク IP の解決](odbc/using-transparent-network-ip-resolution.md) | | [あり](/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring?view=sqlclient-dotnet-1.1&preserve-view=true) | | [あり](/dotnet/api/system.data.sqlclient.sqlconnection.connectionstring?view=netframework-4.8&preserve-view=true) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

| <a id="table2"></a>機能 | [Windows 上の ODBC Driver for SQL Server](odbc/microsoft-odbc-driver-for-sql-server.md) | [Linux および macOS 上の ODBC Driver for SQL Server](odbc/microsoft-odbc-driver-for-sql-server.md) | [JDBC Driver for SQL Server](jdbc/microsoft-jdbc-driver-for-sql-server.md) | [OLE DB Driver for SQL Server](oledb/oledb-driver-for-sql-server.md) |
| :-- | :-- | :-- | :-- | :-- |
| [常に暗号化](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [あり](odbc/using-always-encrypted-with-the-odbc-driver.md) | [はい](odbc/using-always-encrypted-with-the-odbc-driver.md) | [あり](jdbc/using-always-encrypted-with-the-jdbc-driver.md) |
| [セキュリティで保護されたエンクレーブが設定された Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [あり](odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves) | [はい](odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves) | [あり](jdbc/using-always-encrypted-with-the-jdbc-driver.md) | |
| [Azure Active Directory アクセス トークン認証](/azure/active-directory/develop/access-tokens) | [あり](odbc/using-azure-active-directory.md#authenticating-with-an-access-token) | [あり](odbc/using-azure-active-directory.md#authenticating-with-an-access-token) | [はい](jdbc/connecting-using-azure-active-directory-authentication.md#connecting-using-access-token) | [はい](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory パスワード認証](/azure/sql-database/sql-database-aad-authentication) |  [あり](odbc/using-azure-active-directory.md) | [あり](odbc/using-azure-active-directory.md) | [はい](jdbc/connecting-using-azure-active-directory-authentication.md) | [あり](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory 統合認証](/azure/sql-database/sql-database-aad-authentication) | [あり](odbc/using-azure-active-directory.md) | [あり](odbc/using-azure-active-directory.md) | [はい](jdbc/connecting-using-azure-active-directory-authentication.md) | [あり](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory (MFA) 対話型認証](/azure/sql-database/sql-database-aad-authentication) | [あり](odbc/using-azure-active-directory.md) | | | [あり](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory マネージド ID 認証](/azure/active-directory/managed-identities-azure-resources/overview) | [あり](odbc/using-azure-active-directory.md) | [あり](odbc/using-azure-active-directory.md) | [はい](jdbc/connecting-using-azure-active-directory-authentication.md) | [あり](oledb/features/using-azure-active-directory.md) |
| [Azure Active Directory サービス プリンシパル認証](/azure/active-directory/develop/app-objects-and-service-principals) | | | | |
| [Windows 統合認証](/windows-server/security/windows-authentication/windows-authentication-overview) | はい | [はい](odbc/linux-mac/using-integrated-authentication.md) | [はい](jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md) | はい |
| [一括コピー](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | [あり](../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md) | [はい](../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md) | [はい](jdbc/using-bulk-copy-with-the-jdbc-driver.md) | [あり](oledb/features/performing-bulk-copy-operations.md) |
| [データの検出と分類メタデータ](../relational-databases/security/sql-data-discovery-and-classification.md) | [あり](odbc/data-classification.md) | [はい](odbc/data-classification.md) | [あり](jdbc/data-discovery-classification-sample.md) | |
| [複数のアクティブな結果セット (MARS)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [あり](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [はい](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | | [はい](oledb/features/using-multiple-active-result-sets-mars.md) |
| [空間データ型](../relational-databases/spatial/spatial-data-sql-server.md) | | | [あり](jdbc/use-spatial-datatypes.md) | |
| [テーブル値パラメーター (TVP)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | [あり](../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md) | [あり](../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md) | [はい](jdbc/using-table-valued-parameters.md) | [あり](oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md) |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [あり](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [あり](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [はい](jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md) | [あり](oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) |
| [透過的なネットワーク IP の解決](odbc/using-transparent-network-ip-resolution.md) | [あり](odbc/using-transparent-network-ip-resolution.md) | [あり](odbc/using-transparent-network-ip-resolution.md) | [はい](jdbc/setting-the-connection-properties.md) | [あり](oledb/features/using-transparent-network-ip-resolution.md) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

| <a id="table3"></a>機能 | [Windows 上の PHP for SQL Server 用ドライバー](php/microsoft-php-driver-for-sql-server.md)<sup>[1](#note1)</sup> | [Linux および macOS 上の PHP for SQL Server 用ドライバー](php/microsoft-php-driver-for-sql-server.md)<sup>[1](#note1)</sup> | [Tedious (Node.js)](node-js/node-js-driver-for-sql-server.md) | [pyODBC (Python)](python/pyodbc/python-sql-driver-pyodbc.md)<sup>[1](#note1)</sup> |
| :-- | :-- | :-- | :-- | :-- |
| [常に暗号化](../relational-databases/security/encryption/always-encrypted-database-engine.md) | [はい](php/using-always-encrypted-php-drivers.md) | [はい](php/using-always-encrypted-php-drivers.md) | | はい |
| [セキュリティで保護されたエンクレーブが設定された Always Encrypted](../relational-databases/security/encryption/always-encrypted-enclaves.md) | [はい](php/always-encrypted-secure-enclaves.md) | [はい](php/always-encrypted-secure-enclaves.md) | | はい |
| [Azure Active Directory アクセス トークン認証](/azure/active-directory/develop/access-tokens) | [はい](php/azure-active-directory.md) | [はい](php/azure-active-directory.md) | [はい](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | はい |
| [Azure Active Directory パスワード認証](/azure/sql-database/sql-database-aad-authentication) | [はい](php/azure-active-directory.md) | [はい](php/azure-active-directory.md) | [はい](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | はい |
| [Azure Active Directory 統合認証](/azure/sql-database/sql-database-aad-authentication) | [あり](php/azure-active-directory.md) | [はい](php/azure-active-directory.md) | | はい |
| [Azure Active Directory (MFA) 対話型認証](/azure/sql-database/sql-database-aad-authentication) | | | | はい<sup>[2](#note2)</sup> |
| [Azure Active Directory マネージド ID 認証](/azure/active-directory/managed-identities-azure-resources/overview) | [はい](php/azure-active-directory.md) | [はい](php/azure-active-directory.md) | [はい](https://tediousjs.github.io/tedious/api-connection.html#function_newConnection) | はい |
| [Azure Active Directory サービス プリンシパル認証](/azure/active-directory/develop/app-objects-and-service-principals) | | | | |
| [Windows 統合認証](/windows-server/security/windows-authentication/windows-authentication-overview) | [あり](php/how-to-connect-using-windows-authentication.md) | [はい](odbc/linux-mac/using-integrated-authentication.md) | | はい |
| [一括コピー](../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md) | | | [はい](https://tediousjs.github.io/tedious/bulk-load.html) | |
| [データの検出と分類メタデータ](../relational-databases/security/sql-data-discovery-and-classification.md) | ○ | はい | | |
| [複数のアクティブな結果セット (MARS)](../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md) | [あり](php/how-to-disable-multiple-active-resultsets-mars.md) | [はい](php/how-to-disable-multiple-active-resultsets-mars.md) | | はい |
| [空間データ型](../relational-databases/spatial/spatial-data-sql-server.md) | | | | |
| [テーブル値パラメーター (TVP)](../relational-databases/tables/use-table-valued-parameters-database-engine.md) | | | [はい](https://tediousjs.github.io/tedious/parameters.html) | はい |
| [MultiSubnetFailover](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) | [あり](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | [はい](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | | [あり](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md#connecting-with-multisubnetfailover) |
| [透過的なネットワーク IP の解決](odbc/using-transparent-network-ip-resolution.md) | [はい](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | [はい](php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md) | | [はい](odbc/using-transparent-network-ip-resolution.md) |
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<a id="note1"></a><sup>1</sup> これらのドライバーは Microsoft ODBC Driver for SQL Server に依存しているため、その機能をサポートするドライバーのバージョンも使用する必要があります。

<a id="note2"></a><sup>2</sup> Windows 上のみ。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
