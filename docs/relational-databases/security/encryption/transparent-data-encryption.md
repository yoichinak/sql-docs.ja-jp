---
title: 透過的なデータ暗号化 (TDE) | Microsoft Docs
description: SQL Server、Azure SQL Database、Azure Synapse Analytics のデータを暗号化する Transparent Data Encryption について説明します。これは、保存データの暗号化として知られています。
ms.custom: ''
ms.date: 05/09/2019
ms.prod: sql
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Transparent Data Encryption
- database encryption key, about
- TDE
- database encryption key
- TDE, about
- Transparent Data Encryption, about
- encryption [SQL Server], transparent data encryption
ms.assetid: c75d0d4b-4008-4e71-9a9d-cee2a566bd3b
author: jaszymas
ms.author: jaszymas
ms.reviewer: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: edb5d6b73305b9acc840c2f34461c3056a3b9cbd
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006474"
---
# <a name="transparent-data-encryption-tde"></a>Transparent Data Encryption (TDE)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

*透過的なデータ暗号化* (TDE) では、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]、[!INCLUDE[ssSDSFull](../../../includes/sssdsfull-md.md)]、および [!INCLUDE[ssSDWfull](../../../includes/sssdwfull-md.md)] のデータ ファイルを暗号化します。 この暗号化は、保存データの暗号化として知られています。

データベースをセキュリティで保護するのに役立つように、次のような対策を講じることができます。

* セキュリティで保護されたシステムの設計。
* 機密資産の暗号化。
* データベース サーバーに対するファイアウォールの構築。

しかし、ドライブやバックアップ テープなどの物理メディアを盗む悪意のあるユーザーは、データベースを復元またはアタッチし、そのデータを閲覧することができます。

解決策の 1 つは、データベース内の機微なデータを暗号化し、証明書を使用して、データを暗号化するキーを保護することです。 この解決策により、キーを持たないユーザーによるデータの使用を防ぐことができます。 しかし、このような保護は事前に計画しておく必要があります。

TDE では、データとログ ファイルの I/O 暗号化とその解除をリアルタイムで行います。 暗号化では、データベース暗号化キー (DEK) が使用されます。 データベース ブート レコードでは、回復中に使用できるようにキーを格納します。 DEK は対称キーです。 これは、サーバーのマスター データベースに格納されている証明書で、または EKM モジュールによって保護されている非対称キーで保護されます。

TDE では、保存データ (データとログ ファイル) が保護されます。 これにより、ユーザーは多くの法律、規制、およびさまざまな業界で制定されたガイドラインに従うことになります。 この機能により、ソフトウェア開発者は、既存のアプリケーションを変更することなく、AES および 3DES 暗号化アルゴリズムを使用してデータを暗号化できます。

> [!IMPORTANT]
> TDE では、通信チャネル全体で暗号化することはできません。 通信チャネル全体でデータを暗号化する方法の詳細については、「[データベース エンジンへの暗号化接続の有効化 (SQL Server 構成マネージャー)](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。
>
>**関連項目:**
>
> - [Azure SQL Database での Transparent Data Encryption](/azure/azure-sql/database/transparent-data-encryption-tde-overview)
> - [Azure Synapse Analytics での Transparent Data Encryption (TDE) の概要](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql)
> - [別の SQL Server への TDE で保護されたデータベースの移動](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)
> - [EKM の使用による TDE の有効化](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)
> - [SQL 暗号化機能への SQL Server コネクタの使用](../../../relational-databases/security/encryption/use-sql-server-connector-with-sql-encryption-features.md)
> - [よく寄せられる質問での TDE についての SQL Server セキュリティ ブログ](/archive/blogs/sqlsecurity/feature-spotlight-transparent-data-encryption-tde)

## <a name="about-tde"></a>TDE について

データベース ファイルの暗号化は、ページ レベルで行われます。 暗号化されたデータベースのページは、ディスクに書き込まれる前に暗号化され、メモリに読み込まれるときに暗号化解除されます。 TDE では、暗号化されたデータベースのサイズが増えることはありません。

### <a name="information-applicable-to-sssds"></a>[!INCLUDE[ssSDS](../../../includes/sssds-md.md)] に該当する情報

TDE を [!INCLUDE[sqldbesa](../../../includes/sqldbesa-md.md)] V12 と共に使用すると、マスター データベースに格納されるサーバー レベルの証明書が [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] によって自動的に作成されます。 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] で TDE データベースを移動する場合、移動操作のためにデータベースの暗号化を解除する必要はありません。 TDE と [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] の使用について詳しくは、「[Azure SQL Database の Transparent Data Encryption](/azure/azure-sql/database/transparent-data-encryption-tde-overview)」を参照してください。

