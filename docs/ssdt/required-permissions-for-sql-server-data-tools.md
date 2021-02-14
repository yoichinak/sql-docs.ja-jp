---
title: 必要なアクセス許可
description: データベースの作成、単体テストの実行、スキーマの比較など、SQL Server Data Tools のさまざまなタスクに必要なアクセス許可について説明します。
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: b27038c4-94ab-449c-90b7-29d87ce37a8b
author: markingmyname
ms.author: maghan
ms.reviewer: “”
ms.openlocfilehash: 6e519a3786b45d87344f8f5f5355353fd5865d62
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100072456"
---
# <a name="required-permissions-for-sql-server-data-tools"></a>SQL Server Data Tools に必要な権限

Visual Studio でデータベースに対してアクションを実行する前に、そのデータベースに対して特定の権限を持つアカウントを使用してログオンする必要があります。 必要となる特定の権限は、実行するアクションによって異なります。 以下のセクションでは、実行する各アクションと、そのアクションの実行に必要な特定の権限について説明します。  
  
-   [データベースを作成または配置する権限](#DatabaseCreationAndDeploymentPermissions)  
  
-   [データベースをリファクタリングする権限](#DatabaseRefactoringPermissions)  
  
-   [SQL Server データベースで単体テストを実行する権限](#DatabaseUnitTestingPermissions)  
  
-   [データを生成する権限](#DataGenerationPermissions)  
  
-   [スキーマとデータを比較する権限](#SchemaAndDataComparePermissions)  
  
-   [Transact-SQL エディターを実行する権限](#Transact-SQLEditorPermissions)  
  
-   [SQL Server 共通言語ランタイム (SQL CLR) プロジェクトに対する権限](#SQLCLRPermissions)  
  
## <a name="permissions-to-create-or-deploy-a-database"></a><a name="DatabaseCreationAndDeploymentPermissions"></a>データベースを作成または配置する権限  
データベースを作成または配置するには、次の権限が必要です。  
  
|Actions|必要なアクセス許可|  
|-|-|  
|データベースのオブジェクトと設定をインポートする|ソース データベースに接続できる必要があります。<br /><br />ソース データベースが SQL Server 2005 に基づいている場合、各オブジェクトに対する **VIEW DEFINITION** 権限も必要です。<br /><br />ソース データベースが SQL Server 2008 以降に基づいている場合、各オブジェクトに対する **VIEW DEFINITION** 権限も必要です。 ログインには、(データベース暗号化キーに対する) **VIEW SERVER STATE** 権限が必要です。|  
|サーバーのオブジェクトと設定をインポートする|指定されたサーバー上の master データベースに接続できる必要があります。<br /><br />サーバーで SQL Server 2005 が実行されている場合、サーバーに対する **VIEW ANY DEFINITION** 権限が必要です。<br /><br />ソース データベースが SQL Server 2008 以降に基づいている場合、サーバーに対する **VIEW ANY DEFINITION** 権限が必要です。 ログインには、(データベース暗号化キーに対する) **VIEW SERVER STATE** 権限が必要です。|  
|データベース プロジェクトを作成または更新する|データベース プロジェクトを作成または変更するには、データベースの権限は不要です。|  
|新しいデータベースを配置する、または **[データベースを常に再作成する]** オプションを設定した状態で配置する|**CREATE DATABASE** 権限があるか、ターゲット サーバーの **dbcreator** ロールのメンバーである必要があります。<br /><br />データベースを作成すると、Visual Studio は model データベースに接続してその内容をコピーします。 ターゲット データベースへの接続に使用する最初のログイン (*yourLogin* など) には、**db_creator** 権限と **CONNECT SQL** 権限が必要です。 このログインには、model データベースへのユーザー マッピングが必要です。 **sysadmin** 権限がある場合は、次の Transact\-SQL ステートメントを実行してマッピングを作成できます。<br /><br />`USE [model] CREATE USER yourUser FROM LOGIN yourLogin`<br /><br />ユーザー (この例では、yourUser) には、model データベースに対する **CONNECT** 権限と **VIEW DEFINITION** 権限が必要です。 **sysadmin** 権限を持っている場合、次の Transact\-SQL ステートメントを実行してこれらの権限を付与できます。<br /><br />`USE [model] GRANT CONNECT to yourUser GRANT VIEW DEFINITION TO yourUser`<br /><br />名前のない制約が含まれているデータベースを配置し、**CheckNewContraints** オプションが有効な場合 (このオプションは既定では有効になっています)、**db_owner** 権限または **sysadmin** 権限がないと、配置に失敗します。 これは、名前のない制約のみに当てはまります。 **CheckNewConstraints** オプションの詳細については、「[データベース プロジェクト設定の概要](../ssdt/database-project-settings.md)」を参照してください。|  
|既存のデータベースに更新を配置する|有効なデータベース ユーザーである必要があります。 また、**db_ddladmin** ロールのメンバーであるか、スキーマを所有しているか、ターゲット データベースで作成または変更するオブジェクトを所有している必要があります。 配置前スクリプトまたは配置後スクリプトでログインやリンク サーバーなどの高度な概念を使用するには、追加の権限が必要です。<br /><br />**注:** master データベースを配置する場合は、配置先のサーバーに対する **VIEW ANY DEFINITION** 権限も必要です。|  
|データベース プロジェクトの EXTERNAL_ACCESS オプションでアセンブリを使用する|データベース プロジェクトの TRUSTWORTHY プロパティを設定する必要があります。 SQL Server ログインには、EXTERNAL ACCESS ASSEMBLY 権限が必要です。|  
|アセンブリを新しいデータベースまたは既存のデータベースに配置する|ターゲット配置サーバーで sysadmin ロールのメンバーであることが必要です。|  
  
詳しくは、SQL Server オンライン ブックをご覧ください。  
  
## <a name="permissions-to-refactor-a-database"></a><a name="DatabaseRefactoringPermissions"></a>データベースをリファクタリングする権限  
*データベース リファクタリング* は、データベース プロジェクト内でのみ行われます。 データベース プロジェクトを使用する権限が必要です。 変更をターゲット データベースに配置するまで、ターゲット データベースに対する権限は不要です。  
  
## <a name="permissions-to-perform-unit-testing-on-a-sql-server-database"></a><a name="DatabaseUnitTestingPermissions"></a>SQL Server データベースで単体テストを実行する権限  
データベースで単体テストを実行するには、次の権限が必要です。  
  
|Actions|必要なアクセス許可|  
|-|-|   
|テスト アクションを実行する|実行コンテキストのデータベース接続を使用する必要があります。 詳細については、「[接続文字列とアクセス許可の概要](../ssdt/overview-of-connection-strings-and-permissions.md)」を参照してください。|  
|事前テスト アクションまたは事後テスト アクションを実行する|特権コンテキストのデータベース接続を使用する必要があります。 このデータベース接続では、実行コンテキスト接続よりも多くの権限が認められます。|  
|TestInitialize スクリプトと TestCleanup スクリプトを実行する|特権コンテキストのデータベース接続を使用する必要があります。|  
|テストの実行前にデータベースの変更を配置する|特権コンテキストのデータベース接続を使用する必要があります。 詳細については、「[SQL Server の単体テストの実行を構成する方法](../ssdt/how-to-configure-sql-server-unit-test-execution.md)」を参照してください。|  
|テストの実行前にデータを生成する|特権コンテキストのデータベース接続を使用する必要があります。 詳細については、「[SQL Server の単体テストの実行を構成する方法](../ssdt/how-to-configure-sql-server-unit-test-execution.md)」を参照してください。|  
  
## <a name="permissions-to-generate-data"></a><a name="DataGenerationPermissions"></a>データを生成する権限  
データ ジェネレーターを使用してテスト データを生成するには、ターゲット データベース内のオブジェクトに対する **INSERT** 権限と **SELECT** 権限が必要です。 データを生成する前にデータを消去する場合は、ターゲット データベース内のオブジェクトに対する **DELETE** 権限も必要です。 テーブルの **IDENTITY** 列を再設定するには、そのテーブルを所有しているか、db_owner ロールまたは db_ddladmin ロールのメンバーである必要があります。  
  
## <a name="permissions-to-compare-schemas-and-data"></a><a name="SchemaAndDataComparePermissions"></a>スキーマとデータを比較する権限  
スキーマまたはデータを比較するには、次の権限が必要です。  
  
|Actions|必要なアクセス許可|  
|-|-|   
|2 つのデータベースのスキーマを比較する|データベースからオブジェクトと設定をインポートするための権限が必要です (「[データベースを作成または配置する権限](#DatabaseCreationAndDeploymentPermissions)」を参照してください)。|  
|データベースとデータベース プロジェクトのスキーマを比較する|データベースからオブジェクトと設定をインポートするための権限が必要です (「[データベースを作成または配置する権限](#DatabaseCreationAndDeploymentPermissions)」を参照してください)。 また、Visual Studio でデータベース プロジェクトを開いておくことも必要です。|  
|ターゲット データベースに更新を書き込む|ターゲット データベースに更新を配置するための権限が必要です (「[データベースを作成または配置する権限](#DatabaseCreationAndDeploymentPermissions)」を参照してください)。|  
|2 つのデータベースのデータを比較する|2 つのデータベースのスキーマを比較するために必要な権限に加えて、比較するすべてのテーブルに対する **SELECT** 権限、および **VIEW DATABASE STATE** 権限も必要です。|  
  
詳しくは、SQL Server オンライン ブックをご覧ください。  
  
## <a name="permissions-to-run-the-transact-sql-editor"></a><a name="Transact-SQLEditorPermissions"></a>Transact\-SQL エディターを実行する権限  
Transact\-SQL エディター内で実行できる操作は、ターゲット データベースへの実行コンテキストによって決まります。  
  
## <a name="permissions-for-sql-server-common-language-run-time-projects"></a><a name="SQLCLRPermissions"></a>SQL Server 共通言語ランタイム (SQL CLR) プロジェクトに対する権限  
CLR プロジェクトを配置またはデバッグするために必要な権限を次の表に示します。  
  
|Actions|必要なアクセス許可|  
|-----------|------------------------|  
|SAFE 権限セットのアセンブリを配置する (初期または増分)|db_DDLAdmin - 配置するアセンブリとオブジェクトの種類に対する CREATE 権限と ALTER 権限が付与されます。<br /><br />データベース レベルの VIEW DEFINITION - 配置するために必要です。<br /><br />データベース レベルの CONNECT - データベースに接続する権限が付与されます。|  
|external_access 権限セットのアセンブリを配置する|db_DDLAdmin - 配置するアセンブリとオブジェクトの種類に対する CREATE 権限と ALTER 権限が付与されます。<br /><br />データベース レベルの VIEW DEFINITION - 配置するために必要です。<br /><br />データベース レベルの CONNECT - データベースに接続する権限が付与されます。<br /><br />さらに、次のことも必要です。<br /><br />TRUSTWORTHY データベース オプションが ON に設定されている。<br /><br />配置に使用するログインが EXTERNAL ACCESS ASSEMBLY サーバー権限を持っている。|  
|UNSAFE 権限セットのアセンブリを配置する|db_DDLAdmin - 配置するアセンブリとオブジェクトの種類に対する CREATE 権限と ALTER 権限が付与されます。<br /><br />データベース レベルの VIEW DEFINITION - 配置するために必要です。<br /><br />データベース レベルの CONNECT - データベースに接続する権限が付与されます。<br /><br />さらに、次のことも必要です。<br /><br />TRUSTWORTHY データベース オプションが ON に設定されている。<br /><br />配置に使用するログインが UNSAFE ASSEMBLY サーバー権限を持っている。|  
|SQL CLR アセンブリのリモート デバッグを実行する|sysadmin 固定ロールの権限が必要です。|  
  
> [!IMPORTANT]  
> どのような場合でも、アセンブリの所有者は、アセンブリの配置に使用しているユーザーであるか、そのユーザーがメンバーとして属しているロールであることが必要です。 この要件は、配置するアセンブリによって参照されるアセンブリにも適用されます。  
  
## <a name="see-also"></a>参照  
[SQL Server の単体テストの作成と定義](../ssdt/creating-and-defining-sql-server-unit-tests.md)  
[SQL Server Data Tools](../ssdt/sql-server-data-tools.md)  
  
