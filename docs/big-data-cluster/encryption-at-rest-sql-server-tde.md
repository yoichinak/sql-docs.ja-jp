---
title: SQL Server ビッグ データ クラスターの保存時の Transparent Data Encryption (TDE) の使用ガイド
titleSuffix: SQL Server Big Data Clusters
description: この記事では、BDC の SQL Server の保存時の TDE 暗号化機能を使用する方法について説明します
author: DaniBunny
ms.author: dacoelho
ms.reviewer: mihaelab
ms.date: 10/19/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 55456185a6503ee11465a1e65cb9cd91de3ba6e2
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92199583"
---
# <a name="sql-server-big-data-clusters-transparent-data-encryption-tde-at-rest-usage-guide"></a>SQL Server ビッグ データ クラスターの保存時の Transparent Data Encryption (TDE) の使用ガイド

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

このガイドでは、SQL Server ビッグ データ クラスターの保存時の暗号化機能を使用してデータベースを暗号化する方法について説明します。

エクスペリエンスは概して SQL Server on Linux と同じです。特に記載がない限り、[標準の TDE ドキュメント](../relational-databases/security/encryption/transparent-data-encryption.md)が適用されます。 マスターの暗号化の状態を監視するには、[`sys.dm_database_encryption_keys`](../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) と [`sys.certificates`](../relational-databases/system-catalog-views/sys-certificates-transact-sql.md) に加えて標準の DMV クエリ パターンに従います。

__サポートされていない機能:__
* データ プールの暗号化
* [HA デプロイ](deployment-high-availability.md)内の可用性グループに含まれるデータベースの暗号化キーのローテーション。


## <a name="prerequisites"></a><a id="prereqs"></a> 前提条件

- [SQL Server ビッグ データ クラスター CU8 以降](release-notes-big-data-cluster.md)
- [ビッグ データ ツール](deploy-big-data-tools.md)
   - **Azure Data Studio**
- 管理者特権を持つ SQL Server ユーザー

## <a name="query-the-installed-certificates"></a>インストールされている証明書のクエリを実行する

1. Azure Data Studio で、ビッグ データ クラスターの SQL Server マスター インスタンスに接続します。 詳細については、「[SQL Server マスター インスタンスに接続する](connect-to-big-data-cluster.md#master)」を参照してください。

1. **[サーバー]** ウィンドウで接続をダブルクリックして、SQL Server マスター インスタンスのサーバー ダッシュボードを表示します。 **[新しいクエリ]** を選択します。

   ![SQL Server マスター インスタンス クエリ](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. 次の Transact-SQL コマンドを実行し、マスター インスタンスの **master** データベースにコンテキストを変更します。

   ```sql
   USE master
   GO
   ```

1. インストールされているシステム管理証明書に対してクエリを実行します。 

   ```sql
    SELECT TOP 1 name FROM sys.certificates WHERE name LIKE 'TDECertificate%' ORDER BY name DESC
   ```

    必要に応じて別のクエリ条件を使用します。

    証明書名は、"TDECertificate{timestamp}" と表示されます。 TDECertificate のプレフィックスに続いてタイムスタンプが表示された場合、これがシステム管理機能によって提供される証明書です。

## <a name="encrypt-a-database-using-the-system-provided-certificate"></a>システムで提供された証明書を使用してデータベースを暗号化する

次の例では、暗号化のターゲットとして __userdb__ という名前のデータベースと、前のセクションの出力による __TDECertificate2020_09_15_22_46_27__ という名前のシステムで提供された証明書を想定します。

1. 提供されたシステム証明書を使用してデータベース暗号化キーを生成するには、次のパターンを使用します。

   ```sql
    USE userdb; 
    GO
    CREATE DATABASE ENCRYPTION KEY WITH ALGORITHM = AES_256 ENCRYPTION BY SERVER CERTIFICATE TDECertificate2020_09_15_22_46_27;
    GO
   ```

1. 次のコマンドを使用して、データベース __userdb__ を暗号化します。

   ```sql
    ALTER DATABASE userdb SET ENCRYPTION ON;
    GO
   ```

## <a name="next-steps"></a>次の手順

HDFS の保存時の暗号化について学習します。
> [!div class="nextstepaction"]
> [HDFS 暗号化ゾーン](encryption-at-rest-hdfs-encryption-zones.md)