### <a name="information-applicable-to-ssnoversion"></a>[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に該当する情報

データベースをセキュリティで保護した後、正しい証明書を使用して復元することができます。 証明書の詳細については、「 [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)」をご覧ください。

TDE を有効にした後、証明書とそれに関連する秘密キーをすぐにバックアップします。 証明書が使用できなくなった場合、または別のサーバーでデータベースを復元またはアタッチした場合は、証明書と秘密キーのバックアップが必要になります。 そうしないと、データベースを開くことができません。

データベースで TDE を無効にした場合でも、暗号化証明書は保持するようにしてください。 データベースは暗号化されていませんが、トランザクション ログの一部が保護されたままになる可能性があります。 また、データベースの完全バックアップを行うまで、一部の操作で証明書が必要になる場合があります。

有効期限の過ぎた証明書を引き続き使用して、TDE でデータを暗号化および暗号化解除することができます。

### <a name="encryption-hierarchy"></a>暗号化階層

TDE 暗号化のアーキテクチャを次の図に示します。 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] で TDE を使用する場合に、ユーザーが構成できるのは、データベース レベルの項目 (データベース暗号化キーと ALTER DATABASE の部分) のみとなります。

![Transparent Database Encryption のアーキテクチャ](../../../relational-databases/security/encryption/media/tde-architecture.png)

## <a name="enable-tde"></a>TDE を有効にする

TDE を使用するには、次の手順を実行します。

**適用対象**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]

1. マスター キーを作成します。

1. マスター キーで保護された証明書を作成または取得します。

1. データベース暗号化キーを作成し、証明書を使用して保護します。

1. 暗号化を使用するようにデータベースを設定します。

次の例では、サーバーにインストールされている `MyServerCert` という名前の証明書を使用する、`AdventureWorks2012` データベースの暗号化とその解除を示します。

```sql
USE master;
GO
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<UseStrongPasswordHere>';
go
CREATE CERTIFICATE MyServerCert WITH SUBJECT = 'My DEK Certificate';
go
USE AdventureWorks2012;
GO
CREATE DATABASE ENCRYPTION KEY
WITH ALGORITHM = AES_128
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;
GO
ALTER DATABASE AdventureWorks2012
SET ENCRYPTION ON;
GO
```

暗号化および暗号化解除の操作は、 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]によってバックグラウンド スレッドでスケジュールされます。 これらの操作の状態を表示するには、この記事で後述する表のカタログ ビューと動的管理ビューを使用します。

> [!CAUTION]
> TDE が有効になっているデータベースのバックアップ ファイルも、データベース暗号化キーを使用して暗号化されます。 このため、これらのバックアップを復元するときには、データベース暗号化キーを保護する証明書を使用できる必要があります。 したがって、データベースをバックアップするだけでなく、必ず、サーバー証明書のバックアップを保持するようにしてください。 証明書が使用できなくなると、データの損失が発生します。
>
> 詳細については、「 [SQL Server Certificates and Asymmetric Keys](../../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)」をご覧ください。

## <a name="commands-and-functions"></a>コマンドと関数

次のステートメントで TDE 証明書を受け入れるには、データベース マスター キーを使用して証明書を暗号化します。 それらをパスワードのみを使用して暗号化した場合、ステートメントでは暗号化機能として受け付けられません。

> [!IMPORTANT]
> TDE で使用した後に証明書のパスワードを保護すると、再起動後にデータベースにアクセスできなくなります。

次の表に、TDE のコマンドと関数のリンクと説明を示します。

