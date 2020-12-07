---
description: オプション (SQL Server オブジェクト エクスプローラー - [スクリプト作成] ページ)
title: オプション (SQL Server オブジェクト エクスプローラー - [スクリプト作成] ページ)
ms.custom: seo-lt-2019
ms.date: 08/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.ObjectExplorerScripting
- VS.ToolsOptionsPages.Sql_Server_Object_Explorer.ObjectExplorerScripting
ms.assetid: 6105aec9-1b72-4cb2-bd24-fc35f6d95240
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 35a255bb4df3779897ec40da29da9cc15f62ba1f
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037630"
---
# <a name="options-sql-server-object-explorer---scripting-page"></a>オプション (SQL Server オブジェクト エクスプローラー - [スクリプト作成] ページ)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
 このページを使用すると、**オブジェクト エクスプローラー**内にあるオブジェクトのコンテキスト メニューの次の各コマンドに適用されるスクリプト オプションを設定できます。  
  
-   ユーザー テーブルおよびビューに対する **[編集]** コマンド。  
  
-   ユーザーが作成したオブジェクトに対する **[<object> をスクリプト化]** コマンド。  
  
-   ユーザーが作成したオブジェクトに対する **[変更]** コマンド。  
  
-   このページでは、 **SQL Server スクリプト生成ウィザード**で使用するスクリプト オプションの既定値も設定できます。  
  
## <a name="remarks"></a>解説  
**[編集]** コマンドおよび **[変更]** コマンドを実行した場合は、同じオプション設定に対して **[<object> をスクリプト化]** コマンドを実行した場合と異なる結果になることがあります。 **[編集]** コマンドおよび **[変更]** コマンドは、クエリ エディター セッション中に現在のデータベースでオブジェクトを変更するために設計されています。 **[<object> をスクリプト化]** コマンドは、後でオブジェクトの作成に使用できるスクリプトを生成するために設計されています。  
  
## <a name="options"></a>オプション  
スクリプト オプションを指定するには、各オプションの右にあるリストから、いずれかの設定を選択します。

> [!NOTE]
> 一覧表示される既定の設定は、**[データベース全体とすべてのデータベース オブジェクトのスクリプトを作成]** オプションにのみ適用されます。**[特定のデータベース オブジェクトの選択]** オプションを使用すると、異なる場合があります。
  
