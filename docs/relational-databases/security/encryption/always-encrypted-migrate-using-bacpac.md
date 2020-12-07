---
description: Always Encrypted を使用したデータベースのエクスポートとインポート
title: Always Encrypted を使用したデータベースのエクスポートとインポート | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Always Encrypted, configure with SSMS
ms.assetid: 29816a41-f105-4414-8be1-070675d62e84
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3fc54fedce772b267cf19a9396672b61cf6e6254
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127735"
---
# <a name="export-and-import-databases-using-always-encrypted"></a>Always Encrypted を使用したデータベースのエクスポートとインポート 
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]

この記事では、[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) で保護された列を含むデータベースをエクスポートおよびインポートする方法について説明します。

データベースをエクスポートすると、暗号化された列に格納されているすべてのデータが暗号化された形式 (ciphertext) でデータベースから取得され、結果として生成された [BACPAC](../../data-tier-applications/data-tier-applications.md) に入れられます。 生成された BACPAC には、Always Encrypted キーのメタデータも含まれます。

BACPAC をデータベースにインポートすると、BACPAC からの暗号化されたデータがデータベースに読み込まれ、Always Encrypted キーのメタデータが再び作成されます。 

ソース データベース (エクスポートしたデータベース) に格納されている暗号化された列にクエリを実行するように構成されたアプリケーションがある場合、特別なことをしなくても、そのアプリケーションでターゲット データベース内の暗号化されたデータに対してクエリを実行することができます。これは両方のデータベースのキーが同じであるためです。

データベースのエクスポートおよびインポート方法の詳細については、以下をご覧ください。
- [データ層アプリケーションのエクスポート](../../data-tier-applications/export-a-data-tier-application.md)
- [BACPAC ファイルのインポートによる新しいユーザー データベースの作成](../../data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)
- [Azure SQL データベースを BACPAC ファイルにエクスポートする](/azure/sql-database/sql-database-export)
- [BACPAC ファイルを Azure SQL Database のデータベースにインポートする](/azure/sql-database/sql-database-import)
- [SqlPackage.exe](../../../tools/sqlpackage.md)

## <a name="permissions-for-migrating-databases-with-encrypted-columns"></a>暗号化された列を含むデータベースを移行するためのアクセス許可

ソース データベースに対して *ALTER ANY COLUMN MASTER KEY* および *ALTER ANY COLUMN ENCRYPTION KEY* 権限が必要です。 ターゲット データベースに対して *ALTER ANY COLUMN MASTER KEY*、*ALTER ANY COLUMN ENCRYPTION KEY*、*VIEW ANY COLUMN MASTER KEY DEFINITION*、および *VIEW ANY COLUMN ENCRYPTION* が必要です。

暗号化された列に対して構成されている列マスター キーへのアクセス権は必要ありません。エクスポートおよびインポート操作中にデータが暗号化された状態になるためです。

## <a name="next-steps"></a>次の手順
- [Always Encrypted を使用したアプリケーションの開発](always-encrypted-client-development.md)

## <a name="see-also"></a>参照
- [常に暗号化](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [Always Encrypted を使用したデータベースのバックアップと復元](always-encrypted-migrate-using-backup-restore.md)
- [SQL Server インポートおよびエクスポート ウィザードで Always Encrypted を使用して列間でデータを移行する](always-encrypted-migrate-using-import-export-wizard.md)
- [Always Encrypted を使用した暗号化データの列への一括読み込み](migrate-sensitive-data-protected-by-always-encrypted.md)