|コマンドまたは関数|目的|
|-------------------------|-------------|
|[CREATE DATABASE ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)|データベースを暗号化するキーを作成します| 
|[ALTER DATABASE ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/alter-database-encryption-key-transact-sql.md)|データベースを暗号化するキーを変更します|
|[DROP DATABASE ENCRYPTION KEY (Transact-SQL)](../../../t-sql/statements/drop-database-encryption-key-transact-sql.md)|データベースを暗号化するキーを削除します|
|[ALTER DATABASE SET のオプション (Transact-SQL)](../../../t-sql/statements/alter-database-transact-sql-set-options.md)|TDE を有効にするために使用される **ALTER DATABASE** オプションについて説明します|

## <a name="catalog-views-and-dynamic-management-views"></a>カタログ ビューと動的管理ビュー

 次の表に、TDE のカタログ ビューと動的管理ビューを示します。

|カタログ ビューまたは動的管理ビュー|目的|
|---------------------------------------------|-------------|
|[sys.databases (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)|データベース情報を表示するカタログ ビュー|
|[sys.certificates (Transact-SQL)](../../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|データベース内の証明書を表示するカタログ ビュー|
|[sys.dm_database_encryption_keys (Transact-SQL)](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)|データベースの暗号化キーと暗号化の状態に関する情報を提供する動的管理ビュー|

## <a name="permissions"></a>アクセス許可

TDE の各機能とコマンドには、上の表で説明されているように、個別の権限要件があります。

TDE に関係するメタデータを表示するには、証明書に対する VIEW DEFINITION 権限が必要です。

## <a name="considerations"></a>考慮事項

データベース暗号化操作の再暗号化スキャンが実行されている間は、データベースに対するメンテナンス操作が無効になります。 データベースに対してシングル ユーザー モード設定を使用して、メンテナンス操作を行うことができます。 詳細については、「 [データベースをシングル ユーザー モードに設定する](../../../relational-databases/databases/set-a-database-to-single-user-mode.md)」を参照してください。

データベースの暗号化の状態を確認するには、sys.dm_database_encryption_keys 動的管理ビューを使用します。 詳細については、この記事の前述の「カタログ ビューと動的管理ビュー」トピックを参照してください。

TDE では、データベース内のすべてのファイルとファイル グループが暗号化されます。 データベースに READ ONLY とマークされているファイル グループがあると、データベースの暗号化操作は失敗します。

データベースをデータベース ミラーリングまたはログ配布で使用する場合は、両方のデータベースが暗号化されます。 トランザクション ログは、それらの間で送信されるときに暗号化されます。

> [!IMPORTANT]
> データベースを暗号化の対象として設定すると、フルテキスト インデックスが暗号化されます。 SQL Server 2008 より前の SQL Server バージョンで作成されたこのようなインデックスは、SQL Server 2008 以降でデータベースにインポートされ、TDE によって暗号化されます。

> [!TIP]
> データベースの TDE 状態の変更を監視するには、SQL Server Audit または SQL Database 監査を使用します。 SQL Server の場合、TDE は監査アクション グループ DATABASE_CHANGE_GROUP の下で追跡されます。これは「[SQL Server 監査のアクション グループとアクション](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)」で確認できます。

## <a name="restrictions"></a>制限

最初のデータベース暗号化、キー変更、またはデータベースの暗号化解除の実行中は、次の操作は許可されません。

- データベース内のファイル グループからのファイルの削除

- データベースの削除

- データベースのオフライン化

- データベースのデタッチ

- データベースまたはファイル グループの READ ONLY 状態への移行

CREATE DATABASE ENCRYPTION KEY、ALTER DATABASE ENCRYPTION KEY、DROP DATABASE ENCRYPTION KEY、および ALTER DATABASE...SET ENCRYPTION の各ステートメントの実行中は、次の操作は許可されません。

- データベース内のファイル グループからのファイルの削除

- データベースの削除

- データベースのオフライン化

- データベースのデタッチ

- データベースまたはファイル グループの READ ONLY 状態への移行

- ALTER DATABASE コマンドの使用

- データベースまたはデータベース ファイルのバックアップの開始

- データベースまたはデータベース ファイルの復元の開始

- スナップショットの作成

次の操作または状況が発生すると、CREATE DATABASE ENCRYPTION KEY、ALTER DATABASE ENCRYPTION KEY、DROP DATABASE ENCRYPTION KEY、および ALTER DATABASE...SET ENCRYPTION の各ステートメントを実行できません。

- データベースが読み取り専用であるか、読み取り専用のファイル グループを含んでいる。

- ALTER DATABASE コマンドが実行されている。

- データ バックアップが実行されている。

- データベースがオフラインまたは復元中である。

- スナップショットが実行されている。

- データベース メンテナンス タスクが実行されている。

データベース ファイルが作成されるときに、TDE が有効になっているとファイルの瞬時初期化を使用できません。

非対称キーでデータベース暗号化キーを暗号化するには、その非対称キーが拡張キー管理プロバイダーに存在している必要があります。

## <a name="tde-scan"></a>TDE スキャン

データベースで TDE を有効にするには、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] で暗号化スキャンを行う必要があります。 スキャンによって、データ ファイルからバッファー プールに各ページが読み取られ、暗号化されたページがディスクに書き戻されます。

暗号化スキャンをより詳細に制御できるように、[!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] には、suspend および resume 構文を含む、TDE スキャンが導入されています。 システムのワークロードが大きい場合や、ビジネス クリティカルな時間に、スキャンを一時停止し、後でスキャンを再開することができます。

TDE 暗号化のスキャンを一時停止するには、次の構文を使用します。

```sql
ALTER DATABASE <db_name> SET ENCRYPTION SUSPEND;
```

同様に、TDE 暗号化のスキャンを再開するには、次の構文を使用します。

```sql
ALTER DATABASE <db_name> SET ENCRYPTION RESUME;
```

encryption_scan_state 列が、dm_database_encryption_keys 動的管理ビューに追加されました。 暗号化スキャンの現在の状態が表示されています。 また、暗号化スキャンの状態が最後に変更された日時を含む、encryption_scan_modify_date という新しい列もあります。

暗号化スキャンが一時停止されている間に [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンスが再起動した場合、メッセージは起動時にエラー ログに記録されます。 このメッセージは、既存のスキャンが一時停止されていることを示します。

## <a name="tde-and-transaction-logs"></a>TDE とトランザクション ログ

データベースで TDE を使用できるようにすると、現在の仮想トランザクション ログの残りの部分が削除されます。 削除時に、次のトランザクション ログが強制的に作成されます。 この動作により、データベースが暗号化対象として設定された後にログにクリア テキストが残らないことが保証されます。

ログ ファイルの暗号化の状態を確認するには、この例のように、`encryption_state` ビューの `sys.dm_database_encryption_keys` 列を参照します。

```sql
USE AdventureWorks2012;
GO
/* The value 3 represents an encrypted state
   on the database and transaction logs. */
SELECT *
FROM sys.dm_database_encryption_keys
WHERE encryption_state = 3;
GO
```

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] のログ ファイル アーキテクチャの詳細については、「[トランザクション ログ (SQL Server)](../../../relational-databases/logs/the-transaction-log-sql-server.md)」を参照してください。

データベース暗号化キーが変更される前に、以前のデータベース暗号化キーによって、トランザクション ログに書き込まれたすべてのデータが暗号化されます。

データベース暗号化キーを 2 回変更する場合は、データベース暗号化キーを再度変更する前にログ バックアップを行う必要があります。

## <a name="tde-and-the-tempdb-system-database"></a>TDE と tempdb システム データベース

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス上の他のデータベースが TDE を使用して暗号化されている場合、**tempdb** システム データベースは暗号化されます。 この暗号化が、同じ [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] インスタンス上にある暗号化されていないデータベースのパフォーマンスに影響する可能性があります。 **tempdb** システム データベースの詳細については、「[tempdb データベース](../../../relational-databases/databases/tempdb-database.md)」を参照してください。

## <a name="tde-and-replication"></a>TDE とレプリケーション

レプリケーションでは、TDE が有効になっているデータベースのデータが暗号化された形式で自動的にレプリケートされることはありません。 ディストリビューションおよびサブスクライバー データベースを保護する場合は、TDE を個別に有効にします。

スナップショット レプリケーションでは、暗号化されていない中間ファイル (BCP ファイルなど) にデータを格納できます。 トランザクションおよびマージ レプリケーションの初期データ ディストリビューションも可能です。 このようなレプリケーション時に、暗号化を有効にして通信チャネルを保護することができます。

詳細については、「[データベース エンジンへの暗号化接続の有効化 (SQL Server 構成マネージャー)](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)」を参照してください。

## <a name="tde-and-always-on"></a>TDE と Always On    
[暗号化されたデータベースを Always On 可用性グループに追加](../../../database-engine/availability-groups/windows/encrypted-databases-with-always-on-availability-groups-sql-server.md)できます。  

可用性グループに含まれるデータベースを暗号化するには、プライマリ レプリカで[データベース暗号化キー](../../../t-sql/statements/create-database-encryption-key-transact-sql.md)を作成する前に、すべてのセカンダリ レプリカでマスター キーと証明書、または非対称キー (EKM) を作成します。  

証明書がデータベース暗号化キー (DEK) の保護に使用されている場合、プライマリ レプリカで作成された[証明書をバックアップ](../../../t-sql/statements/backup-certificate-transact-sql.md)し、すべてのセカンダリ レプリカで[ファイルから証明書を作成](../../../t-sql/statements/create-certificate-transact-sql.md)してからプライマリ レプリカでデータベース暗号化キーを作成します。 

## <a name="tde-and-filestream-data"></a>TDE と FILESTREAM データ

TDE を有効にした場合でも、**FILESTREAM** データは暗号化されません。

<a name="scan-suspend-resume"></a>

## <a name="remove-tde"></a>TDE の削除

`ALTER DATABASE` ステートメントを使用してデータベースから暗号化を削除します。

```sql
ALTER DATABASE <db_name> SET ENCRYPTION OFF;
```

データベースの状態を表示するには、[sys.dm_database_encryption_keys](../../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md) 動的管理ビューを使います。

暗号化の解除が完了するまで待機し、その後、[DROP DATABASE ENCRYPTION KEY](../../../t-sql/statements/drop-database-encryption-key-transact-sql.md) でデータベース暗号化キーを削除します。

> [!IMPORTANT]
> TDE に使用されているマスター キーと証明書を安全な場所にバックアップします。 データベースが TDE で暗号化されたときに取得されたバックアップを復元するには、マスター キーと証明書が必要です。 データベース暗号化キーを削除したら、ログをバックアップし、それから復号されたデータベースの完全なバックアップを新しく作成します。 

## <a name="tde-and-buffer-pool-extension"></a>TDE とバッファー プール拡張

TDE を使用してデータベースを暗号化する場合、バッファー プール拡張機能 (BPE) に関連するファイルは暗号化されません。 これらのファイルについては、ファイル システム レベルで BitLocker や EFS などの暗号化ツールを使用します。

## <a name="tde-and-in-memory-oltp"></a>TDE とインメモリ OLTP

インメモリ OLTP オブジェクトを含むデータベースで、TDE を有効にすることができます。 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] と [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] では、TDE を有効した場合、インメモリ OLTP ログ レコードとデータが暗号化されます。 [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] では、TDE を有効した場合、インメモリ OLTP ログ レコードは暗号化されますが、MEMORY_OPTIMIZED_DATA ファイル グループのファイルは暗号化されません。

## <a name="related-tasks"></a>関連タスク

[別の SQL Server への TDE で保護されたデータベースの移動](../../../relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server.md)  
[EKM の使用による TDE の有効化](../../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md)  
[Azure Key Vault を使用する拡張キー管理 (SQL Server)](../../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  

## <a name="related-content"></a>関連コンテンツ

[Azure SQL Database での Transparent Data Encryption](/azure/azure-sql/database/transparent-data-encryption-tde-overview)  
[Azure Synapse Analytics での Transparent Data Encryption (TDE) の概要](/azure/synapse-analytics/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql)  
[SQL Server の暗号化](../../../relational-databases/security/encryption/sql-server-encryption.md)  
[SQL Server とデータベースの暗号化キー (データベース エンジン)](../../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)  

## <a name="see-also"></a>関連項目

[SQL Server データベース エンジンと Azure SQL Database のセキュリティ センター](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
[FILESTREAM (SQL Server)](../../../relational-databases/blob/filestream-sql-server.md)