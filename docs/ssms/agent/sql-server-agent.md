---
description: SQL Server エージェント
title: SQL Server エージェント
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, about SQL Server Agent
- automatic administration steps
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/03/2021
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 751a627530b7d1017bfd8f0f89aa626ea84bc35c
ms.sourcegitcommit: ca81fc9e45fccb26934580f6d299feb0b8ec44b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102186540"
---
# <a name="sql-server-agent"></a>SQL Server エージェント

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]
> 現在、[Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance) によって、すべてではありませんが、ほとんどの SQL Server エージェントの機能がサポートされています。 詳細については、[Azure SQL Managed Instance と SQL Server の T-SQL の相違点](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)に関するページを参照してください。

SQL Server エージェントは、SQL Server で、"*ジョブ*" と呼ばれる管理タスクをスケジュールに従って実行する Microsoft Windows サービスです。

## <a name="benefits-of-sql-server-agent"></a><a name="Benefits"></a>SQL Server エージェントの利点

SQL Server エージェントでは、ジョブ情報を格納するのに SQL Server が使用されます。 ジョブには 1 つ以上のジョブ ステップが含まれます。 各ジョブ ステップには、データベースをバックアップするなど、独自のタスクがあります。

SQL Server エージェントでは、スケジュールに従って、特定のイベントに応答して、または必要に応じてジョブを実行できます。 たとえば、毎平日の業務終了後に会社のすべてのサーバーをバックアップする必要がある場合は、そのタスクを自動化できます。 月曜から金曜までの 22:00 以降にバックアップを実行するスケジュールを設定します。 バックアップに問題が発生した場合は、SQL Server エージェントによってイベントが記録され、通知を受け取ることができます。

> [!NOTE]
> SQL Server のインストール時に、SQL Server エージェント サービスを自動起動することをユーザーが明示的に選択しない限り、このサービスは既定で無効になります。

## <a name="sql-server-agent-components"></a><a name="Components"></a>sysadmin

SQL Server エージェントでは、次のコンポーネントを使用して、実行するタスク、タスクを実行する時期、タスクの成功/失敗の報告方法を定義します。

### <a name="jobs"></a>ジョブ

"*ジョブ*" とは、SQL Server エージェントで実行される指定した一連のアクションのことです。 ジョブを使用し、1 回または複数回実行してその成否を監視できる管理タスクを定義します。 ジョブは、1 つのローカル サーバーで実行することも、複数のリモート サーバーで実行することもできます。

> [!IMPORTANT]
> SQL Server フェールオーバー クラスター インスタンスでフェールオーバー イベントが発生したときに実行されていた SQL Server エージェント ジョブは、別のフェールオーバー クラスター ノードにフェールオーバーしても再開されません。 Hyper-V ノードの一時停止時に実行されていた SQL Server エージェント ジョブは、一時停止によって別のノードにフェールオーバーしても再開されません。 ジョブの開始後、フェールオーバー イベントが原因でそのジョブが完了しなかった場合は、開始したことがログに記録されますが、完了か失敗かを示すログ エントリは追加されません。 このようなシナリオでの SQL Server エージェント ジョブは終了していないように見えます。

ジョブは、次のような方法で実行できます。

- 1 つ以上のスケジュールに従って実行する。

- 1 つ以上の警告に応答して実行する。

- sp_start_job ストアド プロシージャの実行によって実行する。

ジョブ内の各処理を *ジョブ ステップ* といいます。 たとえば、ジョブ ステップは、Transact\-SQL ステートメントの実行、SSIS パッケージの実行、Analysis Services サーバーへのコマンドの発行などで構成されます。 ジョブ ステップはジョブの一部として管理されます。

各ジョブ ステップは、特定のセキュリティ コンテキストで実行されます。 Transact\-SQL を使用するジョブ ステップでは、EXECUTE AS ステートメントを使用して、ジョブ ステップにセキュリティ コンテキストを設定します。 その他のジョブ ステップでは、プロキシ アカウントを使用して、ジョブ ステップにセキュリティ コンテキストを設定します。

### <a name="schedules"></a>スケジュール

*スケジュール* では、ジョブを実行する時期を指定します。 同じスケジュールで複数のジョブを実行できるほか、同じジョブに複数のスケジュールを適用することもできます。 ジョブが実行されるタイミングに関して、次の条件をスケジュールで定義できます。

- SQL Server エージェントが開始されるたび。

- コンピューターの CPU 使用率がアイドルとして定義したレベルになるたび。

- 指定した日時に 1 回だけジョブを実行する。

- 定期的なスケジュール。

詳細については、「 [スケジュールの作成とジョブへのアタッチ](../../ssms/agent/create-and-attach-schedules-to-jobs.md)」を参照してください。

### <a name="alerts"></a>警告

*警告* とは、特定のイベントに対する自動応答のことです。 たとえば、ジョブが開始されたり、システム リソースが特定のしきい値に達したときなどがイベントと見なされます。 警告では、それが発生する条件を定義します。

警告は、次のいずれかの条件に対して生成できます。

- SQL Server のイベント

