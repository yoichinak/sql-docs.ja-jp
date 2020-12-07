---
title: インメモリ OLTP でサポートされていない T-SQL
description: メモリ最適化テーブル、ネイティブ コンパイル ストアド プロシージャ、およびユーザー定義関数でサポートされていない Transact-SQL 機能について説明します。
ms.custom: seo-dt-2019
ms.date: 11/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e3f8009c-319d-4d7b-8993-828e55ccde11
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 04bc3b16152307b5d5ed4a3437934e5c7ce6a45a
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868783"
---
# <a name="transact-sql-constructs-not-supported-by-in-memory-oltp"></a>インメモリ OLTP でサポートされていない Transact-SQL の構造
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  メモリ最適化テーブルと、ネイティブ コンパイル ストアド プロシージャおよびユーザー定義関数では、ディスク ベース テーブルと、解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャおよびユーザー定義関数でサポートされる完全な [!INCLUDE[tsql](../../includes/tsql-md.md)] 領域はサポートされません。 サポートされていない機能を使用しようとすると、サーバーはエラーを返します。  
  
 エラー メッセージのテキストには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントの種類 (機能、操作、オプションなど) と、機能名または [!INCLUDE[tsql](../../includes/tsql-md.md)] キーワード名が含まれます。 ほとんどのサポートされていない機能では、サポートされていない機能を示すエラー メッセージ テキストと共にエラー 10794 が返されます。 次の表に、エラー メッセージのテキストに表示される可能性がある [!INCLUDE[tsql](../../includes/tsql-md.md)] の機能およびキーワードと、エラーを解決するための修正措置を示します。  
  
 メモリ最適化テーブルとネイティブ コンパイル ストアド プロシージャでサポートされる機能の詳細については、次のトピックを参照してください。  
  
-   [ネイティブ コンパイル ストアド プロシージャの移行に関する問題](./a-guide-to-query-processing-for-memory-optimized-tables.md)  
  
-   [Transact-SQL によるインメモリ OLTP のサポート](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)  
  
-   [インメモリ OLTP に対してサポートされていない SQL Server の機能](../../relational-databases/in-memory-oltp/unsupported-sql-server-features-for-in-memory-oltp.md)  
  
-   [ネイティブ コンパイル ストアド プロシージャ](./a-guide-to-query-processing-for-memory-optimized-tables.md)  
  
## <a name="databases-that-use-in-memory-oltp"></a>インメモリ OLTP を使用するデータベース  
 次の表に、サポートされていない [!INCLUDE[tsql](../../includes/tsql-md.md)] 機能、およびインメモリ OLTP データベースに関するエラー メッセージのテキストに含まれるキーワードを示します。 また、エラーの解決方法も示します。  
  
|Type|名前|解決方法|  
|----------|----------|----------------|  
|オプション|AUTO_CLOSE|データベース オプション AUTO_CLOSE=ON は、MEMORY_OPTIMIZED_DATA ファイル グループのあるデータベースではサポートされていません。|  
|オプション|ATTACH_REBUILD_LOG|CREATE データベース オプション ATTACH_REBUILD_LOG は、MEMORY_OPTIMIZED_DATA ファイル グループのあるデータベースではサポートされていません。|  
|特徴量|DATABASE SNAPSHOT|データベース スナップショットの作成は、MEMORY_OPTIMIZED_DATA ファイル グループのあるデータベースではサポートされていません。|  
|特徴量|sync_method 'database snapshot' または 'database snapshot character' の使用によるレプリケーション|sync_method 'database snapshot' または 'database snapshot character' の使用によるレプリケーションは、MEMORY_OPTIMIZED_DATA ファイル グループのあるデータベースではサポートされていません。|  
|特徴量|DBCC CHECKDB<br /><br /> DBCC CHECKTABLE|DBCC CHECKDB では、データベース内のメモリ最適化テーブルがスキップされます。<br /><br /> DBCC CHECKTABLE は、メモリ最適化テーブルで失敗します。|  
  
