---
title: SQL Server への接続 (SQL server への接続) |Microsoft Docs
description: SQL Database のターゲットインスタンスに接続して Access データベースを移行する方法について説明します。 SSMA は SQL Database のデータベースに関するメタデータを取得します。
ms.prod: sql
ms.custom: ''
ms.date: 11/16/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- authentication
- instance of SQL Server
- metadata, refreshing
- ports
- refreshing metadata
- spaces in database names
- special characters
- SQL Server
- SQL Server, connecting
- SQL Server, connecting to
- SQL Server, reconnecting
ms.assetid: f84cf007-ddf1-4396-a07c-3e0729abc769
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1bd54d3fdf90447dbbf8b35a96c6b454ca6c4e56
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869566"
---
# <a name="connecting-to-sql-server-accesstosql"></a>SQL Server への接続 (SQL server)

Access データベースをに移行するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の対象インスタンスに接続する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 接続すると、SSMA はのインスタンス内のデータベースに関するメタデータ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を取得し、 **SQL Server メタデータエクスプローラー** にデータベースのメタデータを表示します。 SSMA は、接続先ののインスタンスに関する情報を格納し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ますが、パスワードは保存しません。

への接続 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、プロジェクトを閉じるまでアクティブなままになります。 プロジェクトを再度開いたときに、サーバーへのアクティブな接続が必要な場合は、に再接続する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 データベースオブジェクトをに読み込んでデータを移行するまで、オフラインで作業することができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

のインスタンスに関するメタデータ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、自動的には同期されません。 代わりに、メタデータエクスプローラー SQL Server メタデータを更新するには、メタデータを手動で更新する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、このトピックで後述する「SQL Server メタデータの同期」を参照してください。

## <a name="required-sql-server-permissions"></a>必要な SQL Server アクセス許可

への接続に使用するアカウントには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントが実行するアクションに応じて、異なるアクセス許可が必要です。

- Access オブジェクトを構文に変換し [!INCLUDE[tsql](../../includes/tsql-md.md)] たり、からメタデータを更新したり、変換され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] た構文をスクリプトに保存したりするには、アカウントにのインスタンスにログオンする権限が必要 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] です。

- データベースオブジェクトをに読み込むには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントが **db_ddladmin** データベースロールのメンバーである必要があります。

- にデータを移行するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アカウントが **db_owner** データベースロールのメンバーである必要があります。

## <a name="establishing-a-sql-server-connection"></a>SQL Server 接続の確立

Access データベースオブジェクトを構文に変換する前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] access データベースを移行するインスタンスへの接続を確立する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

接続プロパティを定義するときに、オブジェクトとデータを移行するデータベースも指定します。 このマッピングは、に接続した後、Access データベースレベルでカスタマイズでき [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 詳細については、「 [ソースデータベースとターゲットデータベースのマッピング](mapping-source-and-target-databases-accesstosql.md)」を参照してください。

> [!IMPORTANT]
> に接続する前に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、のインスタンスが実行されていて、接続を受け入れることができることを確認し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に接続するには次の操作を行います。

1. [ **ファイル** ] メニューの [ **SQL Server に接続**] を選択します。
   以前にに接続していた場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、コマンド名は **SQL Server に再接続** されます。

2. [ **サーバー名** ] ボックスに、のインスタンスの名前を入力または選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。
   - ローカルコンピューター上の既定のインスタンスに接続している場合 `localhost` は、またはドット () を入力でき `.` ます。
   - 別のコンピューター上の既定のインスタンスに接続している場合は、コンピューターの名前を入力します。
   - 名前付きインスタンスに接続する場合は、コンピューター名、円記号、およびインスタンス名を入力します。 (例: `MyServer\MyInstance`)。
   - のアクティブなユーザーインスタンスに接続するに [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] は、名前付きパイププロトコルを使用して接続し、などのパイプ名を指定し `\\.\pipe\sql\query` ます。 詳細については、[!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] のドキュメントを参照してください。

3. のインスタンス [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] が既定以外のポートで接続を受け入れるように構成されている場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [ **サーバーポート** ] ボックスに接続に使用するポート番号を入力します。 の既定のインスタンスの場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、既定のポート番号は1433です。 名前付きインスタンスの場合、SSMA は Browser サービスからポート番号の取得を試み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

4. [ **データベース** ] ボックスに、オブジェクトおよびデータ移行の対象となるデータベースの名前を入力します。
   このオプションは、に再接続するときには使用できません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。
   ターゲットデータベース名にスペースや特殊文字を含めることはできません。 たとえば、Access データベースを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] という名前のデータベースに移行でき `abc` ます。 ただし、Access データベースをという名前のデータベースに移行することはできません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `a b-c` 。
   このマッピングは、接続後にデータベースごとにカスタマイズできます。 詳細については、「[ソースデータベースとターゲットデータベースのマッピング](mapping-source-and-target-databases-accesstosql.md)」を参照してください。

5. [ **認証** ] ドロップダウンメニューで、接続に使用する認証の種類を選択します。 現在の Windows アカウントを使用するには、[ **Windows 認証**] を選択します。 ログインを使用するには [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、[ **SQL Server 認証**] を選択し、ユーザー名とパスワードを入力します。

6. セキュリティで保護された接続の場合は、2つのコントロールが追加され、[ **接続の暗号化** ] チェックボックスと [ **trustservercertificate** ] チェックボックスが **暗号化接続** チェックボックスがオンになっている場合にのみ、 **trustservercertificate** チェックボックスが表示されます。 [ **暗号化接続** ] がオンになっている場合 (true)、 **trustservercertificate** がオフになっている場合 (false)、は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSL 証明書を検証します。 サーバー証明書の検証は、SSL ハンドシェイクの一部であり、接続先のサーバーが適切なサーバーであることを保証します。 これを実現するには、証明書をクライアント側とサーバー側の両方にインストールする必要があります。

7. **[Connect]** をクリックします。

> [!IMPORTANT]
> 新しいバージョンのに接続することもできますが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、移行プロジェクトの作成時に選択したバージョンとは異なり、データベースオブジェクトの変換は、接続先のバージョンではなく、プロジェクトのターゲットバージョンによって決まり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

## <a name="synchronizing-sql-server-metadata"></a>SQL Server メタデータの同期

接続後にスキーマが変更された場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] メタデータをサーバーと同期させることができます。

メタデータを同期するには、 **メタデータエクスプローラー SQL Server**、[ **データベース**] を右クリックし、[ **データベースとの同期**] を選択し SQL Server ます。

## <a name="reconnecting-to-sql-server"></a>SQL Server に再接続しています

への接続 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、プロジェクトを閉じるまでアクティブなままになります。 プロジェクトを再度開いたときに、サーバーへのアクティブな接続が必要な場合は、に再接続する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 データベースオブジェクトをに読み込んでデータを移行するまで、オフラインで作業することができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。

に再接続する手順 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、接続を確立する手順と同じです。

## <a name="next-steps"></a>次の手順

ソースデータベースとターゲットデータベース間のマッピングをカスタマイズする場合は、「 [ソースデータベースとターゲットデータベースのマッピング](mapping-source-and-target-databases-accesstosql.md) 」を参照してください。それ以外の場合は、次の手順では、データベースオブジェクト [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の [変換](converting-access-database-objects-accesstosql.md)を使用してデータベースオブジェクトを構文に変換します。

## <a name="see-also"></a>参照

[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)
