---
title: SQL Server 2017 データベース エンジンの非推奨の機能 | Microsoft Docs
titleSuffix: SQL Server 2019
description: SQL Server 2017 (14.x) で引き続き使用できるデータベース エンジンの非推奨の機能について説明します。ただし、新しいアプリケーションではこれらを使用しないでください。
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- deprecated features [SQL Server]
- Database Engine [SQL Server], backward compatibility
- deprecation [SQL Server], feature list
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 5285873c9fc81849d8da8b48140dfbb71281e1aa
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670523"
---
# <a name="deprecated-database-engine-features-in-sql-server-2017"></a>SQL Server 2017 データベース エンジンの非推奨の機能

[!INCLUDE[SQL Server 2017](../includes/applies-to-version/sqlserver2017.md)]

  このトピックでは、[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] でまだ使用できるものの、非推奨とされた [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]の機能について説明します。 非推奨の機能を新しいアプリケーションで使用しないでください。  
  
機能に非推奨の印が付いている場合、それは次のことを意味します。

- その機能は保守管理状態にあり、それ以外では利用されていません。 新しい変更は行われません。新しい機能との相互運用性に関する変更もありません。
- Microsoft は、アップグレードを容易にする目的で、今後のリリースから非推奨機能を外さないように努めます。 ただし、非推奨機能が将来の技術革新を制限してしまう場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] からそれを永久的に外すことをまれに選択することがあります。
- 新しい開発作業に非推奨機能を使用することはお勧めしません。      

非推奨の機能の使用は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Deprecated Features オブジェクトのパフォーマンス カウンターおよびトレース イベントを使用して監視できます。 詳細については、「 [SQL Server オブジェクトの使用](../relational-databases/performance-monitor/use-sql-server-objects.md)」を参照してください。  

これらのカウンターの値は、次のステートメントを実行して入手することもできます。  

```sql
SELECT * FROM sys.dm_os_performance_counters
WHERE object_name = 'SQLServer:Deprecated Features';
```

> [!NOTE]
> このリストは、[!INCLUDE[sssql15-md](../includes/sssql15-md.md)] のリストと同じです。 [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)] で提供が終了または中止されることが新しく発表されたデータベース エンジン機能はありません。

## <a name="features-deprecated-in-the-next-version-of-sql-server"></a>SQL Server の次のバージョンで非推奨となっている機能

次の SQL Server データベース エンジン機能は、SQL Server の次のバージョンでは非推奨となっています。 新規の開発作業ではこれらの機能を使用しないようにし、現在これらの機能を使用しているアプリケーションはできるだけ早く修正してください。 **機能名**の値は、トレース イベントには ObjectName として表示され、パフォーマンス カウンターと `sys.dm_os_performance_counters` にはインスタンス名として表示されます。 **機能 ID** の値は、トレース イベントに ObjectId として表示されます。

### <a name="back-up-and-restore"></a>バックアップと復元