- SQL Server のパフォーマンス条件

- SQL Server エージェントが実行されているコンピューターで発生した Microsoft Windows Management Instrumentation (WMI) イベント

警告では、次のアクションを実行できます。

- 1 人または複数のオペレーターへの通知

- ジョブの実行

詳細については、「 [警告](../../ssms/agent/alerts.md)」を参照してください。  

### <a name="operators"></a>オペレーター

"*オペレーター*" は、SQL Server の 1 つまたは複数のインスタンスについて、そのメンテナンスの担当者の連絡先情報を定義します。 一部の企業では、オペレーターの責任は 1 人に割り当てられます。 サーバーを複数台使用している企業では、多数の担当者がオペレーターの責任を共有します。 オペレーターは、セキュリティ情報を持たず、セキュリティ プリンシパルも定義しません。  

SQL Server では、次の方法でオペレーターに警告を通知することができます。

- 電子メール

- 電子メール経由のポケットベル

- **net send**

> [!NOTE]
> **net send** を使用して通知を送信するには、SQL Server エージェントが置かれているコンピューターで Windows Messenger サービスを開始する必要があります。

> [!IMPORTANT]
> SQL Server の今後のバージョンでは、SQL Server エージェントからポケットベルおよび **net send** オプションが削除されます。 新しい開発作業では、これらの機能の使用を避け、現在これらの機能を使用しているアプリケーションは修正するようにしてください。  

電子メールまたはポケットベルを使用してオペレーターに通知を送信するには、データベース メールを使用するように SQL Server エージェントを構成する必要があります。 詳細については、「[データベース メール](../../relational-databases/database-mail/database-mail.md)」を参照してください。

オペレーターは、個人のグループを表す別名として定義できます。 この方法では、その別名のすべてのメンバーが同時に確認されるわけではありません。 詳細については、「[演算子](../../ssms/agent/operators.md)」を参照してください。

## <a name="security-for-sql-server-agent-administration"></a><a name="Security"></a>SQL Server エージェントのセキュリティ管理

SQL Server エージェントでは **msdb** データベースの固定データベース ロールである **SQLAgentUserRole**、**SQLAgentReaderRole**、**SQLAgentOperatorRole** を使用して、**sysadmin** 固定サーバー ロールのメンバーではないユーザーの SQL Server エージェントへのアクセスを制御します。 これらの固定データベース ロールに加え、サブシステムとプロキシを使用することで、タスクの実行に最低限必要な権限で各ジョブ ステップを実行できるようになります。  

### <a name="roles"></a>役割

**msdb** の固定データベース ロールである **SQLAgentUserRole**、**SQLAgentReaderRole**、**SQLAgentOperatorRole** のメンバーと、**sysadmin** 固定サーバー ロールのメンバーは、SQL Server エージェントにアクセスできます。 これらのどのロールのメンバーでもないユーザーは、SQL Server エージェントを使用できません。 SQL Server エージェントによって使用されるロールの詳細については、「[SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)」を参照してください。

### <a name="subsystems"></a>サブシステム

サブシステムは事前に定義されたオブジェクトで、任意のジョブ ステップで使用できる機能を表します。 各プロキシは 1 つ以上のサブシステムにアクセスできます。 サブシステムはプロキシで使用できる機能へのアクセスを制限することによりセキュリティを提供します。 Transact\-SQL ジョブ ステップ以外の各ジョブ ステップは、プロキシのコンテキストで実行されます。 Transact\-SQL ジョブ ステップでは、EXECUTE AS コマンドを使用してセキュリティ コンテキストをジョブの所有者に設定します。  

SQL Server には、次の表に示すサブシステムが定義されています。  

|サブシステム名|説明|
|--------------|-----------|
|Microsoft ActiveX スクリプト|ActiveX スクリプティング ジョブ ステップを実行します。<br /><br />**警告** ActiveX スクリプティング サブシステムは、Microsoft SQL Server の将来のバージョンで SQL Server エージェントから削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。|  
|オペレーティング システム (**CmdExec**)|実行可能なプログラムを実行します。|
|PowerShell|PowerShell スクリプティング ジョブ ステップを実行します。|
|レプリケーション ディストリビューター|レプリケーション ディストリビューション エージェントをアクティブにするジョブ ステップを実行します。|
|レプリケーション マージ|レプリケーション マージ エージェントをアクティブにするジョブ ステップを実行します。|
|レプリケーション キュー リーダー|レプリケーション キュー リーダー エージェントをアクティブにするジョブ ステップを実行します。|
|レプリケーション スナップショット|レプリケーション スナップショット エージェントをアクティブにするジョブ ステップを実行します。|
|レプリケーション トランザクション ログ リーダー|レプリケーション ログ リーダー エージェントをアクティブにするジョブ ステップを実行します。|
|Analysis Services コマンド|Analysis Services コマンドを実行します。|
|Analysis Services クエリ|Analysis Services クエリを実行します。|
|SSIS パッケージ実行|SSIS パッケージを実行します。|

