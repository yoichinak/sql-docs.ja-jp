---
title: 外部データへのアクセス:ODBC ジェネリック型 - PolyBase
description: SQL Server で PolyBase を使用すると、ODBC コネクタから互換性のあるデータ ソースに接続できます。 ODBC ドライバーをインストールし、外部テーブルを作成します。
ms.date: 07/16/2020
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 51dbde0144f26171994638d50659192ca31400ee
ms.sourcegitcommit: bf8cf755896a8c964774a438f2bd461a2a648c22
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2020
ms.locfileid: "88216687"
---
# <a name="configure-polybase-to-access-external-data-with-odbc-generic-types"></a>ODBC ジェネリック型の外部データにアクセスするための PolyBase の構成

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

SQL Server 2019 で PolyBase を使用すると、ODBC コネクタを使用して ODBC と互換性のあるデータ ソースに接続できます。

この記事では、ODBC データ ソースを使用して構成接続を作成する方法について説明します。 提供されるガイダンスでは、例として 1 つの特定の ODBC ドライバーを使用します。 特定の例については、ODBC プロバイダーにお問い合わせください。 適切な接続文字列のオプションを決定するには、データ ソースの ODBC ドライバーに関するドキュメントを参照してください。 この記事の例は、特定の ODBC ドライバーには適用されない場合があります。

## <a name="prerequisites"></a>前提条件

>[!NOTE]
>この機能を使用するには、SQL Server on Windows が必要です。

* PolyBase をインストールし、SQL Server インスタンス用に有効にする必要があります ([PolyBase のインストール](polybase-installation.md))。

* データベース スコープ資格情報より前に、[マスター キー](../../t-sql/statements/create-master-key-transact-sql.md)を作成しておく必要があります。

## <a name="install-the-odbc-driver"></a>ODBC ドライバーをインストールする

各 PolyBase ノードで、接続するデータ ソースの ODBC ドライバーをダウンロードしてインストールします。 ドライバーが適切にインストールされたら、 **[ODBC データ ソースの管理者]** からドライバーを表示してテストできます。

![PolyBase スケールアウト グループ](../../relational-databases/polybase/media/polybase-odbc-admin.png) 

上の例で、赤色の円で囲んでいるのがドライバーの名前です。 外部データ ソースを作成するときに、この名前を使用します。

> [!IMPORTANT]
> クエリのパフォーマンスを向上させるために、接続プールを有効にします。 この操作は、 **[ODBC データ ソースの管理者]** から実行できます。

## <a name="create-dependent-objects-in-sql-server"></a>SQL Server に依存オブジェクトを作成する

ODBC データ ソースを使用するには、最初にいくつかのオブジェクトを作成して構成を完了する必要があります。

このセクションでは以下の Transact-SQL コマンドが使用されます。

* [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 

1. ODBC ソースにアクセスするために、データベース スコープ資格情報を作成します。

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL <credential_name> WITH IDENTITY = '<username>', Secret = '<password>';
    ```

    たとえば、次の例では、`username` という ID と複雑なパスワードを使用して、`credential_name` という名前の資格情報を作成します。

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'BycA4ZjrE#*2W%!';
    ```

1. [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md) を使用して外部データ ソースを作成します。

    ```sql
    CREATE EXTERNAL DATA SOURCE <external_data_source_name>
    WITH ( LOCATION = 'odbc://<ODBC server address>[:<port>]',
    CONNECTION_OPTIONS = 'Driver={<Name of Installed Driver>};
    ServerNode = <name of server  address>:<Port>',
    -- PUSHDOWN = [ON] | OFF,
    CREDENTIAL = <credential_name> );
    ```

    次の例では、以下の条件で外部データ ソースを作成します。
    * `external_data_source_name` という名前
    * ODBC `SERVERNAME` およびポート `4444`に配置する
    * `CData ODBC Driver For SAP 2015` に接続する - これは、「[ODBC ドライバーをインストールする](#install-the-odbc-driver)」で作成したドライバーです。
    * `ServerNode``sap_server_node` のポート `5555`
    * サーバーへのプッシュ ダウンを処理できるように構成する (`PUSHDOWN = ON`)
    * 資格情報 `credential_name` を使用する

    ```sql
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( LOCATION = 'odbc://SERVERNAME:4444',
    CONNECTION_OPTIONS = 'Driver={CData ODBC Driver For SAP 2015};
    ServerNode = sap_server_node:5555',
    PUSHDOWN = ON,
    CREDENTIAL = credential_name );
    ```
    
## <a name="create-an-external-table"></a>外部テーブルを作成する

依存オブジェクトを作成したら、T-SQL を使用して外部テーブルを作成できます。 

このセクションでは以下の Transact-SQL コマンドが使用されます。
* [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md)
* [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. 1 つ以上の外部テーブルを作成します。

   外部テーブルを作成します。 `DATA_SOURCE` 引数を使用して上で作成した外部データ ソースを参照し、ソース テーブルを `LOCATION` として指定する必要があります。 すべての列を参照する必要はありませんが、型が正しくマップされていることを確認する必要があります。  

   ```sql
     CREATE EXTERNAL TABLE <your_table_name>
     (
     <col1_name>     DECIMAL(38) NOT NULL,
     <col2_name>     DECIMAL(38) NOT NULL,
     <col3_name>     CHAR COLLATE Latin1_General_BIN NOT NULL
     )
     WITH (
     LOCATION='<sap_table_name>',
     DATA_SOURCE= <external_data_source_name>
     )
     ;
   ```

   > [!NOTE]
   > この外部データ ソースを使用するすべての外部テーブルで依存オブジェクトを再利用できることに注意してください。

1. **省略可能:** 外部テーブルの統計を作成します。

    クエリのパフォーマンスを最適化するには、外部テーブルの列、特に結合、フィルター、集計に使用される列に統計を作成することをお勧めします。

    ```sql
    CREATE STATISTICS statistics_name ON contact (FirstName) WITH FULLSCAN; 
    ```
    
## <a name="next-steps"></a>次のステップ

PolyBase の詳細については、[SQL Server PolyBase の概要](polybase-guide.md)に関する記事をご覧ください。
