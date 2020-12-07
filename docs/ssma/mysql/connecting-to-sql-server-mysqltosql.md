---
title: SQL Server に接続しています (MySQLToSQL) |Microsoft Docs
description: SQL Server のターゲットインスタンスに接続して MySQL データベースを移行する方法について説明します。 SSMA は SQL Server のデータベースに関するメタデータを取得します。
ms.prod: sql
ms.custom: ''
ms.date: 11/16/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- connecting to SQL Server 2008, SQL Server permission
- connecting to SQL Server 2008, synchronization
ms.assetid: 08233267-693e-46e6-9ca3-3a3dfd3d2be7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: c004f4ced6bad2b6db45f4be56e442a10965a514
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870238"
---
# <a name="connecting-to-sql-server-mysqltosql"></a>SQL Server への接続 (MySQLToSQL)

MySQL データベースをに移行するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のターゲットインスタンスに接続する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 接続すると、SSMA はインスタンス内のすべてのデータベースに関するメタデータ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を取得し、 **SQL Server メタデータエクスプローラー** にデータベースのメタデータを表示します。 SSMA は、接続しているのインスタンスの情報を格納し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ますが、パスワードは保存しません。

への接続 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、プロジェクトを閉じるまでアクティブなままになります。 プロジェクトを再度開いたときに、サーバーへのアクティブな接続が必要な場合は、に再接続する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 データベースオブジェクトをに読み込んでデータを移行するまで、オフラインで作業することができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

のインスタンスに関するメタデータ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、自動的には同期されません。 代わりに、メタデータ **エクスプローラー SQL Server** メタデータを更新するには、メタデータを手動で更新する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、このトピックで後述する「SQL Server メタデータの同期」を参照してください。

## <a name="required-sql-server-permissions"></a>必要な SQL Server アクセス許可

への接続に使用するアカウントには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントが実行するアクションに応じて、異なるアクセス許可が必要です。

- MySQL オブジェクトを構文に変換し [!INCLUDE[tsql](../../includes/tsql-md.md)] たり、からメタデータを更新し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] たり、変換された構文をスクリプトに保存したりするには、アカウントがのインスタンスにログオンする権限を持っている必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

- データベースオブジェクトをに読み込むには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントが **db_ddladmin** データベースロールのメンバーである必要があります。

- にデータを移行するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、アカウントが次のようになっている必要があります。
  - クライアント側のデータ移行エンジンを使用している場合は、 **db_owner** データベースロールのメンバー。
  - サーバー側のデータ移行エンジンを使用している場合は、 **sysadmin** サーバーロールのメンバー。 これは、 `CmdExec` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ssma 一括コピーツールを実行するためにデータ移行中にエージェントジョブステップを作成するために必要です。
    > [!NOTE]
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントプロキシアカウントは、サーバー側のデータ移行ではサポートされていません。

## <a name="establishing-a-sql-server-connection"></a>SQL Server 接続の確立

MySQL データベースオブジェクトを構文に変換する前に、MySQL データベースの移行先となる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスへの接続を確立する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