> [!NOTE]
> Transact\-SQL ジョブ ステップではプロキシが使用されないため、Transact\-SQL ジョブ ステップ用の SQL Server エージェント サブシステムはありません。  

ジョブ ステップでタスクを実行する権限がプロキシのセキュリティ プリンシパルに通常割り当てられている場合でも、SQL Server エージェントではサブシステム制約が強制的に適用されます。 たとえば、sysadmin 固定サーバー ロールのメンバーであるユーザーのプロキシから SSIS サブシステムにアクセスできなければ、そのユーザーが SSIS パッケージを実行できる場合でも、そのプロキシで SSIS ジョブ ステップを実行することはできません。  

### <a name="proxies"></a>プロキシ

SQL Server エージェントでは、プロキシを使用してセキュリティ コンテキストを管理します。 プロキシは、複数のジョブ ステップで使用できます。 固定サーバー ロール **sysadmin** のメンバーは、プロキシを作成できます。  

各プロキシには対応するセキュリティ資格情報が 1 つあります。 各プロキシは、一連のサブシステムや一連のログインに関連付けることができます。 プロキシは、そのプロキシに関連付けられているサブシステムを使用するジョブ ステップにのみ使用できます。 特定のプロキシを使用するジョブ ステップを作成するには、ジョブの所有者がそのプロキシに関連付けられているログインを使用しているか、プロキシへ制限なしにアクセスできるロールのメンバーである必要があります。 固定サーバー ロール **sysadmin** のメンバーは、プロキシに制限なしにアクセスできます。 **SQLAgentUserRole**、 **SQLAgentReaderRole**、または **SQLAgentOperatorRole** のメンバーは、特定のアクセスが許可されているプロキシしか使用できません。 これらの SQL Server エージェントの固定データベース ロールのメンバーであるユーザーが特定のプロキシを使用するジョブ ステップを作成するには、ユーザーごとにこれらの特定のプロキシへのアクセスが許可されている必要があります。  

## <a name="related-tasks"></a>Related Tasks

SQL Server 管理を自動化するように SQL Server エージェントを構成するには、次の手順に従ってください。

1. 定期的に発生する管理タスクまたはサーバー イベントを確定し、それらをプログラムによって管理できるかどうかも確定します。 手順の順序が予測可能で、特定の時刻または特定のイベントに対する応答として行われるタスクは、自動化に適しています。

2. SQL Server Management Studio、Transact\-SQL スクリプト、または SQL Server 管理オブジェクト (SMO) を使用して、ジョブ、スケジュール、警告、およびオペレーターから構成されるセットを定義します。 詳細については、「 [ジョブの作成](../../ssms/agent/create-jobs.md)」を参照してください。  

3. 定義した SQL Server エージェント ジョブを実行します。

> [!NOTE]
> SQL Server の既定のインスタンスの場合、SQL Server サービスの名前は SQLSERVERAGENT です。 名前付きインスタンスの場合、SQL Server エージェント サービスの名前は SQLAgent$*instancename* です。

複数の SQL Server インスタンスを実行している場合、すべてのインスタンスに共通なタスクをマルチサーバー管理を使用して自動化できます。 詳細については、「 [エンタープライズ全体の管理の自動化](../../ssms/agent/automated-administration-across-an-enterprise.md)」を参照してください。

次のタスクを使用して、SQL Server エージェントの使用を開始します。

|説明|トピック|
|-----------|-----|
|SQL Server エージェントを構成する方法について説明します。|[SQL Server エージェントの構成](../../ssms/agent/configure-sql-server-agent.md)|  
|SQL Server エージェント サービスを開始、停止、および一時停止する方法について説明します。|[SQL Server エージェント サービスの開始、停止、または一時停止](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)|
|SQL Server エージェント サービスのアカウントを指定する際の考慮事項について説明します。|[SQL Server エージェント サービスのアカウントの選択](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md)|
|SQL Server エージェントのエラー ログを使用する方法について説明します。|[SQL Server エージェント エラー ログ](../../ssms/agent/sql-server-agent-error-log.md)|  
|パフォーマンス オブジェクトを使用する方法について説明します。|[パフォーマンス オブジェクトの使用](../../ssms/agent/use-performance-objects.md)|
|メンテナンス プラン ウィザードについて説明します。これは、SQL Server のインスタンスを自動管理するためのジョブ、警告、およびオペレーターを作成するために使用するユーティリティです。|[メンテナンス プラン ウィザードの使用](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)|
|SQL Server エージェントを使用して管理タスクを自動化する方法について説明します。|[管理タスクの自動化 &#40;SQL Server エージェント&#41;](../../ssms/agent/automated-administration-tasks-sql-server-agent.md)|

## <a name="nosqlps"></a>NOSQLPS

[!INCLUDE [sql-server-powershell-no-sqlps](../../includes/sql-server-powershell-no-sqlps.md)]

## <a name="see-also"></a>参照

- [セキュリティ構成](../../relational-databases/security/surface-area-configuration.md)
- [PowerShell を使用した SQL Server エージェント](../../powershell/sql-server-powershell.md#sql-server-agent)