## <a name="memory-optimized-tables"></a>メモリ最適化テーブル  
 次の表に、サポートされていない [!INCLUDE[tsql](../../includes/tsql-md.md)] 機能、およびメモリ最適化テーブルに関するエラー メッセージのテキストに含まれるキーワードを示します。 また、エラーの解決方法も示します。  
  
|Type|名前|解決方法|  
|----------|----------|----------------|  
|特徴量|ON|メモリ最適化テーブルをファイル グループまたはパーティション構成に配置できません。 **CREATE TABLE** ステートメントから ON 句を削除します。<br /><br /> すべてのメモリ最適化テーブルは、メモリ最適化ファイル グループにマップされます。|  
|データ型|*データ型名*|指示されたデータ型はサポートされていません。 サポートされているデータ型に置き換えます。 詳細については、「 [サポートされるデータ型](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)」を参照してください。|  
|特徴量|計算列|**適用対象:** [!INCLUDE[ssSQL14-md](../../includes/sssql14-md.md)] および [!INCLUDE[ssSQL15-md](../../includes/sssql15-md.md)]<br/>計算列は、メモリ最適化テーブルではサポートされていません。 **CREATE TABLE** ステートメントから計算列を削除します。<br/><br/>[!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull-md.md)] および [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 以降の SQL Server では、メモリ最適化テーブルでの計算列およびインデックスをサポートしています。|  
|特徴量|レプリケーション|レプリケーションはメモリ最適化テーブルではサポートされていません。|  
|特徴量|FILESTREAM|FILESTREAM ストレージは、メモリ最適化テーブルのサポートされた列ではありません。 列定義から **FILESTREAM** キーワードを削除します。|  
|特徴量|SPARSE|メモリ最適化テーブルの列を SPARSE として定義することはできません。 列定義から **SPARSE** キーワードを削除します。|  
|特徴量|ROWGUIDCOL|ROWGUIDCOL オプションはメモリ最適化テーブルの列ではサポートされていません。 列定義から **ROWGUIDCOL** キーワードを削除します。|  
|特徴量|FOREIGN KEY|**適用対象:** [!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull-md.md)] および [!INCLUDE[ssSQL15-md](../../includes/sssql15-md.md)] 以降の SQL Server<br/>メモリ最適化テーブルでは、FOREIGN KEY 制約は、他のメモリ最適化テーブルの主キーを参照している外部キーでのみサポートされます。 外部キーが一意制約を参照している場合は、テーブル定義から制約を削除します。<br/><br/>[!INCLUDE[ssSQL14-md](../../includes/sssql14-md.md)] では、外部キー制約はメモリ最適化テーブルでサポートされていません。|  
|特徴量|クラスター化インデックス|非クラスター化インデックスを指定します。 主キー インデックスの場合は **PRIMARY KEY NONCLUSTERED** を指定する必要があります。|  
|特徴量|DDL 内部トランザクション|メモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャは、ユーザー トランザクションのコンテキストで作成または削除できません。 トランザクションを開始せず、CREATE または DROP ステートメントを実行する前にセッション設定 IMPLICIT_TRANSACTION を OFF に設定していることを確認します。|  
|特徴量|DDL トリガー|DDL 操作のサーバーまたはデータベース トリガーがある場合は、メモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャを作成または削除できません。 CREATE/DROP TABLE および CREATE/DROP PROCEDURE のサーバーおよびデータベース トリガーを削除します。|  
|特徴量|EVENT NOTIFICATION|DDL 操作のサーバーまたはデータベース イベント通知がある場合は、メモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャを作成または削除できません。 CREATE TABLE または DROP TABLE および CREATE PROCEDURE または DROP PROCEDURE のサーバーおよびデータベース イベント通知を削除します。|  
|特徴量|FileTable|メモリ最適化テーブルをファイル テーブルとして作成できません。 引数 **AS FileTable** を **CREATE TABLE** ステートメントから削除してください。|  
|操作|主キー列の更新|メモリ最適化テーブルおよびテーブル型の主キー列を更新できません。 主キーを更新する必要がある場合は、古い行を削除し、更新された主キーで新しい行を挿入します。|  
|操作|CREATE INDEX|メモリ最適化テーブルのインデックスは、 **CREATE TABLE** ステートメントまたは **ALTER TABLE** ステートメントを使用してインラインで指定する必要があります。|  
|操作|CREATE FULLTEXT INDEX|フルテキスト インデックスは、メモリ最適化テーブルでサポートされていません。|  
|操作|スキーマの変更|メモリ最適化テーブルとネイティブ コンパイル ストアド プロシージャでは、以下のスキーマの変更はサポートされていません。<br/> [!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull-md.md)] および [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 以降の SQL Server:ALTER TABLE、ALTER PROCEDURE、および sp_rename 操作がサポートされています。 拡張プロパティの追加など、その他のスキーマの変更はサポートされていません。<br/><br/>[!INCLUDE[ssSQL15-md](../../includes/sssql15-md.md)]:ALTER TABLE および ALTER PROCEDURE 操作はサポートされています。 sp_rename など、その他のスキーマ変更はサポートされていません。<br/><br/>[!INCLUDE[ssSQL14-md](../../includes/sssql14-md.md)]: スキーマの変更はサポートされていません。 メモリ最適化テーブルまたはネイティブ コンパイル ストアド プロシージャの定義を変更するには、まずオブジェクトを削除し、次に目的の定義でオブジェクトを再作成します。| 
|操作|TRUNCATE TABLE|メモリ最適化テーブルでは TRUNCATE 操作はサポートされません。 テーブルからすべての行を削除するには、 **DELETE FROM**_table_ を使用してすべての行を削除するか、テーブルを削除してから再作成します。|  
|操作|ALTER AUTHORIZATION|既存のメモリ最適化テーブルまたはネイティブ コンパイル ストアド プロシージャでの所有者の変更はサポートされていません。 所有者を変更するには、テーブルまたはプロシージャを削除した後、再作成します。|  
|操作|ALTER SCHEMA|既存のメモリ最適化テーブルまたはネイティブ コンパイル ストアド プロシージャを別のスキーマに転送することはサポートされていません。 スキーマ間で転送を行うには、オブジェクトを削除してから再作成します。|  
|操作|DBCC CHECKTABLE|DBCC CHECKTABLE はメモリ最適化テーブルではサポートされていません。 ディスク上のチェックポイント ファイルの整合性を確認するには、MEMORY_OPTIMIZED_DATA ファイル グループのバックアップを実行します。|  
|特徴量|ANSI_PADDING OFF|メモリ最適化テーブルまたはネイティブ コンパイル ストアド プロシージャを作成するときは、セッション オプション **ANSI_PADDING** は ON にする必要があります。 CREATE ステートメントを実行する前に、 **SET ANSI_PADDING ON** を実行します。|  
|オプション|DATA_COMPRESSION|データ圧縮は、メモリ最適化テーブルではサポートされていません。 テーブル定義からオプションを削除します。|  
|特徴量|DTC|メモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャは、分散トランザクションからアクセスできません。 代わりに SQL トランザクションを使用してください。|  
|操作|MERGE のターゲットとしてのメモリ最適化テーブル|メモリ最適化テーブルを **MERGE** 操作の対象にすることはできません。 代わりに、**INSERT**、**UPDATE**、または **DELETE** ステートメントを使用します。|  
  
## <a name="indexes-on-memory-optimized-tables"></a>メモリ最適化テーブルのインデックス  
 次の表に、メモリ最適化テーブルのインデックスに関連したエラー メッセージのテキストに表示される可能性がある [!INCLUDE[tsql](../../includes/tsql-md.md)] の機能およびキーワードと、エラーを解決するための修正措置を示します。  
  
|Type|名前|解決方法|  
|----------|----------|----------------|  
|特徴量|フィルター選択されたインデックス|フィルター選択されたインデックスは、メモリ最適化テーブルでサポートされていません。 インデックスの指定から **WHERE** 句を削除します。|  
|特徴量|[付加列]|付加列の指定は、メモリ最適化テーブルにとって必須ではありません。 メモリ最適化テーブルのすべての列は、各メモリ最適化インデックスに暗黙的に含まれています。|  
|操作|DROP INDEX|メモリ最適化テーブルのインデックスの削除はサポートされていません。 インデックスを削除するには、ALTER TABLE を使用します。<br /><br /> 詳細については、「 [メモリ最適化テーブルの変更](../../relational-databases/in-memory-oltp/altering-memory-optimized-tables.md)」を参照してください。|  
|インデックス オプション|*インデックス オプション*|1 つのインデックス オプション - HASH インデックスの BUCKET_COUNT のみがサポートされています。|  
  
## <a name="nonclustered-hash-indexes"></a>非クラスター化ハッシュ インデックス  
 次の表に、非クラスター化ハッシュ インデックスに関連したエラー メッセージのテキストに表示される可能性がある [!INCLUDE[tsql](../../includes/tsql-md.md)] の機能およびキーワードと、エラーを解決するための修正措置を示します。  
  
|Type|名前|解決方法|  
|----------|----------|----------------|  
|オプション|ASC/DESC|非クラスター化ハッシュ インデックスは順序付けされません。 インデックス キーの指定からキーワード **ASC** および **DESC** を削除します。|  
  
## <a name="natively-compiled-stored-procedures-and-user-defined-functions"></a>ネイティブ コンパイル ストアド プロシージャおよびユーザー定義関数  
 次の表に、ネイティブ コンパイル ストアド プロシージャおよびユーザー定義関数に関連したエラー メッセージのテキストに表示される可能性がある [!INCLUDE[tsql](../../includes/tsql-md.md)] の機能およびキーワードと、エラーを解決するための修正措置を示します。  
  
|Type|特徴量|解決方法|  
|----------|-------------|----------------|  
|特徴量|インライン テーブル変数|テーブル型は、変数宣言を使用してインラインで宣言できません。 テーブル型は、 **CREATE TYPE** ステートメントを使用して明示的に宣言する必要があります。|  
|特徴量|カーソル|カーソルは、ネイティブ コンパイル ストアド プロシージャではサポートされていません。<br /><br /> クライアントからプロシージャを実行する場合、カーソル API ではなく RPC を使用します。 ODBC で、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントから削除してください。 **EXECUTE**を避け、代わりにプロシージャの名前を直接指定します。<br /><br /> [!INCLUDE[tsql](../../includes/tsql-md.md)] バッチまたは他のストアド プロシージャからプロシージャを実行する場合、ネイティブ コンパイル ストアド プロシージャでカーソルを使用しないでください。<br /><br /> ネイティブ コンパイル ストアド プロシージャを作成する場合は、カーソルを使用せずに、セットベースのロジックまたは **WHILE** ループを使用します。|  
|特徴量|定数以外のパラメーターの既定値|ネイティブ コンパイル ストアド プロシージャのパラメーターで既定値を使用する場合、値は定数にする必要があります。 パラメーター宣言からワイルドカードを削除します。|  
|特徴量|EXTERNAL|CLR ストアド プロシージャをネイティブでコンパイルすることはできません。 CREATE PROCEDURE ステートメントから AS EXTERNAL 句または NATIVE_COMPILATION オプションを削除します。|  
|特徴量|番号付きストアド プロシージャ|ネイティブ コンパイル ストアド プロシージャには番号を付けられません。 **CREATE PROCEDURE**_ステートメントから_ ; **number** を削除してください。|  
|特徴量|複数行の INSERT...VALUES ステートメント|ネイティブ コンパイル ストアド プロシージャでは、同じ **INSERT** ステートメントを使用して複数行を挿入できません。 各行に対して **INSERT** ステートメントを作成します。|  
|特徴量|共通テーブル式 (CTE)|共通テーブル式 (CTE) は、ネイティブ コンパイル ストアド プロシージャでサポートされません。 クエリを書き直します。|  
|特徴量|COMPUTE|**COMPUTE** 句はサポートされていません。 クエリから削除します。|  
|特徴量|SELECT INTO|**INTO** 句は **SELECT** ステートメントではサポートされていません。 クエリを **INSERT INTO** _Table_ **SELECT** に書き換えます。|  
|特徴量|不完全な挿入列リスト|通常、INSERT ステートメントでは、テーブルのすべての列に値を指定する必要があります。<br /><br /> ただし、メモリ最適化テーブルでは、DEFAULT 制約と IDENTITY(1,1) 列はサポートされません。 これらの列は INSERT 列リストから省略でき、IDENTITY 列の場合は INSERT 列リストから省略する必要があります。|  
|特徴量|*Function*|いくつかの組み込み関数は、ネイティブ コンパイル ストアド プロシージャではサポートされません。 ストアド プロシージャから、拒否された関数を削除します。 サポートされる組み込み関数の詳細については、<br />「[ネイティブ コンパイル T-SQL モジュールでサポートされる機能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)」または<br />「[ネイティブ コンパイル ストアド プロシージャ](./a-guide-to-query-processing-for-memory-optimized-tables.md)」を参照してください。|  
|特徴量|CASE|**適用対象:** [!INCLUDE[ssSQL14-md](../../includes/sssql14-md.md)] および [!INCLUDE[ssSQL15-md](../../includes/sssql15-md.md)] 以降の SQL Server<br/>**CASE** 式は、ネイティブ コンパイル ストアド プロシージャ内のクエリではサポートされていません。 各ケースのクエリを作成します。 詳細については、「 [ネイティブ コンパイル ストアド プロシージャに CASE 式を実装する](../../relational-databases/in-memory-oltp/implementing-a-case-expression-in-a-natively-compiled-stored-procedure.md)」を参照してください。<br/><br/>[!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull-md.md)] および [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 以降の SQL Server では CASE 式をサポートしていません。|  
|特徴量|INSERT EXECUTE|参照を削除します。|  
|特徴量|EXECUTE|ネイティブ コンパイル ストアド プロシージャおよびユーザー定義関数を実行する場合にのみサポートされます。|  
|特徴量|ユーザー定義集計|ユーザー定義集計関数はネイティブ コンパイル ストアド プロシージャ内で使用できません。 プロシージャから関数への参照を削除します。|  
|特徴量|ブラウズ モード メタデータ|ネイティブ コンパイル ストアド プロシージャでは、ブラウズ モード メタデータはサポートされていません。 セッション オプション **NO_BROWSETABLE** を OFF に設定します。|  
|特徴量|FROM 句と DELETE|ネイティブ コンパイル ストアド プロシージャ内でテーブル ソースを指定した **FROM** ステートメントに対して **DELETE** 句はサポートされません。<br /><br /> **DELETE** 句を使用した **FROM** がサポートされるのは、削除元のテーブルを示すために句を使用している場合です。|  
|特徴量|FROM 句と UPDATE|ネイティブ コンパイル ストアド プロシージャ内の **FROM** ステートメントに対して **UPDATE** 句はサポートされません。| 
|特徴量|一時プロシージャ|一時ストアド プロシージャはネイティブでコンパイルできません。 永続的なネイティブ コンパイル ストアド プロシージャまたは解釈された一時 [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャを作成します。|  
|分離レベル|READ UNCOMMITTED|ネイティブ コンパイル ストアド プロシージャに対して分離レベル READ UNCOMMITTED はサポートされません。 SNAPSHOT など、サポートされる分離レベルを使用します。|  
|分離レベル|READ COMMITTED|ネイティブ コンパイル ストアド プロシージャに対して分離レベル READ COMMITTED はサポートされません。 SNAPSHOT など、サポートされる分離レベルを使用します。|  
|特徴量|一時テーブル|tempdb 内のテーブルはネイティブ コンパイル ストアド プロシージャ内では使用できません。 代わりに、テーブル変数または DURABILITY=SCHEMA_ONLY のメモリ最適化テーブルを使用します。|  
|特徴量|DTC|メモリ最適化テーブルおよびネイティブ コンパイル ストアド プロシージャは、分散トランザクションからアクセスできません。 代わりに SQL トランザクションを使用してください。|  
|特徴量|EXECUTE WITH RECOMPILE|オプション **WITH RECOMPILE** は、ネイティブ コンパイル ストアド プロシージャではサポートされていません。|  
|特徴量|専用管理者接続からの実行|ネイティブ コンパイル ストアド プロシージャでは、専用管理者接続 (DAC) から実行することはできません。 通常の接続を使用してください。|  
|操作|セーブポイント (savepoint)|ネイティブ コンパイル ストアド プロシージャは、アクティブなセーブポイントを含むトランザクションから呼び出すことはできません。 トランザクションからセーブポイントを削除します。|  
|操作|ALTER AUTHORIZATION|既存のメモリ最適化テーブルまたはネイティブ コンパイル ストアド プロシージャでの所有者の変更はサポートされていません。 所有者を変更するには、テーブルまたはプロシージャを削除した後、再作成します。|  
|演算子|OPENROWSET|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **OPENROWSET** を削除します。|  
|演算子|OPENQUERY|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **OPENQUERY** を削除します。|  
|演算子|OPENDATASOURCE|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **OPENDATASOURCE** を削除します。|  
|演算子|OPENXML|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **OPENXML** を削除します。|  
|演算子|CONTAINSTABLE|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **CONTAINSTABLE** を削除します。|  
|演算子|FREETEXTTABLE|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **FREETEXTTABLE** を削除します。|  
|特徴量|テーブル値関数|テーブル値関数はネイティブ コンパイル ストアド プロシージャから参照できません。 この制限に関する対処方法の 1 つは、プロシージャの本体にテーブル値関数のロジックを追加することです。|  
|演算子|CHANGETABLE|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **CHANGETABLE** を削除します。|  
|演算子|GOTO|この演算子はサポートされていません。 WHILE など他の構造を使用します。|  
|演算子|OFFSET|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **OFFSET** を削除します。|  
|演算子|INTERSECT|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **INTERSECT** を削除します。 場合によっては INNER JOIN を使用して同じ結果を得ることができます。|  
|演算子|EXCEPT|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **EXCEPT** を削除します。|  
|演算子|APPLY|**適用対象:** [!INCLUDE[ssSQL14-md](../../includes/sssql14-md.md)] および [!INCLUDE[ssSQL15-md](../../includes/sssql15-md.md)] 以降の SQL Server<br/>この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **APPLY** を削除します。<br/><br/>[!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull-md.md)] および [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 以降の SQL Server では、ネイティブ コンパイル モジュール内で APPLY 演算子をサポートしていません。|  
|演算子|PIVOT|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **PIVOT** を削除します。|  
|演算子|UNPIVOT|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **UNPIVOT** を削除します。|  
|演算子|CONTAINS|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **CONTAINS** を削除します。|  
|演算子|FREETEXT|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **FREETEXT** を削除します。|  
|演算子|TSEQUAL|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **TSEQUAL** を削除します。|  
|演算子|LIKE|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **LIKE** を削除します。|  
|演算子|NEXT VALUE FOR|シーケンスは、ネイティブ コンパイル ストアド プロシージャ内で参照できません。 解釈された [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用して値を取得し、それをネイティブ コンパイル ストアド プロシージャに渡します。 詳細については、「 [メモリ最適化テーブルへの IDENTITY の実装](../../relational-databases/in-memory-oltp/implementing-identity-in-a-memory-optimized-table.md)」を参照してください。|  
|SET オプション|*オプション*|SET オプションは、ネイティブ コンパイル ストアド プロシージャ内で変更できません。 特定のオプションは BEGIN ATOMIC ステートメントで設定できます。 詳細については、「 [Natively Compiled Stored Procedures](./a-guide-to-query-processing-for-memory-optimized-tables.md)」の ATOMIC ブロックに関するセクションを参照してください。|  
|オペランド|TABLESAMPLE|この演算子はサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **TABLESAMPLE** を削除します。|  
|オプション|RECOMPILE|ネイティブ コンパイル ストアド プロシージャは、作成時にコンパイルされます。 プロシージャの定義から **RECOMPILE** を削除します。<br /><br /> ネイティブ コンパイル ストアド プロシージャに対して sp_recompile を実行できます。これにより、このプロシージャは次の実行時に再コンパイルされます。|  
|オプション|ENCRYPTION|このオプションはサポートされていません。 プロシージャの定義から **ENCRYPTION** を削除します。|  
|オプション|FOR REPLICATION|ネイティブ コンパイル ストアド プロシージャはレプリケーション用に作成できません。 プロシージャの定義から **FOR REPLICATION** を削除します。|  
|オプション|FOR XML|このオプションはサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **FOR XML** を削除します。|  
|オプション|FOR BROWSE|このオプションはサポートされていません。 ネイティブ コンパイル ストアド プロシージャから **FOR BROWSE** を削除します。|  
|結合ヒント|HASH、MERGE|ネイティブ コンパイル ストアド プロシージャは、入れ子になったループ結合のみをサポートします。 HASH および MERGE 結合はサポートされていません。 結合ヒントを削除します。|  
|クエリ ヒント|*クエリ ヒント*|このクエリ ヒントはネイティブ コンパイル ストアド プロシージャ内にありません。 サポートされているクエリ ヒントについては、「[クエリ ヒント &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md)」を参照してください。|  
|オプション|PERCENT|このオプションは **TOP** 句でサポートされていません。 ネイティブ コンパイル ストアド プロシージャのクエリから **PERCENT** を削除します。|  
|オプション|WITH TIES|**適用対象:** [!INCLUDE[ssSDS14_md](../../includes/sssql14-md.md)] および [!INCLUDE[ssSQL15-md](../../includes/sssql15-md.md)]<br/>このオプションは **TOP** 句でサポートされていません。 ネイティブ コンパイル ストアド プロシージャのクエリから **WITH TIES** を削除します。<br/><br/>[!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull-md.md)] および [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 以降の SQL Server では、**TOP WITH TIES** をサポートしていません。|  
|集計関数|*集計関数*|集計関数はすべてサポートされているわけではありません。 ネイティブ コンパイル T-SQL モジュールでサポートされている集計関数の詳細については、「[ネイティブ コンパイル T-SQL モジュールでサポートされる機能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)」を参照してください。|  
|順位付け関数|*順位付け関数*|順位付け関数は、ネイティブ コンパイル ストアド プロシージャではサポートされていません。 プロシージャの定義から削除します。|  
|機能|*Function*|この関数はサポートされません。 ネイティブ コンパイル T-SQL モジュールでサポートされている関数の詳細については、「[ネイティブ コンパイル T-SQL モジュールでサポートされる機能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)」を参照してください。|  
|ステートメント|*ステートメント*|このステートメントはサポートされていません。 ネイティブ コンパイル T-SQL モジュールでサポートされている関数の詳細については、「[ネイティブ コンパイル T-SQL モジュールでサポートされる機能](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md)」を参照してください。|  
|特徴量|バイナリおよび文字列で使用される MIN と MAX|集計関数 **MIN** および **MAX** は、ネイティブ コンパイル ストアド プロシージャ内の文字やバイナリ文字列値に使用できません。|  
|特徴量|GROUP BY ALL|ALL は、ネイティブ コンパイル ストアド プロシージャ内の GROUP BY 句では使用できません。 GROUP BY 句から ALL を削除します。|  
|特徴量|GROUP BY ()|空のリストによる GROUP BY はサポートされていません。 GROUP BY 句を削除するか、グループ化リストに列を含めます。|  
|特徴量|ROLLUP|**ROLLUP** は、ネイティブ コンパイル ストアド プロシージャ内の **GROUP BY** 句では使用できません。 プロシージャの定義から **ROLLUP** を削除します。|  
|特徴量|CUBE|**CUBE** は、ネイティブ コンパイル ストアド プロシージャ内の **GROUP BY** 句では使用できません。 プロシージャの定義から **CUBE** を削除します。|  
|特徴量|GROUPING SETS|**GROUPING SETS** は、ネイティブ コンパイル ストアド プロシージャ内の **GROUP BY** 句では使用できません。 プロシージャの定義から **GROUPING SETS** を削除します。|  
|特徴量|BEGIN TRANSACTION、COMMIT TRANSACTION、ROLLBACK TRANSACTION|ATOMIC ブロックを使用してトランザクションおよびエラー処理を制御します。 詳細については、「 [Atomic Blocks](../../relational-databases/in-memory-oltp/atomic-blocks-in-native-procedures.md)」を参照してください。|  
|特徴量|インライン テーブル変数の宣言。|テーブル変数は、明示的に定義されたメモリ最適化テーブル型を参照する必要があります。 メモリ最適化テーブル型を作成し、(インライン型を指定する変わりに) 変数の宣言でその型を使用します。|  
|特徴量|ディスク ベース テーブル|ディスク ベース テーブルには、ネイティブ コンパイル ストアド プロシージャからアクセスできません。 ディスク ベース テーブルへの参照をネイティブ コンパイル ストアド プロシージャから削除します。 または、ディスク ベース テーブルをメモリ最適化テーブルに移行します。|  
|特徴量|ビュー|ビューには、ネイティブ コンパイル ストアド プロシージャからアクセスできません。 ビューではなく、基になるベース テーブルを参照します。|  
|特徴量|テーブル値関数|**適用対象:** [!INCLUDE[ssSDSFull_md](../../includes/ssSDSFull-md.md)] および [!INCLUDE[ssSQL15-md](../../includes/sssql15-md.md)] 以降の SQL Server<br/>複数ステートメントのテーブル値関数には、ネイティブ コンパイル T-SQL モジュールからアクセスできません。 インライン テーブル値関数はサポートされていますが、NATIVE_COMPILATION で作成する必要があります。<br/><br/>**適用対象**: [!INCLUDE[ssSQL14-md](../../includes/ssSQL14-md.md)]<br/>テーブル値関数はネイティブ コンパイル T-SQL モジュールから参照できません。|  
|オプション|PRINT|参照を削除します。|  
|特徴量|DDL (DDL)|DDL はネイティブ コンパイル T-SQL モジュールでサポートされていません。|  
|オプション|STATISTICS XML|サポートされていません。 STATISTICS XML を有効にしてクエリを実行すると、ネイティブ コンパイル ストアド プロシージャの部分が欠如した XML コンテンツが返されます。|  
  
## <a name="transactions-that-access-memory-optimized-tables"></a>メモリ最適化テーブルにアクセスするトランザクション  
 次の表に、メモリ最適化テーブルにアクセスするトランザクションに関連したエラー メッセージのテキストに表示される可能性がある [!INCLUDE[tsql](../../includes/tsql-md.md)] の機能およびキーワードと、エラーを解決するための修正措置を示します。  
  
|Type|名前|解決方法|  
|----------|----------|----------------|  
|特徴量|セーブポイント (savepoint)|メモリ最適化テーブルにアクセスするトランザクション内での明示的なセーブポイントの作成はサポートされていません。|  
|特徴量|バインドされたトランザクション|バインドされたセッションは、メモリ最適化テーブルにアクセスするトランザクションに参加できません。 プロシージャを実行する前にセッションをバインドしないでください。|  
|特徴量|DTC|メモリ最適化テーブルにアクセスするトランザクションは、分散トランザクションにすることはできません。|  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP への移行](./plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)  
  
