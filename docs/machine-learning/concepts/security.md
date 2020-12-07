---
title: 機能拡張に関するセキュリティ アーキテクチャ
description: この記事では、SQL Server Machine Learning Services の機能拡張フレームワークに関するセキュリティ アーキテクチャについて説明します。 これには、ログインとユーザー アカウント、SQL Server スタート パッド サービス、ワーカー アカウント、実行中の複数のスクリプト、およびファイルのアクセス許可に関するセキュリティが含まれます。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.custom: contperfq1, seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: eb5ab3d1f6408bb63d194b964626bf303ba9e249
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870013"
---
# <a name="security-architecture-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services の機能拡張フレームワークに関するセキュリティ アーキテクチャ

[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

この記事では、[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) で SQL Server データベース エンジンおよび関連するコンポーネントと機能拡張フレームワークを統合するために使用されるセキュリティ アーキテクチャについて説明します。 セキュリティ保護可能なリソース、サービス、プロセス ID、およびアクセス許可について詳しく説明します。 この記事で取り上げた主なポイントは、スタート パッド、SQLRUserGroup、およびワーカー アカウントの目的、外部スクリプトのプロセス分離、ユーザー ID をワーカーアカウントにマップする方法です。

SQL Server での機能拡張の主要概念とコンポーネントの詳細については、「[SQL Server Machine Learning Services の機能拡張アーキテクチャ](extensibility-framework.md)」を参照してください。

## <a name="securables-for-external-script"></a>外部スクリプトでのセキュリティ保護可能リソース

外部スクリプトは、この目的のために作成された[システム ストアド プロシージャ](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)に入力パラメーターとして送信されるか、または定義したストアド プロシージャでラップされます。 このスクリプトは、R、Python、または Java や .NET などの外部言語で記述されています。 または、事前にトレーニングされ、バイナリ形式でデータベース テーブルに格納され、T-SQL [PREDICT](../../t-sql/queries/predict-transact-sql.md) 関数で呼び出し可能なモデルを使用することもできます。

スクリプトは、既存のデータベース スキーマ オブジェクト、ストアド プロシージャ、およびテーブルによって提供されるため、SQL Server Machine Learning Services では新しい[セキュリティ保護可能なリソース](../../relational-databases/security/securables.md)はありません。

スクリプトの使用方法や、スクリプトが何で構成されているかにかかわらず、データベース オブジェクトは作成され、多くの場合、保存されますが、スクリプトを格納するための新しいオブジェクト型は導入されていません。 このため、データベース オブジェクトを使用、作成、および保存できるかどうかは、ユーザーに対して既に定義されているデータベースのアクセス許可に大きく依存します。

<a name="permissions"></a>

## <a name="permissions"></a>アクセス許可

SQL Server のデータベース ログインとロールのデータ セキュリティ モデルは、外部スクリプトにまで拡張されています。 SQL Server データを使用する外部スクリプトまたはコンピューティング コンテキストとして SQL Server で実行される外部スクリプトを実行する場合、SQL Server ログインまたは Windows ユーザー アカウントが必要です。 クエリを実行するアクセス許可を持つデータベース ユーザーは、外部スクリプトから同じデータにアクセスできます。

ログインまたはユーザー アカウントによって、外部スクリプトの要件に応じて、複数レベルのアクセスを必要とする場合のある *セキュリティ プリンシパル* が特定されます。

+ 外部スクリプトが有効になっているデータベースにアクセスするためのアクセス許可。
+ テーブルなどのセキュリティで保護されたオブジェクトからデータを読み取るためのアクセス許可。
+ モデルやスコア付けの結果など、新しいデータをテーブルに書き込むための許可。
+ テーブル、外部スクリプトを使用するストアド プロシージャ、外部スクリプト ジョブを使用するカスタム関数など、新しいオブジェクトを作成するための許可。
+ SQL Server コンピューターに新しいパッケージをインストールする権限、またはユーザーのグループに提供されるパッケージを使用する権限。

実行コンテキストとして SQL Server を使用して外部スクリプトを実行する各ユーザーを、データベース内のユーザーにマップする必要があります。 データベース ユーザーのアクセス許可を個別に設定するのではなく、アクセス許可のセットを管理するロールを作成し、それらのロールにユーザーを割り当てることができます。

詳細については、「[SQL Server Machine Learning Services にユーザー アクセス許可を付与する](../../machine-learning/security/user-permission.md)」を参照してください。

## <a name="permissions-when-using-an-external-client-tool"></a>外部クライアント ツールを使用する場合のアクセス許可

外部クライアント ツールでスクリプトを使用するユーザーは、データベース内で外部スクリプトを実行したり、データベース オブジェクトやデータにアクセスしたりする必要がある場合、ログインまたはアカウントをデータベース内のユーザーにマップする必要があります。 外部スクリプトを、リモート データ サイエンス クライアントから送信するか、T-SQL ストアド プロシージャを使用して実行するかにかかわらず、同じアクセス許可が必要です。

たとえば、ローカル コンピューターで実行される外部スクリプトを作成し、そのスクリプトを SQL Server で実行したいとします。 次の条件が満たされていることを確認する必要があります。

+ データベースがリモート接続を許可します。
+ データベース アクセスに使用した SQL ログインまたは Windows アカウントが、インスタンス レベルで SQL Server に追加されています。
+ SQL ログインまたは Windows ユーザーには、外部スクリプトを実行するためのアクセス許可が必要です。 一般に、このアクセス許可を追加できるのはデータベース管理者のみです。
+ SQL ログインまたは Window ユーザーが、適切なアクセス許可を持つユーザーとして、外部スクリプトによって次の操作が実行される各データベースに追加されている必要があります。
  + データの取得。
  + データの書き込みまたは更新。
  + 新しいオブジェクト (テーブルやストアド プロシージャなど) の作成。

ログインまたは Windows ユーザー アカウントがプロビジョニングされ、必要なアクセス許可が付与された後、R のデータ ソース オブジェクトまたは Python の **revoscalepy** ライブラリを使用することで、あるいは外部スクリプトを含むストアド プロシージャを呼び出すことで、SQL Server で外部スクリプトを実行できます。

外部スクリプトが SQL Server から起動されるたびに、データベース エンジンのセキュリティによって、ジョブを開始したユーザーのセキュリティ コンテキストが取得され、セキュリティ保護可能なオブジェクトへのユーザーまたはログインのマッピングが管理されます。

このため、リモート クライアントから開始されるすべての外部スクリプトで、接続文字列の一部として、ログインまたはユーザーの情報を指定する必要があります。

<a name="launchpad"></a>

::: moniker range="=sql-server-2016||=sql-server-2017||=sqlallproducts-allversions"

## <a name="services-used-in-external-processing-launchpad"></a>外部処理で使用されるサービス (スタート パッド)

機能拡張フレームワークによって、SQL Server のインストールで [サービスの一覧](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details)に次の新しい NT サービスが追加されます:[**SQL Server Launchpad (MSSSQLSERVER)**](extensibility-framework.md#launchpad)。

データベース エンジンでは、SQL Server **スタート パッド** サービスを使用して、外部スクリプト セッションが別個のプロセスとしてインスタンス化されます。 
このプロセスは低い特権のアカウントで実行されます。 このアカウントは、SQL Server、スタート パッド自体、およびストアド プロシージャまたはホスト クエリの実行に使用されたユーザー ID とは異なります。 スクリプトを、低い特権のアカウント下の別のプロセスで実行することは、SQL Server での外部スクリプトのセキュリティおよび分離モデルの基礎です。

また SQL Server では、サテライト プロセスを開始するために使用される低い特権のワーカー アカウントへの、呼び出し元ユーザーの ID のマッピングも維持されます。 スクリプトまたはコードによって、データおよび操作のために SQL Server に対してコールバックが行われる一部の状況では、SQL Server によって、通常、ID 転送をシームレスに管理できます。 SELECT ステートメントや呼び出し元関数、およびその他のプログラミング オブジェクトを含むスクリプトは通常、呼び出し元のユーザーが十分な権限を持っていれば成功します。

> [!NOTE]
> 既定では、[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] は **NT Service\MSSQLLaunchpad** で実行されるように構成されています。これは、外部スクリプトの実行に必要なすべてのアクセス許可がプロビジョニングされています。 構成可能なオプションの詳細については、「[SQL Server Launchpad のサービスの構成](../security/sql-server-launchpad-service-account.md)」を参照してください。

::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

## <a name="services-used-in-external-processing-launchpad"></a>外部処理で使用されるサービス (スタート パッド)

機能拡張フレームワークによって、SQL Server のインストールで [サービスの一覧](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details)に次の新しい NT サービスが追加されます:[**SQL Server スタート パッド (MSSSQLSERVER)**](extensibility-framework.md#launchpad)。

データベース エンジンでは、SQL Server **スタート パッド** サービスを使用して、外部スクリプト セッションが別個のプロセスとしてインスタンス化されます。 
プロセスはスタート パッドのユーザー ID で実行されますが、AppContainer 内に含められるという制限が追加されます。 スクリプトを、AppContainer 下の別のプロセスで実行することは、SQL Server での外部スクリプトのセキュリティおよび分離モデルの基礎です。

また SQL Server では、サテライト プロセスを開始するために使用される低い特権のワーカー アカウントへの、呼び出し元ユーザーの ID のマッピングも維持されます。 スクリプトまたはコードによって、データおよび操作のために SQL Server に対してコールバックが行われる一部の状況では、SQL Server によって、通常、ID 転送をシームレスに管理できます。 SELECT ステートメントや呼び出し元関数、およびその他のプログラミング オブジェクトを含むスクリプトは通常、呼び出し元のユーザーが十分な権限を持っていれば成功します。

> [!NOTE]
> 既定では、[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] は **NT Service\MSSQLLaunchpad** で実行されるように構成されています。これは、外部スクリプトの実行に必要なすべてのアクセス許可がプロビジョニングされています。 構成可能なオプションの詳細については、「[SQL Server Launchpad のサービスの構成](../security/sql-server-launchpad-service-account.md)」を参照してください。

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

## <a name="services-used-in-external-processing"></a>外部処理で使用されるサービス

機能拡張フレームワークでは、SQL Server インストールに次の新しいデーモンが 1 つ追加されます: [mssql-launchpadd](extensibility-framework.md#launchpad)。 mssql-launchpadd は、mssql-server-extensibility パッケージをインストールしたときに作成される、低い特権のアカウント mssql_launchpadd で実行されます。

1 つのデータベース エンジン インスタンスのみがサポートされ、そのインスタンスにバインドされたスタート パッド サービスが 1 つ存在します。 スクリプトが実行されると、スタート パッド サービスでは、権限の低いユーザー アカウント mssql_satellite を使用して、独自の新しい PID、IPC、マウント、およびネットワーク名前空間で、別のスタート パッド プロセスが開始されます。 各サテライト プロセスにより、スタート パッドの mssql_satellite ユーザー アカウントが継承され、スクリプトの実行中にこのアカウントが使用されます。

詳細については、「[SQL Server Machine Learning Services の機能拡張アーキテクチャ](extensibility-framework.md)」を参照してください。

::: moniker-end

<a name="sqlrusergroup"></a>

::: moniker range="=sql-server-2016||=sql-server-2017||=sqlallproducts-allversions"

## <a name="identities-used-in-processing-sqlrusergroup"></a>処理で使用される ID (SQLRUserGroup)

**SQLRUserGroup** (SQL 制限ユーザー グループ) は、SQL Server セットアップによって作成され、低い特権のローカル Windows ユーザー アカウントのプールを含みます。 外部プロセスが必要な場合、スタート パッドでは使用可能なワーカー アカウントを取得し、それを使用してプロセスが実行されます。 具体的には、スタート パッドによって、使用可能なワーカー アカウントがアクティブ化され、それが呼び出し元ユーザーの ID にマップされ、そのワーカー アカウントでスクリプトが実行されます。

+ **SQLRUserGroup** は、特定のインスタンスにリンクされます。 Machine Learning が有効になっているインスタンスごとに、ワーカー アカウントの個別プールが必要です。 インスタンス間でアカウントを共有することはできません。

+ ユーザー アカウント プールのサイズは静的であり、既定値は 20 です。これにより、20 の同時セッションがサポートされます。 同時に起動できる外部ランタイム セッションの数は、このユーザー アカウント プールのサイズによって制限されます。 

+ プール内のワーカー アカウント名の形式は、SQLInstanceName *nn* です。 たとえば、既定のインスタンスの場合、**SQLRUserGroup** には、MSSQLSERVER01、MSSQLSERVER02 (MSSQLSERVER20 まで以後同様) という名前のアカウントが含まれます。

並列化されたタスクでは、追加のアカウントは使用されません。 たとえば、ユーザーが並列処理を使用するスコアリング タスクを実行する場合、同じワーカー アカウントがすべてのスレッドで再利用されます。 Machine Learning を頻繁に使用する場合、外部スクリプトの実行に使用するアカウントの数を増やすことができます。 詳細については、「[SQL Server Machine Learning Services での外部スクリプトの同時実行のスケーリング](../../machine-learning/administration/scale-concurrent-execution-external-scripts.md)」を参照してください。

### <a name="permissions-granted-to-sqlrusergroup"></a>SQLRUserGroup に付与されるアクセス許可

既定では、**SQLRUserGroup** のメンバーには、SQL Server **Binn**、**R_SERVICES**、および **PYTHON_SERVICES** ディレクトリのファイルに対する読み取りと実行のアクセス許可が付与されます。 これには、SQL Server とともにインストールされる R および Python ディストリビューションの実行可能ファイル、ライブラリ、および組み込みデータセットへのアクセス権が含まれます。 

SQL Server の機密性の高いリソースを保護するために、**SQLRUserGroup** へのアクセスを拒否するアクセス制御リスト (ACL) を必要に応じて定義できます。 逆に、SQL Server 自体とは別のホスト コンピューターに存在するローカル データ リソースへのアクセス許可を付与することもできます。 

仕様により、**SQLRUserGroup** には、データベース ログインまたはデータへのアクセス許可はありません。 特定の状況、特に信頼された Windows ID が呼び出し元のユーザーである場合、ループバック接続を許可するログインを作成できます。 この機能は、[*暗黙の認証*](#implied-authentication)と呼ばれます。 詳細については、[データベース ユーザーとしての SQLRUserGroup の追加](../../machine-learning/security/create-a-login-for-sqlrusergroup.md)に関する記事を参照してください。

## <a name="identity-mapping"></a>ID のマッピング

セッションを開始すると、スタート パッドによって、呼び出し元のユーザーの ID がワーカー アカウントにマップされます。 ワーカー アカウントに対する外部の Windows ユーザーまたは有効な SQL ログインのマッピングは、外部スクリプトを実行する SQL ストアド プロシージャの有効期間中のみ有効です。 同じログインからの並列クエリは、同じユーザー ワーカー アカウントにマップされます。

実行中、スタート パッドではセッション データを格納する一時フォルダーが作成され、セッションの終了時にそれらは削除されます。 ディレクトリへのアクセスは制限されます。 R の場合、RLauncher がこのタスクを実行します。 Python の場合、PythonLauncher がこのタスクを実行します。 個々のワーカー アカウントは、その所有フォルダーに制限され、その所有レベルを超えているフォルダー内のファイルにはアクセスできません。 ただし、ワーカー アカウントは、作成されたセッション作業フォルダーの下位にある子の読み取り、書き込み、または削除を行うことができます。 コンピューターの管理者であれば、各プロセスによって作成されたディレクトリを表示できます。 各ディレクトリはセッション GUID によって識別されます。

::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

## <a name="appcontainer-isolation"></a>AppContainer の分離

[AppContainer](/windows/desktop/secauthz/appcontainer-isolation) によって分離が実現されます。 実行時に、ストアド プロシージャまたはクエリで外部スクリプトが検出されると、拡張機能固有の起動ツールの要求を使用して SQL Server からスタート パッドが呼び出されます。 Launchpad は、自身の ID の下のプロセスで適切なランタイム環境を呼び出し、AppContainer をインスタンス化して、それを含めます。 ローカル アカウントとパスワードの管理が不要になったため、これは有益な変更です。 また、ローカル ユーザー アカウントが禁止されているインストールでは、ローカル ユーザー アカウントの依存関係を削除することで、この機能を使用できるようになります。

AppContainer は、SQL Server に実装されているため、内部メカニズムです。 プロセス モニターには AppContainer の物理的な証拠は表示されませんが、セットアップによって作成された、プロセスによるネットワーク呼び出しを防ぐための送信ファイアウォール規則で AppContainer を見つけることができます。 詳細については、「[SQL Server Machine Learning Services のファイアウォール構成](../../machine-learning/security/firewall-configuration.md)」を参照してください。

## <a name="identity-mapping"></a>ID のマッピング

セッションを開始すると、呼び出し元のユーザーの ID がスタート パッドによって **AppContainer** にマップされます。

> [!Note]
> SQL Server 2019 以降では、**SQLRUserGroup** には、複数のワーカー アカウントではなく、1 つの SQL Server スタート パッド サービス アカウントとなったメンバーが 1 つだけ用意されます。

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

## <a name="identity-mapping"></a>ID のマッピング

**スタート パッド** (ダブル 'D' - [mssql-launchpadd](extensibility-framework.md#launchpad)) デーモンでは、"スタート パッド GUID" フォルダーとサテライト証明書を使用して、呼び出し元ユーザーの ID が別の **スタート パッド** (シングル 'D') プロセスにマップされます。 これらのスタート パッド GUID フォルダーは `/var/opt/mssql-extensibility/data/` の下に作成されます。 スタート パッド プロセスでは、この証明書を使用して SQL に対する認証が実行され、スタート パッド GUID フォルダーの下に各セッション GUID 用の一時フォルダーが作成されます。 サテライト (R、Python、または ExtHost) プロセスには、スタート パッド GUID フォルダー、その下の証明書、およびそのセッション GUID フォルダーへのアクセス権があります。

次の SQL スクリプトでは、スタート パッドのフォルダーの内容が出力されます。

```sql
EXECUTE sp_execute_external_script @language = N'R'
    ,@script = N'
print("Contents of /var/opt/mssql-extensibility/data :");
print(system("ls -al /var/opt/mssql-extensibility/data"));
print("Contents of Launchpad GUID folder:");
print(system("ls -al /var/opt/mssql-extensibility/data/*"));
print(system("ls -al /var/opt/mssql-extensibility/data/*/*"))
'
    ,@input_data_1 = N'SELECT 1 AS hello'
```

::: moniker-end

<a name="implied-authentication"></a>

::: moniker range="=sql-server-2016||=sql-server-2017||=sqlallproducts-allversions"

## <a name="implied-authentication-loopback-requests"></a>暗黙の認証 (ループバック要求)

"*暗黙の認証*" では、接続要求の動作が示されます。これにおいては、データまたは操作のループバック要求で、低い特権のワーカー アカウントとして実行されている外部プロセスが信頼されたユーザー ID として SQL Server に提示されます。 暗黙の認証は、R または Python スクリプトなどの外部プロセスから送信される要求で、SQL Server 接続文字列によって信頼関係接続が指定されるという点で、概念として Windows 認証に固有です。 これは、"*ループバック*" と呼ばれることもあります。

信頼関係接続は外部スクリプトから使用できますが、構成を追加した場合のみ使用できます。 機能拡張アーキテクチャでは、外部プロセスはワーカー アカウントで実行され、親 **SQLRUserGroup** からアクセス許可を継承します。 接続文字列で `Trusted_Connection=True` が指定されると、ワーカー アカウントの ID が接続要求で提示されます。これは、既定では SQL Server には通知されません。

信頼関係接続を正常に確立するには、**SQLRUserGroup** のデータベース ログインを作成する必要があります。 これを行った後、**SQLRUserGroup** のメンバーからのすべての信頼関係接続に SQL Server へのログイン権限が与えられます。 詳しい手順については、[データベース ログインへの SQLRUserGroup の追加](../../machine-learning/security/create-a-login-for-sqlrusergroup.md)に関する記事を参照してください。

信頼関係接続は、最も広く使用されている接続要求の形式ではありません。 外部スクリプトで接続を指定するとき、ODBC データ ソースへの接続の場合には、SQL ログインを使用するか、または完全指定のユーザー名とパスワードを使用するのがより一般的です。

### <a name="how-implied-authentication-works-for-external-script-sessions"></a>外部スクリプト セッションでの暗黙の認証のしくみ

次の図は、SQL Server コンポーネントと言語ランタイムの相互作用、および Windows で暗黙の認証が行われる方法を示しています。

![Windows での暗黙の認証](../security/media/implied-auth-windows-2017.png)

::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

## <a name="implied-authentication-loopback-requests"></a>暗黙の認証 (ループバック要求)

"*暗黙の認証*" では、接続要求の動作が示されます。これにおいては、AppContainers で実行されている外部プロセスが、データまたは操作のループバック要求で、信頼されたユーザー ID として SQL Server に提示されます。 暗黙の認証は、R または Python スクリプトなどの外部プロセスから送信される要求で、SQL Server 接続文字列によって信頼関係接続が指定されるという点で、概念として Windows 認証に固有ではなくなりました。 これは、"*ループバック*" と呼ばれることもあります。

ユーザーの資格情報を使用したリソースへのアクセスまたは他の環境へのログインを防ぐために、AppContainer では ID と資格情報が管理されます。 AppContainer 環境ではユーザーとアプリケーションの ID の組み合わせを使用した識別子が作成されるため、資格情報はユーザーとアプリケーションのペアリングごとに一意であり、アプリケーションがユーザーの権限を借用することができません。 詳細については、「[AppContainer の分離](/windows/win32/secauthz/appcontainer-isolation)」を参照してください。

ループバック接続の詳細については、「[Python または R スクリプトからの SQL Server へのループバック接続](../connect/loopback-connection.md)」を参照してください。

### <a name="how-implied-authentication-works-for-external-script-sessions"></a>外部スクリプト セッションでの暗黙の認証のしくみ

次の図は、SQL Server コンポーネントと言語ランタイムの相互作用、および Windows で暗黙の認証が行われる方法を示しています。

![Windows での暗黙の認証](../security/media/implied-auth-windows.png)

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

## <a name="implied-authentication-loopback-requests"></a>暗黙の認証 (ループバック要求)

"*暗黙の認証*" では、接続要求の動作が示されます。これにおいては、データまたは操作のループバック要求で、低い特権 mssql_satellite のユーザーとして独自の名前空間で実行されている外部プロセスが信頼されたユーザー ID として SQL Server に提示されます。 これは、ループバックと呼ばれることもあります。

ループバック接続を実現するには、スタート パッド GUID フォルダーからのサテライト証明書を使用して、再び SQL Server に対する認証をサテライト プロセスから行います。 呼び出し元ユーザーの ID はこの証明書にマップされます。したがって、その証明書を使用して SQL Server に再び接続するサテライト プロセスを、該当する呼び出し元ユーザーに再びマップすることができます。

詳細については、「[Python または R スクリプトからの SQL Server へのループバック接続](../connect/loopback-connection.md)」を参照してください。

### <a name="how-implied-authentication-works-for-external-script-sessions"></a>外部スクリプト セッションでの暗黙の認証のしくみ

次の図は、SQL Server コンポーネントと言語ランタイムの相互作用、および Linux で暗黙の認証が行われる方法を示しています。

![Linux での暗黙の認証](../security/media/implied-auth-linux.png)

::: moniker-end

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>透過的なデータ暗号化はサポートされない

[透過的なデータ暗号化 (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) は、外部スクリプト ランタイムとの間で送受信されるデータに対してはサポートされません。 これは、外部プロセスが SQL Server プロセスの外部で実行されるためです。 このため、外部ランタイムによって使用されるデータは、データベース エンジンの暗号化機能によって保護されません。 この動作は、データベースからデータを読み取り、コピーを作成する、SQL Server コンピューターで実行される他のクライアントと同様です。

このため、TDE は、外部スクリプトで使用するデータ、ディスクに保存されるデータ、または保存される中間結果のいずれにも適用 **されません**。 ただし、Windows BitLocker 暗号化や、ファイルまたはフォルダー レベルで適用されるサード パーティ暗号化など、その他の種類の暗号化は引き続き適用されます。

[Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md) の場合、外部ランタイムは暗号化キーにアクセスできません。 そのため、スクリプトにデータを送信できません。

## <a name="next-steps"></a>次のステップ

この記事では、[機能拡張フレームワーク](../../machine-learning/concepts/extensibility-framework.md)に組み込まれたセキュリティ アーキテクチャのコンポーネントと相互作用モデルについて学習しました。 この記事で取り上げた主なポイントは、スタート パッド、SQLRUserGroup、およびワーカー アカウントの目的、外部スクリプトのプロセス分離、ユーザー ID をワーカーアカウントにマップする方法です。 

次の手順として、[アクセス許可付与](../../machine-learning/security/user-permission.md)の手順を確認してください。 Windows 認証を使用するサーバーの場合、追加の構成が必要になるタイミングを確認するために、[データベース ログインへの SQLRUserGroup の追加](../../machine-learning/security/create-a-login-for-sqlrusergroup.md)に関する記事も参照する必要があります。