接続プロパティを定義するときに、オブジェクトとデータを移行するデータベースも指定します。 このマッピングは、に接続した後に MySQL スキーマレベルでカスタマイズでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「 [MySQL データベースを SQL Server スキーマ &#40;MySQLToSQL&#41;にマップする ](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)」を参照してください。

> [!IMPORTANT]
> に接続する前に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、のインスタンス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が実行されていて、接続を受け入れることができることを確認してください。

SQL Server に接続するには:

1. [ **ファイル** ] メニューの [ **SQL Server に接続** ] を選択します (このオプションは、プロジェクトの作成後に有効になります)。
   に既に接続している場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、コマンド名が **SQL Server に再接続** されます。

2. [接続] ダイアログボックスで、のインスタンスの名前を入力または選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。
   - ローカルコンピューター上の既定のインスタンスに接続している場合 `localhost` は、またはドット () を入力でき `.` ます。
   - 別のコンピューター上の既定のインスタンスに接続している場合は、コンピューターの名前を入力します。
   - 別のコンピューター上の名前付きインスタンスに接続する場合は、コンピューター名とその後に円記号を入力し、インスタンス名 (など) を入力し `MyServer\MyInstance` ます。

3. のインスタンス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が既定以外のポートで接続を受け入れるように構成されている場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [ **サーバーポート** ] ボックスに接続に使用するポート番号を入力します。 の既定のインスタンスの場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、既定のポート番号は1433です。 名前付きインスタンスの場合、SSMA は Browser サービスからポート番号の取得を試み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

4. [ **認証** ] ボックスで、接続に使用する認証の種類を選択します。 現在の Windows アカウントを使用するには、[ **Windows 認証**] を選択します。 ログインを使用するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、[ **SQL Server 認証**] を選択し、ログイン名とパスワードを入力します。

5. セキュリティで保護された接続では、[ **暗号化接続** ] チェックボックスと [ **trustservercertificate** ] チェックボックスの2つのコントロールが追加されます。 [ **暗号化接続** ] をオンにした場合にのみ、[ **trustservercertificate** ] チェックボックスが表示されます。 [ **暗号化接続** ] がオンになっている場合 (true)、 **trustservercertificate** がオフになっている場合 (false)、SSL 証明書が検証され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 サーバー証明書の検証は、SSL ハンドシェイクの一部であり、接続先のサーバーが適切なサーバーであることを保証します。 これを実現するには、証明書をクライアント側とサーバー側の両方にインストールする必要があります。

6. **[Connect]** をクリックします。

> [!IMPORTANT]
> 新しいバージョンのに接続することもできますが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、移行プロジェクトの作成時に選択したバージョンとは異なり、データベースオブジェクトの変換は、接続先のバージョンではなく、プロジェクトのターゲットバージョンによって決まり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

## <a name="synchronizing-sql-server-metadata"></a>SQL Server メタデータの同期

データベースに関するメタデータ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は自動的に更新されません。 **SQL Server メタデータエクスプローラー** のメタデータは、最初に接続したとき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、またはメタデータを手動で更新したときにメタデータのスナップショットになります。 すべてのデータベース、または任意の1つのデータベースまたはデータベースオブジェクトのメタデータを手動で更新できます。 メタデータを同期するには:

1. に接続されていることを確認し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

2. **SQL Server メタデータエクスプローラー** で、更新するデータベースまたはデータベーススキーマの横にあるチェックボックスをオンにします。
   たとえば、すべてのデータベースのメタデータを更新するには、[ **データベース**] の横にあるチェックボックスをオンにします。

3. [データベース]、または個々のデータベースまたはデータベーススキーマを **右クリックし**、[ **データベースとの同期**] を選択します。

## <a name="next-step"></a>次の手順

移行の次のステップは、プロジェクトのニーズによって異なります。

- MySQL スキーマと SQL Server データベースおよびスキーマ間のマッピングをカスタマイズするには、「 [Mysql データベースの SQL Server スキーマ &#40;MySQLToSQL&#41;へのマッピング ](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)」を参照してください。
- プロジェクトの構成オプションをカスタマイズするには、「 [プロジェクトオプションの設定 &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md)」を参照してください。
- ソースとターゲットのデータ型のマッピングをカスタマイズするには、「 [MySQL と SQL Server のデータ型のマッピング &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)」を参照してください。
- これらのタスクを実行する必要がない場合は、MySQL データベースオブジェクト定義をオブジェクト定義に変換でき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「 [MySQL データベース &#40;MySQLToSQL&#41;の変換 ](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)」を参照してください。

## <a name="see-also"></a>参照

[MySQL データベースを SQL Server Azure SQL Database &#40;MySQLToSql&#41;に移行する ](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)
