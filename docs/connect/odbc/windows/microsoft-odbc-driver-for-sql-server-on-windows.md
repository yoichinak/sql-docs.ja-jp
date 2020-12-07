---
description: Microsoft ODBC Driver for SQL Server on Windows
title: Microsoft ODBC Driver for SQL Server on Windows | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b10cfc22-6a2c-4707-a456-0dcec317982b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b52e3df054a0c13846741237000855c079c842b
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005902"
---
# <a name="microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server on Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用 Microsoft ODBC Driver は、Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に標準の ODBC インターフェイスを実装するアプリケーション プログラミング インターフェイス (API) を提供するスタンドアロン ODBC ドライバーです。

Microsoft ODBC Driver for SQL Server を使用して、新しいアプリケーションを作成できます。 現在古いバージョンの ODBC ドライバーを使用している古いバージョンのアプリケーションをアップグレードすることもできます。 ODBC Driver for SQL Server を使用すると、Azure SQL Database、Azure Synapse Analytics、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に接続できます。  

## <a name="summary"></a>まとめ

| Version       | サポートされている機能      |
| ------------- |---------------| 
| Microsoft ODBC Driver 17 for SQL Server | <ul><li>BCP API の Always Encrypted のサポート</li><li>新しい接続文字列属性 UseFMTONLY により、一時テーブルを必要とする特別なケースで以前のメタデータがドライバーで使用されます</li>
| Microsoft ODBC Driver 13.1 for SQL Server     | <ul><li>Always Encrypted</li><li>Azure AD Authentication</li><li>AlwaysOn 可用性グループ (AG)</li></ul>   | 
| Microsoft ODBC Driver 13 for SQL Server      | <ul><li>国際化ドメイン名 (IDN)</li></ul> |
| Microsoft SQL Server 用 ODBC Driver 11 | <ul><li>ドライバー対応接続プール</li><li>接続の回復</li><li>非同期実行 (ポーリング メソッド)</li></ul> |    

## <a name="documentation"></a>ドキュメント  
[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用 Microsoft ODBC Driver に関するこのドキュメントの内容は次のとおりです。  
  
-   [Windows 上の SQL Server に対する ODBC のリリース ノート](../../../connect/odbc/windows/release-notes-odbc-sql-server-windows.md)  
-   [Microsoft ODBC Driver for SQL Server on Windows の機能](../../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)  
-   [システム要件、インストール、およびドライバー ファイル](../../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)  
-   [ODBC Driver for SQL Server のドライバー対応接続プール](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)  
-   [非同期実行 &#40;通知方法&#41; の例](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)  
-   [Windows ODBC ドライバーの接続の復元性](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)  
-   [ODBC ドライバーで Always Encrypted を使用する](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
-   [ODBC ドライバーでの Azure Active Directory の使用](../../../connect/odbc/using-azure-active-directory.md) 
-   [透過的なネットワーク IP の解決の使用](../../../connect/odbc/using-transparent-network-ip-resolution.md)   

## <a name="community"></a>コミュニティ  
- [SQL Server ドライバーのブログ](https://techcommunity.microsoft.com/t5/sql-server/bg-p/SQLServer/label-name/SQLServerDrivers)  
- [SQL Server データ アクセス フォーラム](https://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
  
## <a name="see-also"></a>参照  
- [SQL Server Native Client を使用したアプリケーションのビルド](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)   
- [SQL Server Native Client に関する FAQ](/previous-versions/aa937707(v=msdn.10))   
- [ODBC プログラマー リファレンス](../../../odbc/reference/odbc-programmer-s-reference.md)   
- [SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)