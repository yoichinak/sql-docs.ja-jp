---
title: コマンド ライン ツールを使用したプロジェクト指向のデータベース開発
description: SQLPackage.exe や DbSqlPackage などの、.dacpac ファイルを操作するために、SQL Server Data Tools に用意されているコマンドライン ツールで使用可能なリソースを確認します。
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: 9a26def9-8fbd-43e4-9e57-414840b73ed8
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 04/26/2017
ms.openlocfilehash: f596b6a6d7e5d996d89b0d351396115bf9922638
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87934099"
---
# <a name="project-oriented-database-development-using-command-line-tools"></a>コマンド ライン ツールを使用したプロジェクト指向のデータベース開発

SQL Server Data Tools は、プロジェクト指向の各種データベース開発シナリオを実現に導くコマンド ライン ツールを提供します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-|-|  
|[SqlPackage.exe](../tools/sqlpackage.md)|このトピックでは、次のタスクに使用される SQLPackage.exe ユーティリティについて説明します。<br /><br />-   ライブ SQL Server データベースから .dacpac ファイルを抽出する。<br />-   .dacpac ファイルをライブ SQL Server データベースに公開し、その .dacpac に合わせてライブ データベース スキーマの増分更新を行う。<br />-   .dacpac ファイルをライブ SQL Server データベースと比較し、ライブ データベースを更新することなく、増分アップグレード Transact\-SQL スクリプトを生成する。<br />-   2 つの .dacpac ファイルを比較して、増分アップグレード Transact\-SQL スクリプトを生成する。<br />-   データベースの増分アップグレードが行われた場合に発生する、増分アップグレードによる変更をまとめた XML レポートを生成する。|  
|[dbSqlPackage プロバイダーでの MSDeploy の使用](../ssdt/using-msdeploy-with-dbsqlpackage-provider.md)|このトピックでは、SSDT に付属する、dbSqlPackage という名前の [Web 配置ツール](https://go.microsoft.com/fwlink/?LinkId=231798) プロバイダーについて説明します。これは、Microsoft インターネット インフォメーション サービス (IIS) の Web 配置ツール (MSDeploy.exe) と共に次のタスクに使用します。<br /><br />-   リモートとローカルの SQL Server または Azure SQL Database から .dacpac ファイルを抽出する。<br />-   .dacpac をリモートとローカルの SQL Server または SQL Azure SQL Database に公開し、増分アップグレードを行う。<br />-   ローカル SQL Server データベースからリモート SQL Server または Azure SQL Database に公開し、リモート データベースの増分アップグレードを行う。<br />-   .dacpac をリモートとローカルの SQL Server または Azure SQL Database と比較し、ライブ データベースを更新することなく、増分アップグレード Transact\-SQL スクリプトを生成する。<br />-   データベースの増分アップグレードが行われた場合に発生する、増分アップグレードによる変更をまとめた XML レポートを生成する。|  
  
## <a name="related-sections"></a>関連項目  
[プロジェクト指向のオフライン データベース開発](../ssdt/project-oriented-offline-database-development.md)  
  