| 非推奨の機能 | 代替 | 機能名 | 機能 ID |
|--------------------|-------------|--------------|------------|
| RESTORE { DATABASE &#124; LOG } WITH [MEDIA]PASSWORD はこれまでどおり非推奨とされます。<br /><br />BACKUP { DATABASE &#124; LOG } WITH PASSWORD および BACKUP { DATABASE &#124; LOG } WITH MEDIAPASSWORD は廃止されました。 | [なし] : | BACKUP DATABASE または LOG WITH PASSWORD<br /><br />BACKUP DATABASE または LOG WITH MEDIAPASSWORD | 104<br /><br /> 103 |

### <a name="compatibility-levels"></a>互換性レベル

| 非推奨の機能 | 代替 | 機能名 | 機能 ID |
|--------------------|-------------|--------------|------------|
バージョン 100 (SQL Server 2008 および SQL Server 2008 R2) からアップグレードします。 | SQL Server バージョンが[サポート](/lifecycle/products/?products=sql-server)対象外になったときに、関連するデータベース互換性レベルに非推奨の印が付けられます。 しかし、Microsoft では、アップグレードをより簡単にする目的で、サポートされているあらゆるデータベース互換性レベルで認められているアプリケーションのサポートを可能な限り継続します。 互換性レベルの詳細については、「[ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。 | Database compatibility level 100 | 108 |

### <a name="database-objects"></a>データベース オブジェクト

| 非推奨の機能 | 代替 | 機能名 | 機能 ID |
|--------------------|-------------|--------------|------------|
| トリガーから結果セットを返す機能 | なし | トリガーから結果を返す | 12 |

### <a name="encryption"></a>暗号化

| 非推奨の機能 | 代替 | 機能名 | 機能 ID |
|--------------------|-------------|--------------|------------|
| RC4 または RC4_128 を使用した暗号化は非推奨とされており、次のバージョンで削除される予定です。 RC4 および RC4_128 の暗号化解除は非推奨ではありません。 | AES など、別の暗号化アルゴリズムを使用してください。 | 非推奨の暗号化アルゴリズム | 253 |
| MD2、MD4、MD5、SHA、および SHA1 の使用は非推奨とされます。 | 代わりに SHA2_256 または SHA2_512 を使用してください。 以前のアルゴリズムは引き続き機能しますが、非推奨のイベントが発生します。 |非推奨のハッシュ アルゴリズム | なし |

### <a name="remote-servers"></a>リモート サーバー

| 非推奨の機能 | 代替 | 機能名 | 機能 ID |
|--------------------|-------------|--------------|------------|
| sp_addremotelogin<br /><br />sp_addserver <br /><br /> sp_dropremotelogin <br /><br /> sp_helpremotelogin <br /><br /> sp_remoteoption|リンク サーバーを使用してリモート サーバーを置き換えてください。 sp_addserver は、ローカル オプションでのみ使用できます。 | sp_addremotelogin<br /><br />sp_addserver <br /><br /> sp_dropremotelogin <br /><br /> sp_helpremotelogin <br /><br > sp_remoteoption | 70 <br /><br /> 69 <br /><br /> 71 <br /><br /> 72 <br /><br /> 73 |
| \@\@remserver | リンク サーバーを使用してリモート サーバーを置き換えてください。 | なし | なし |
| SET REMOTE_PROC_TRANSACTIONS|リンク サーバーを使用してリモート サーバーを置き換えてください。 | SET REMOTE_PROC_TRANSACTIONS | 110 |

### <a name="transact-sql"></a>Transact-SQL

| 非推奨の機能 | 代替 | 機能名 | 機能 ID |
|--------------------|-------------|--------------|------------|
| **SET ROWCOUNT** 、 **INSERT**、および **UPDATE**ステートメントの **DELETE** | TOP キーワード | SET ROWCOUNT | 109 |
| HOLDLOCK table hint without parenthesis | かっこ付きの HOLDLOCK を使用します。 | HOLDLOCK table hint without parenthesis | 167 |

## <a name="features-deprecated-in-a-future-version-of-sql-server"></a>SQL Server の将来のバージョンで非推奨となっている機能

以下の SQL Server データベース エンジン機能は、SQL Server の次のバージョンでサポートされます。 SQL Server の具体的なバージョンは決定されていません。

### <a name="back-up-and-restore"></a>バックアップと復元

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| BACKUP { DATABASE &#124; LOG } TO TAPE <br /><br /> BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_tape*|BACKUP { DATABASE &#124; LOG } TO DISK <br /><br /> BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_disk* | BACKUP DATABASE または LOG TO TAPE |
| sp_addumpdevice '**tape**' | sp_addumpdevice '**disk**' | ADDING TAPE DEVICE |
| sp_helpdevice | sys.backup_devices | sp_helpdevice |

### <a name="compatibility-levels"></a>互換性レベル

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| sp_dbcmptlevel|ALTER DATABASE ...SET COMPATIBILITY_LEVEL です。 詳細については、「[ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。 | sp_dbcmptlevel |
| データベース互換性レベル 110 および 120。 | 今後のリリースでデータベースおよびアプリケーションのアップグレードを計画してください。 しかし、Microsoft では、アップグレードをより簡単にする目的で、サポートされているあらゆるデータベース互換性レベルで認められているアプリケーションのサポートを可能な限り継続します。 互換性レベルの詳細については、「[ALTER DATABASE 互換性レベル &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。 | データベース互換性レベル 110 <br /><br /> データベース互換性レベル 120 |

### <a name="collations"></a>照合順序

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| Korean_Wansung_Unicode <br /><br /> Lithuanian_Classic <br /><br /> SQL_AltDiction_CP1253_CS_AS | [なし] : これらの照合順序は SQL Server 2005 (9.x) に存在しますが、fn_helpcollations には表示されません。 | Korean_Wansung_Unicode <br /><br /> Lithuanian_Classic <br /><br /> SQL_AltDiction_CP1253_CS_AS |
| ヒンディー語 <br /><br /> マケドニア語 | これらの照合順序は SQL Server 2005 (9.x) 以降に存在しますが、fn_helpcollations には表示されません。 代わりに Macedonian_FYROM_90 および Indic_General_90 を使用してください。|ヒンディー語 <br /><br /> マケドニア語 |
| Azeri_Latin_90 <br /><br /> Azeri_Cyrilllic_90 | Azeri_Latin_100 <br /><br /> Azeri_Cyrilllic_100 | Azeri_Latin_90 <br /><br /> Azeri_Cyrilllic_90 |

### <a name="data-types"></a>データ型

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| sp_addtype <br /><br /> sp_droptype|CREATE TYPE<br /><br /> DROP TYPE | sp_addtype<br /><br /> sp_droptype |
| **timestamp** データ型の **rowversion** 構文 | **rowversion** データ型の構文 | timestamp |
| **timestamp** 列に null 値を挿入する機能 | 代わりに DEFAULT を使用してください。 | TIMESTAMP 列への INSERT NULL |
| 'text in row' テーブル オプション|**varchar(max)** 、**nvarchar(max)** 、および **varbinary(max)** データ型を使用してください。 詳細については、「[sp_tableoption &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)」を参照してください。|Text in row テーブル オプション |
| データ型:<br /><br /> **text**<br /><br /> **ntext**<br /><br /> **image**|**varchar(max)** 、**nvarchar(max)** 、および **varbinary(max)** データ型を使用してください。|データ型 : **text**、**ntext**、または **image** |

### <a name="database-management"></a>データベースの管理

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| sp_attach_db <br /><br /> sp_attach_single_file_db|CREATE DATABASE ステートメントで FOR ATTACH オプションを使用します。 複数のログ ファイルを再構築するときに、これらのログ ファイル 1 つ以上に対して新しい場所を指定する場合は、FOR ATTACH_REBUILD_LOG を使用します。 | sp_attach_db <br /><br /> sp_attach_single_file_db |
| sp_certify_removable<br /><br /> sp_create_removable|sp_detach_db|sp_certify_removable<br /><br /> sp_create_removable |
| sp_dbremove | DROP DATABASE | sp_dbremove |
| sp_renamedb | ALTER DATABASE の MODIFY NAME | sp_renamedb |

### <a name="database-objects"></a>データベース オブジェクト

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| CREATE DEFAULT<br /><br /> DROP DEFAULT<br /><br /> sp_bindefault<br /><br /> sp_unbindefault|CREATE TABLE および ALTER TABLE の DEFAULT キーワード|CREATE_DROP_DEFAULT<br /><br /> sp_bindefault<br /><br /> sp_unbindefault |
| CREATE RULE<br /><br /> DROP RULE<br /><br /> sp_bindrule<br /><br /> sp_unbindrule | CREATE TABLE および ALTER TABLE の CHECK キーワード | CREATE_DROP_RULE<br /><br /> sp_bindrule<br /><br /> sp_unbindrule |
| sp_change_users_login | ALTER USER を使用してください。 | sp_change_users_login |
| sp_depends | sys.dm_sql_referencing_entities および sys.dm_sql_referenced_entities | sp_depends |
| sp_getbindtoken | MARS または分散トランザクションを使用してください。 | sp_getbindtoken |

### <a name="database-options"></a>データベース オプション

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| sp_bindsession | MARS または分散トランザクションを使用してください。 | sp_bindsession |
| sp_resetstatus | ALTER DATABASE SET { ONLINE &#124; EMERGENCY } | sp_resetstatus
| ALTER DATABASE の TORN_PAGE_DETECTION オプション|ALTER DATABASE の PAGE_VERIFY TORN_PAGE_DETECTION オプション | ALTER DATABASE WITH TORN_PAGE_DETECTION |

### <a name="dbcc"></a>DBCC

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| DBCC DBREINDEX|ALTER INDEX の REBUILD オプション | DBCC DBREINDEX |
| DBCC INDEXDEFRAG|ALTER INDEX の REORGANIZE オプション | DBCC INDEXDEFRAG |
| DBCC SHOWCONTIG|sys.dm_db_index_physical_stats | DBCC SHOWCONTIG |
| DBCC PINTABLE<br /><br /> DBCC UNPINTABLE | 機能しません。 | DBCC [UN]PINTABLE |

### <a name="extended-properties"></a>拡張プロパティ

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| 拡張プロパティをレベル 1 型またはレベル 2 型のオブジェクトに追加するための、Level0type = 'type' および Level0type = 'USER' の使用 | Level0type = 'USER' は、拡張プロパティをユーザーまたはロールに直接追加する場合のみ使用します。<br /><br /> Level0type = 'SCHEMA' を使用して、拡張プロパティを TABLE や VIEW のようなレベル 1 型に、または COLUMN や TRIGGER のようなレベル 2 型に追加します。 詳細については、「[sp_addextendedproperty &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)」を参照してください。 | EXTPROP_LEVEL0TYPE<br /><br /> EXTPROP_LEVEL0USER |

### <a name="extended-stored-procedures"></a>拡張ストアド プロシージャ

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig|CREATE LOGIN を使用してください。<br /><br /> SERVERPROPERTY の DROP LOGIN IsIntegratedSecurityOnly 引数を使用してください。|xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginconfig |

### <a name="extended-stored-procedures-programming"></a>拡張ストアド プロシージャのプログラミング

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| srv_alloc<br /><br /> srv_convert<br /><br /> srv_describe<br /><br /> srv_getbindtoken<br /><br /> srv_got_attention<br /><br /> srv_message_handler<br /><br /> srv_paramdata<br /><br /> srv_paraminfo<br /><br /> srv_paramlen<br /><br /> srv_parammaxlen<br /><br /> srv_paramname<br /><br /> srv_paramnumber<br /><br /> srv_paramset<br /><br /> srv_paramsetoutput<br /><br /> srv_paramstatus<br /><br /> srv_paramtype<br /><br /> srv_pfield<br /><br /> srv_pfieldex<br /><br /> srv_rpcdb<br /><br /> srv_rpcname<br /><br /> srv_rpcnumber<br /><br /> srv_rpcoptions<br /><br /> srv_rpcowner<br /><br /> srv_rpcparams<br /><br /> srv_senddone<br /><br /> srv_sendmsg<br /><br /> srv_sendrow<br /><br /> srv_setcoldata<br /><br /> srv_setcollen<br /><br /> srv_setutype<br /><br /> srv_willconvert<br /><br /> srv_wsendmsg | 代わりに CLR Integration を使用してください。 | XP_API |
| sp_addextendedproc<br /><br /> sp_dropextendedproc<br /><br /> sp_helpextendedproc | 代わりに CLR Integration を使用してください。 | sp_addextendedproc<br /><br /> sp_dropextendedproc<br /><br /> sp_helpextendedproc |
| xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig|CREATE LOGIN を使用してください。<br /><br /> SERVERPROPERTY の DROP LOGIN IsIntegratedSecurityOnly 引数を使用してください。 | xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginconfig |

### <a name="high-availability"></a>高可用性

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| データベース ミラーリング (database mirroring) | Always On 可用性グループ<br /><br /> ご利用の SQL Server のエディションで Always On 可用性グループがサポートされていない場合は、ログ配布を使用します。 | DATABASE_MIRRORING |

### <a name="index-options"></a>インデックス オプション

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| sp_indexoption | ALTER INDEX | sp_indexoption |
| オプションがかっこで囲まれていない CREATE TABLE、ALTER TABLE、または CREATE INDEX 構文 | 現在の構文を使用してステートメントを書き直してください。 | INDEX_OPTION |

### <a name="instance-options"></a>インスタンスのオプション

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| sp_configure の 'allow updates' オプション|システム テーブルは更新できなくなりました。 設定しても何の影響もありません。 | sp_configure 'allow updates' |
| sp_configure オプション: <br /><br /> 'locks' <br /><br /> 'open objects'<br /><br /> 'set working set size' | 自動的に構成されるようになりました。 設定しても何の影響もありません。 | sp_configure 'locks'<br /><br /> sp_configure 'open objects'<br /><br /> sp_configure 'set working set size' |
| sp_configure の 'priority boost' オプション | システム テーブルは更新できなくなりました。 設定しても何の影響もありません。 代わりに、Windows start /high ... program.exe オプションを使用してください。 | sp_configure 'priority boost' |
| sp_configure の 'remote proc trans' オプション | システム テーブルは更新できなくなりました。 設定しても何の影響もありません。 | sp_configure 'remote proc trans' |

### <a name="linked-servers"></a>リンク サーバー

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| リンク サーバーの SQLOLEDB プロバイダーの指定 | SQL Server Native Client (SQLNCLI) | SQLOLEDDB for linked servers |

### <a name="metadata"></a>Metadata

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| FILE_ID<br /><br /> INDEXKEY_PROPERTY | FILE_IDEX<br /><br /> sys.index_columns | FILE_ID<br /><br /> INDEXKEY_PROPERTY |

### <a name="native-xml-web-services"></a>ネイティブ XML Web サービス

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| FOR SOAP オプションを指定した CREATE ENDPOINT または ALTER ENDPOINT ステートメント<br /><br /> sys.endpoint_webmethods<br /><br /> sys.soap_endpoints|代わりに Windows Communications Foundation (WCF) または ASP.NET を使用してください。 | CREATE/ALTER ENDPOINT<br /><br /> sys.endpoint_webmethods<br /><br /> EXT_soap_endpoints<br /><br /> sys.soap_endpoints |

### <a name="other"></a>その他

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| DB-Library<br /><br />Embedded SQL for C|データベース エンジンでは、DB-Library および Embedded SQL API を使用する既存のアプリケーションからの接続が引き続きサポートされますが、これらの API を使用するアプリケーションでのプログラミング作業に必要なファイルやドキュメントは含まれません。 SQL Server データベース エンジンの今後のバージョンでは、DB-Library または Embedded SQL アプリケーションからの接続はサポートされません。 新しいアプリケーションの開発には DB-Library や Embedded SQL を使用しないでください。 DB-Library や Embedded SQL への依存関係は、既存アプリケーションを変更するときに削除してください。 これらの API の代わりに、SQLClient 名前空間または ODBC などの API を使用します。 SQL Server 2019 (15.x) には、これらのアプリケーションの実行に必要な DB-Library DLL が含まれていません。 DB-Library または Embedded SQL アプリケーションを実行するには、SQL Server バージョン 6.5、SQL Server 7.0、または SQL Server 2000 (8.x) から DB-Library DLL を入手する必要があります。 | なし |

### <a name="security"></a>セキュリティ

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| ALTER LOGIN WITH SET CREDENTIAL 構文 | 新しい ALTER LOGIN ADD および DROP CREDENTIAL 構文に置き換えられます。 | ALTER LOGIN WITH SET CREDENTIAL |
| sp_addapprole<br /><br /> sp_dropapprole | CREATE APPLICATION ROLE<br /><br /> DROP APPLICATION ROLE | sp_addapprole<br /><br /> sp_dropapprole |
| sp_addlogin<br /><br /> sp_droplogin | CREATE LOGIN<br /><br /> DROP LOGIN|sp_addlogin<br /><br /> sp_droplogin |
| sp_adduser<br /><br /> sp_dropuser | CREATE USER<br /><br /> DROP USER|sp_adduser<br /><br /> sp_dropuser |
| sp_grantdbaccess<br /><br /> sp_revokedbaccess|CREATE USER<br /><br /> DROP USER|sp_grantdbaccess<br /><br /> sp_revokedbaccess |
| sp_addrole<br /><br /> sp_droprole | CREATE ROLE<br /><br /> DROP ROLE|sp_addrole<br /><br /> sp_droprole |
| sp_approlepassword<br /><br /> sp_password | ALTER APPLICATION ROLE<br /><br /> ALTER LOGIN|sp_approlepassword<br /><br /> sp_password |
| sp_changedbowner|ALTER AUTHORIZATION | sp_changedbowner |
| sp_changeobjectowner|ALTER SCHEMA または ALTER AUTHORIZATION | sp_changeobjectowner |
| sp_control_dbmasterkey_password | マスター キーが存在し、パスワードが正しくなければなりません。|sp_control_dbmasterkey_password |
| sp_defaultdb<br /><br /> sp_defaultlanguage | ALTER LOGIN|sp_defaultdb<br /><br /> sp_defaultlanguage |
| sp_denylogin<br /><br /> sp_grantlogin<br /><br /> sp_revokelogin|ALTER LOGIN DISABLE<br /><br /> CREATE LOGIN<br /><br /> DROP LOGIN|sp_denylogin<br /><br /> sp_grantlogin<br /><br /> sp_revokelogin |
| USER_ID|DATABASE_PRINCIPAL_ID | USER_ID |
| sp_srvrolepermission<br /><br /> sp_dbfixedrolepermission|これらのストアド プロシージャは、 [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]で正しかった情報を返します。 出力には、SQL Server 2008 に実装された権限階層への変更が反映されません。 詳細については、「 [固定サーバー ロールの権限](https://msdn.microsoft.com/library/ms175892\(SQL.100\).aspx)」を参照してください。 | sp_srvrolepermission<br /><br /> sp_dbfixedrolepermission |
| GRANT ALL<br /><br /> DENY ALL<br /><br /> REVOKE ALL|GRANT、DENY、および REVOKE 固有の権限。|ALL 権限 |
| PERMISSIONS 組み込み関数 | 代わりに sys.fn_my_permissions をクエリしてください。 | PERMISSIONS |
| SETUSER | EXECUTE AS | SETUSER |
| RC4 および DESX 暗号化アルゴリズム|AES など、別のアルゴリズムを使用してください。 | DESX アルゴリズム |

### <a name="server-configuration-options"></a>サーバー構成オプション

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| c2 audit オプション default trace enabled オプション<br /><br /> default trace enabled オプション | [common criteria compliance enabled サーバー構成オプション](../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md)<br /><br /> [拡張イベント](../relational-databases/extended-events/extended-events.md) | sp_configure 'c2 audit mode'<br /><br />sp_configure 'default trace enabled' |

### <a name="smo-classes"></a>SMO クラス

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| *Microsoft.SQLServer.Management.Smo.Information* クラス<br /><br />*Microsoft.SQLServer.Management.Smo.Settings* クラス<br /><br />*Microsoft.SQLServer.Management.Smo.DatabaseOptions* クラス<br /><br />*Microsoft.SqlServer.Management.Smo.DatabaseDdlTrigger.NotForReplication* プロパティ | *Microsoft.SqlServer.Management.Smo.Server* クラス<br /><br />**Microsoft.SqlServer.Management.Smo.Server* クラス<br /><br />* Microsoft.SqlServer. Management.Smo.Database* クラス<br /><br />なし | なし |

### <a name="sql-server-agent"></a>SQL Server エージェント

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| **net send** による通知<br /><br />ポケットベルによる通知 | メール通知<br /><br />メール通知 | なし |

### <a name="sql-server-management-studio"></a>SQL Server Management Studio

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| SQL Server Management Studio でのソリューション エクスプローラーの統合 | | なし |

### <a name="system-stored-procedures-and-functions"></a>システム ストアド プロシージャとシステム関数

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| sp_db_increased_partitions | [なし] : SQL Server 2019 (15. x) では、増加したパーティションのサポートを既定で使用できます。 | sp_db_increased_partitions |
| fn_virtualservernodes<br /><br />fn_servershareddrives | sys.dm_os_cluster_nodes<br /><br />sys.dm_io_cluster_shared_drives | fn_virtualservernodes<br /><br /> fn_servershareddrives |
| fn_get_sql | sys.dm_exec_sql_text | fn_get_sql |
| sp_lock | sys.dm_tran_locks | sp_lock |

### <a name="system-tables"></a>システム テーブル

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| sysaltfiles<br /><br />syscacheobjects<br /><br />syscolumns<br /><br />syscomments<br /><br />sysconfigures<br /><br />sysconstraints<br /><br />syscurconfigs<br /><br />sysdatabases<br /><br />sysdepends<br /><br />sysdevices<br /><br />sysfilegroups<br /><br />sysfiles<br /><br />sysforeignkeys<br /><br />sysfulltextcatalogs<br /><br />sysindexes<br /><br />sysindexkeys<br /><br />syslockinfo<br /><br />syslogins<br /><br />sysmembers<br /><br />sysmessages<br /><br />sysobjects<br /><br />sysoledbusers<br /><br />sysopentapes<br /><br />sysperfinfo<br /><br />syspermissions<br /><br />sysprocesses<br /><br />sysprotects<br /><br />sysreferences<br /><br />sysremotelogins<br /><br />sysservers<br /><br />systypes<br /><br />sysusers|互換性ビュー。 詳細については、「[互換性ビュー &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)」を参照してください。<br /><br />**重要:** 互換性ビューには、SQL Server 2005 (9.x) で導入された機能のメタデータが表示されません。 カタログ ビューを使用するようにアプリケーションをアップグレードすることをお勧めします。 詳細については、「[カタログ ビュー &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/catalog-views-transact-sql.md)」を参照してください。 | sysaltfiles<br /><br />syscacheobjects<br /><br />syscolumns<br /><br />syscomments<br /><br />sysconfigures<br /><br />sysconstraints<br /><br />syscurconfigs<br /><br />sysdatabases<br /><br />sysdepends<br /><br />sysdevices<br /><br />sysfilegroups<br /><br />sysfiles<br /><br />sysforeignkeys<br /><br />sysfulltextcatalogs<br /><br />sysindexes<br /><br />sysindexkeys<br /><br />syslockinfo<br /><br />syslogins<br /><br />sysmembers<br /><br />sysmessages<br /><br />sysobjects<br /><br />sysoledbusers<br /><br />sysopentapes<br /><br />sysperfinfo<br /><br />syspermissions<br /><br />sysprocesses<br /><br />sysprotects<br /><br />sysreferences<br /><br />sysremotelogins<br /><br />sysservers<br /><br />systypes<br /><br />sysusers |
| sys.numbered_procedures<br /><br />sys.numbered_procedure_parameters | なし | numbered_procedures<br /><br />numbered_procedure_parameters |

### <a name="sql-trace-stored-procedures-functions-and-catalog-views"></a>SQL トレースのストアド プロシージャ、関数、およびカタログ ビュー

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| sp_trace_create<br /><br />sp_trace_setevent<br /><br />sp_trace_setfilter<br /><br />sp_trace_setstatus<br /><br />fn_trace_geteventinfo<br /><br />fn_trace_getfilterinfo<br /><br />fn_trace_getinfo<br /><br />fn_trace_gettable<br /><br />sys.traces<br /><br />sys.trace_events<br /><br />sys.trace_event_bindings<br /><br />sys.trace_categories<br /><br />sys.trace_columns<br /><br />sys.trace_subclass_values|[拡張イベント](../relational-databases/extended-events/extended-events.md) | sp_trace_create<br /><br />sp_trace_setevent<br /><br />sp_trace_setfilter<br /><br />sp_trace_setstatus<br /><br />fn_trace_geteventinfo<br /><br />fn_trace_getfilterinfo<br /><br />fn_trace_getinfo<br /><br />fn_trace_gettable<br /><br />sys.traces<br /><br />sys.trace_events<br /><br />sys.trace_event_bindings<br /><br />sys.trace_categories<br /><br />sys.trace_columns<br /><br />sys.trace_subclass_values |

### <a name="system-views"></a>システム ビュー

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| sys.sql_dependencies|sys.sql_expression_dependencies|sys.sql_dependencies |

### <a name="table-compression"></a>テーブル圧縮

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| vardecimal ストレージ形式の使用 | Vardecimal ストレージ形式は非推奨とされます。 SQL Server 2019 (15.x) のデータ圧縮では、10 進数値およびその他のデータ型が圧縮されます。 vardecimal ストレージ形式ではなくデータ圧縮を使用することをお勧めします。 | vardecimal ストレージ形式 |
| sp_db_vardecimal_storage_format プロシージャの使用|Vardecimal ストレージ形式は非推奨とされます。 SQL Server 2019 (15.x) のデータ圧縮では、10 進数値およびその他のデータ型が圧縮されます。 vardecimal ストレージ形式ではなくデータ圧縮を使用することをお勧めします。 | sp_db_vardecimal_storage_format |
| sp_estimated_rowsize_reduction_for_vardecimal プロシージャの使用|代わりにデータ圧縮と sp_estimate_data_compression_savings プロシージャを使用してください。 |sp_estimated_rowsize_reduction_for_vardecimal |

### <a name="text-pointers"></a>テキスト ポインター

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| WRITETEXT<br /><br />UPDATETEXT<br /><br />READTEXT|なし|UPDATETEXT または WRITETEXT<br /><br />READTEXT |
| TEXTPTR()<br /><br />TEXTVALID() | なし | TEXTPTR<br /><br />TEXTVALID |

### <a name="transact-sql"></a>Transact-SQL

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| :: 関数呼び出しの手順 | SELECT *column_list* FROM sys.\<*function_name*>() で置き換えられました。<br /><br />たとえば、`SELECT * FROM ::fn_virtualfilestats(2,1)` は `SELECT * FROM sys.fn_virtualfilestats(2,1)` に置き換わります。 | '::' 関数呼び出し構文 |
| 3 つおよび 4 つの部分で構成された列参照 | 2 つの部分で構成される名前が標準に準拠した動作です。|3 つ以上の部分で構成される列名 |
| SELECT リストの式に対して、列の別名として使用される、引用符で囲まれた文字列:<br /><br />'*string_alias*' = *expression* | *expression* [AS] *column_alias*<br /><br />*expression* [AS] [*column_alias*]<br /><br />*expression* [AS] "*column_alias*"<br /><br />*expression* [AS] '*column_alias*'<br /><br />*column_alias* = *expression* | 列の別名としての文字列リテラル |
| 番号付きプロシージャ | [なし] : 使用しないでください。 | ProcNums |
| DROP INDEX での*table_name.index_name* 構文|DROP INDEX での*index_name* ON *table_name* 構文です。|2 部構成の名前が使用された DROP INDEX |
| セミコロンで終了しない Transact-SQL ステートメント。|Transact-SQL ステートメントをセミコロン (;) で終了してください。 | なし |
| GROUP BY ALL|状況に応じて UNION または派生テーブルを使用したカスタム ソリューションを使用してください。 | GROUP BY ALL |
| DML ステートメントでの列名としての ROWGUIDCOL の使用|$rowguid を使用してください。|ROWGUIDCOL |
| DML ステートメントでの列名としての IDENTITYCOL の使用|$identity を使用してください。|IDENTITYCOL |
| 一時テーブル名および一時ストアド プロシージャ名としての #、## の使用 | 別の文字を少なくとも 1 文字は使用してください。|'#' および ' ##' 一時テーブルおよびストアド プロシージャの名前として
| Transact-SQL 識別子としての \@、\@\@、または \@\@ の使用。 | \@、\@\@、または \@\@ で始まる名前を識別子として使用しないでください。 | Transact-SQL 識別子としての "\@" と "\@\@" で始まる名前 |
| 既定値としての DEFAULT キーワードの使用|DEFAULT キーワードを既定値として使用しないでください。 | 既定値としての DEFAULT キーワード |
| テーブル ヒントの区切り文字としてのスペースの使用|テーブル ヒントはコンマを使用して区切ってください。 | コンマで区切られていない複数のテーブル ヒント |
| 集計インデックス付きビューの選択リストには、互換性モードが 90 の場合、COUNT_BIG (\*) の指定が必要 | COUNT_BIG (\*) を使用してください。 | COUNT_BIG(\*) がないインデックス付きビューの選択リスト |
| ビュー経由で複数ステートメントのテーブル値関数 (TVF) を呼び出す、テーブル ヒントの間接アプリケーション|[なし] :|間接的な TVF ヒント |
| ALTER DATABASE 構文:<br /><br />MODIFY FILEGROUP READONLY<br /><br />MODIFY FILEGROUP READWRITE | MODIFY FILEGROUP READ_ONLY<br /><br />MODIFY FILEGROUP READ_WRITE | MODIFY FILEGROUP READONLY<br /><br />MODIFY FILEGROUP READWRITE |
| SET ANSI_NULLS OFF および ANSI_NULLS OFF データベース オプション<br /><br />SET ANSI_PADDING OFF および ANSI_PADDING OFF データベース オプション<br /><br />SET CONCAT_NULL_YIELDS_NULL OFF および CONCAT_NULL_YIELDS_NULL OFF データベース オプション<br /><br />SET OFFSETS | [なし] : <br /><br /> ANSI_NULLS、ANSI_PADDING および CONCAT_NULLS_YIELDS_NULL は常に ON に設定されます。 SET OFFSETS は使用できません。 | SET ANSI_NULLS OFF <br /><br /> SET ANSI_PADDING OFF<br /><br />SET CONCAT_NULL_YIELDS_NULL OFF<br /><br />SET OFFSETS<br /><br />ALTER DATABASE SET ANSI_NULLS OFF<br /><br />ALTER DATABASE SET ANSI_PADDING OFF <br /><br /> ALTER DATABASE SET CONCAT_NULL_YIELDS_NULL OFF |
| SET FMTONLY | [sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md)、[sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)、[sp_describe_first_result_set &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)、[sp_describe_undeclared_parameters &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)。 | SET FMTONLY |
| UPDATE または DELETE ステートメントの FROM 句での NOLOCK または READUNCOMMITTED の指定 | FROM 句から NOLOCK または READUNCOMMITTED のテーブル ヒントを削除します。 | NOLOCK or READUNCOMMITTED in UPDATE or DELETE |
| WITH キーワードを使用しないテーブル ヒントの指定 | WITH を使用します。 | Table hint without WITH |
| INSERT_HINTS | | INSERT_HINTS |

### <a name="tools"></a>ツール

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| SQL Server Profiler for Trace Capture | SQL Server Management Studio に組み込まれている Extended Events Profiler を使用します。|SQL Server プロファイラー |
| SQL Server Profiler for Trace Replay | [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md) |

### <a name="trace-management-objects"></a>トレース管理オブジェクト

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| Microsoft.SqlServer.Management.Trace namespace (SQL Server の Trace および Replay オブジェクト用の API が含まれています)|トレース構成: <xref:Microsoft.SqlServer.Management.XEvent><br /><br />トレース読み取り: <xref:Microsoft.SqlServer.XEvent.Linq><br /><br />トレース再生:なし | |

### <a name="xml"></a>XML

| 非推奨の機能 | 代替 | 機能名 |
|--------------------|-------------|--------------|
| インライン XDR スキーマの生成 | FOR XML オプションに対する XMLDATA ディレクティブは非推奨とされます。 RAW モードと AUTO モードの場合は、XSD 世代を使用してください。 EXPLICIT モードでは、XMLDATA ディレクティブに代わる機能はありません。 | XMLDATA |

> [!NOTE]
> **sp_setapprole** のクッキーの **OUTPUT** パラメーターは現在、適切な最大長である **varbinary(8000)** としてドキュメントに記載されています。 ただし、現在の実装では **varbinary(50)** を返します。 開発者が **varbinary(50)** を割り当てると、今後のリリースでクッキーの戻り値のサイズが増えた場合にアプリケーションの変更が必要になる可能性があります。 これは廃止の問題ではありませんが、アプリケーションの調整と似ているため、このトピックで説明されています。 詳細については、「[sp_setapprole &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server 2016 で廃止されたデータベース エンジンの機能](./discontinued-database-engine-functionality-in-sql-server.md)  