### <a name="general-scripting-options"></a>全般スクリプト作成オプション  
**[各ステートメントを区切る]**  
バッチ区切り記号を使用して、個々の [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを区切ります。 **クエリ エディター**の既定のバッチ区切り記号を変更するには、 **[ツール]**/**[オプション]**/**[クエリ実行]**/**[SQL Server]**/**[全般]**/**[バッチ区切り記号]** の順に選択します。 既定値は False です。 詳細については、「 [GO (Transact-SQL)](../../t-sql/language-elements/sql-server-utilities-statements-go.md)」を参照してください。  
  
**[説明用ヘッダーを含める]**  
スクリプトをオブジェクトごとのセクションに分割し、説明用のコメントを追加します。 既定値は True です。 詳細については、「 [/ *...* / (コメント) (Transact-SQL)](../../t-sql/language-elements/slash-star-comment-transact-sql.md)」を参照してください。  
  
**[Include enabling vardecimal compression]\(vardecimal 圧縮の有効化を含める\)**  
vardecimal ストレージ オプションを含めます。 既定値は False です。 詳細については、「[sp_db_vardecimal_storage_format (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)」を参照してください。  
  
**[変更の追跡のスクリプトを作成]**  
変更の追跡の情報をスクリプトに含めます。  
  
**[フルテキスト カタログのスクリプトを作成]**  
フルテキスト カタログのスクリプトを含めます。 既定値は False です。 詳細については、「 [CREATE FULLTEXT CATALOG (Transact-SQL)](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)」を参照してください。  
  
**[USE のスクリプトを作成] <database>**  
スクリプトに USE &lt;データベース&gt; ステートメントを追加することにより、現在の **オブジェクト エクスプローラー** データベースのコンテキストでデータベース オブジェクトを作成します。 スクリプトが別のデータベースで使用される可能性がある場合は、False を選択して除外します。 既定値は True です。 詳細については、「 [USE (Transact-SQL)](../../t-sql/language-elements/use-transact-sql.md)」を参照してください。  
  
### <a name="object-scripting-options"></a>オブジェクト スクリプト作成オプション  

**[オブジェクトの有無を確認する]** 指定された名前のオブジェクトが削除または変更される前に存在していたこと、または指定された名前のオブジェクトが作成前に存在していないことを確認します。 詳細については、「 [IF...ELSE (Transact-SQL)](../../t-sql/language-elements/if-else-transact-sql.md) 」と「 [EXISTS (Transact-SQL)](../../t-sql/language-elements/exists-transact-sql.md)」を参照してください。

**[依存オブジェクトのスクリプトを生成する]**  
選択したオブジェクトのスクリプトを実行する際に必要な追加オブジェクトのスクリプトを生成します。 既定値は False です。  
  
**[オブジェクト名を修飾するスキーマ]**  
オブジェクト名をオブジェクト スキーマで修飾します。 既定値は False です。 詳細については、「 [データベース スキーマの作成](../../relational-databases/security/authentication-access/create-a-database-schema.md)」を参照してください。  

**[データ圧縮オプションのスクリプトを作成]** データ圧縮オプションをスクリプトに含めます。 既定値は False です。

**[拡張プロパティのスクリプトを作成]**  
オブジェクトに拡張プロパティが含まれている場合、それらの拡張プロパティをスクリプトに追加します。 既定値は False です。 詳細については、「 [sp_addextendedproperty (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md)」を参照してください。  
  
**[所有者のスクリプトを作成]**  
生成されたスクリプトに所有者を含めます。 既定値は False です。  
  
**[権限のスクリプトを作成]**  
データベース オブジェクトに対する権限をスクリプトに含めます。 既定値は True です。 詳細については、「 [アクセス許可](../../relational-databases/security/permissions-database-engine.md)」を参照してください。  
  
### <a name="tableview-options"></a>テーブル/ビュー オプション  
次のオプションは、テーブルまたはビューのスクリプトのみに適用されます。  
  
**[ユーザー定義データ型から基本データ型に変換します]**  
ユーザー定義データ型を元の基本型に変換します。 スクリプトを実行するデータベースに、ソース データベースのユーザー定義データ型が存在しない場合は、True を使用します。 ユーザー定義データ型を保持する場合は、False を使用します。 既定値は False です。 詳細については、「 [CREATE TYPE (Transact-SQL)](../../t-sql/statements/create-type-transact-sql.md)」を参照してください。  
  
**[SET ANSI PADDING コマンドを生成する]**  
各 CREATE TABLE ステートメントの前後に SET ANSI_PADDING ステートメントを追加します。 既定値は True です。 詳細については、「 [SET ANSI_PADDING (Transact-SQL)](../../t-sql/statements/set-ansi-padding-transact-sql.md)」を参照してください。  
  
**[照合順序を含める]**  
列定義に照合順序を含めます。 既定値は True です。 詳細については、「 [Collation and Unicode Support](../../relational-databases/collations/collation-and-unicode-support.md)」を参照してください。  
  
**[IDENTITY プロパティを含める]**  
IDENTITY シードおよび IDENTITY インクリメントの定義を含めます。 既定値は True です。 詳細については、「 [IDENTITY (プロパティ) (Transact-SQL)](../../t-sql/statements/create-table-transact-sql-identity-property.md)」を参照してください。  
  
**[外部キー参照を修飾するスキーマ]**  
FOREIGN KEY 制約のテーブル参照にスキーマ名を追加します。 既定値は True です。  
  
**[バインドされた既定値およびルールのスクリプトを作成]**  
バインド ストアド プロシージャ **sp_bindefault** および **sp_bindrule** の呼び出しを含めます。 既定値は True です。 詳細については、「 [sp_bindefault (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md) 」と「 [sp_bindrule (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-bindrule-transact-sql.md)」を参照してください。  
  
**[CHECK 制約のスクリプトを作成]**  
スクリプトに [CHECK 制約](../../relational-databases/tables/unique-constraints-and-check-constraints.md) を追加します。 既定値は True です。  
  
**[既定のスクリプトを作成]**  
スクリプトに列の既定値を含めます。 既定値は False です。 詳細については、「 [CREATE DEFAULT (Transact-SQL)](../../t-sql/statements/create-default-transact-sql.md)」を参照してください。  
  
**[ファイル グループのスクリプトを作成]**  
テーブル定義で ON 句にファイル グループを指定します。 既定値は False です。 詳細については、「 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)」を参照してください。  
  
**[外部キーのスクリプトを作成]**  
スクリプトに [FOREIGN KEY 制約](../../relational-databases/tables/primary-and-foreign-key-constraints.md) を含めます。 既定値は False です。  
  
**[フルテキスト インデックスのスクリプトを作成]**  
スクリプトにフルテキスト インデックスを含めます。 既定値は False です。 詳細については、「 [CREATE FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/create-fulltext-index-transact-sql.md)」を参照してください。  
  
**[インデックスのスクリプトを作成]**  
スクリプトにクラスター化、非クラスター化、および XML インデックスを含めます。 既定値は True です。 詳細については、「 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)」を参照してください。  
  
**[パーティション構成のスクリプトを作成]**  
スクリプトにテーブル パーティション分割構成を含めます。 既定値は False です。 詳細については、「 [CREATE PARTITION SCHEME (Transact-SQL)](../../t-sql/statements/create-partition-scheme-transact-sql.md)」を参照してください。  
  
**[主キーのスクリプトを作成]**  
スクリプトに [PRIMARY KEY 制約](../../relational-databases/tables/primary-and-foreign-key-constraints.md) を含めます。 既定値は True です。  
  
**[統計のスクリプトを作成]**  
スクリプトにユーザー定義統計を含めます。 既定値は False です。 詳細については、「 [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)」をご覧ください。  
  
**[トリガーのスクリプトを作成]**  
スクリプトにトリガーを含めます。 既定値は False です。 詳細については、「 [CREATE TRIGGER (Transact-SQL)](../../t-sql/statements/create-trigger-transact-sql.md)」をご覧ください。  
  
**[一意キーのスクリプトを作成]**  
スクリプトに [UNIQUE 制約と CHECK 制約](../../relational-databases/tables/unique-constraints-and-check-constraints.md) を含めます。 既定値は False です。  
  
**[ビュー列のスクリプトを作成]**  
ビュー ヘッダーにビュー列を宣言します。 既定値は False です。 詳細については、「 [CREATE VIEW (Transact-SQL)](../../t-sql/statements/create-view-transact-sql.md)」を参照してください。  
  
**[Include dri system names]\(dri システム名を含める\)**  
宣言参照整合性を適用するために、システムによって生成される制約名を含めます。 既定値は False です。 詳細については、「 [REFERENTIAL_CONSTRAINTS (Transact-SQL)](../../relational-databases/system-information-schema-views/referential-constraints-transact-sql.md)」を参照してください。  
  
### <a name="version-options"></a>バージョン オプション

**[スクリプト設定をソースに一致させる]** ターゲット バージョンが有効な場合、生成されたスクリプトのエンジン エディションとエンジンの種類が、スクリプト化されるオブジェクトのサーバーの値に設定されます。 これにより他のバージョンのオプションが無効化 (無視) されます。 

**[データベース エンジン エディションのスクリプト]** 生成されたスクリプトは、指定した[エンジン エディション](/dotnet/api/microsoft.sqlserver.management.smo.edition)のターゲットになります。

**[データベース エンジンの種類に対応したスクリプト]** 生成されたスクリプトは、指定した[データベース エンジンの種類](/previous-versions/sql/sql-server-2014/ee642509(v=sql.120))のターゲットになります。

**[サーバーのバージョン互換のスクリプト]**  
生成されたスクリプトは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の指定したバージョンのターゲットになります。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の新機能のスクリプトを以前のバージョン用に生成することはできません。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 用に作成したスクリプトには、以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で動作しているサーバーや、以前の [データベース互換性レベルの設定](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)が適用されているデータベースに対して実行できないものもあります。  

## <a name="see-also"></a>関連項目  
[スクリプトの生成 (SQL Server Management Studio)](../scripting/generate-scripts-sql-server-management-studio.md)  
