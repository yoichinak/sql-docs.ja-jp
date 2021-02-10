---
title: SAP ASE への接続 (SybaseToSQL) |Microsoft Docs
description: アダプティブサーバーに接続して、SAP Adaptive Server Enterprise (ASE) データベースを SQL Server または Azure SQL Database に移行する方法について説明します。
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to Sybase
ms.assetid: a45a2330-9175-4c9e-af38-ef920e350614
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 7afb893d194b874da4cbb6482df4ba8a16e8c0a7
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100056867"
---
# <a name="connecting-to-sap-ase-sybasetosql"></a>SAP ASE への接続 (SybaseToSQL)

SAP Adaptive Server Enterprise (ASE) データベースをまたは SQL Azure に移行するに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、移行するデータベースが含まれている Adaptive Server に接続する必要があります。 接続すると、SSMA は、Adaptive Server 上のすべてのデータベースに関するメタデータを取得し、データベースメタデータを Sybase メタデータエクスプローラーペインに表示します。 SSMA は、データベースサーバーに関する情報を格納しますが、パスワードは保存しません。  
  
ASE への接続は、プロジェクトを閉じるまでアクティブのままになります。 プロジェクトを再度開いたときに、サーバーへのアクティブな接続が必要な場合は、ASE に再接続する必要があります。  
  
Adaptive Server に関するメタデータは自動的に更新されません。 代わりに、Sybase メタデータエクスプローラーでメタデータを更新する場合は、このトピックで後述する「Sybase ASE メタデータの更新」の説明に従って、メタデータを手動で更新する必要があります。  
  
## <a name="required-ase-permissions"></a>必要な ASE 権限

ASE への接続に使用するアカウントには、少なくとも master データベースへのパブリックアクセスと、移行先または SQL Azure のソースデータベースへの **パブリック** アクセスが必要です [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 さらに、移行するテーブルに対する権限を選択するには、次のシステムテーブルに対する SELECT 権限を持っている必要があります。  
  
- [source_db] .dbo.sysオブジェクト  
- [source_db] .dbo.sys列  
- [source_db] .dbo.sysユーザー  
- [source_db] .dbo.sysの種類  
- [source_db] .dbo.sys制約  
- [source_db] .dbo.sysコメント  
- [source_db] .dbo.sysインデックス  
- [source_db] .dbo.sys参照  
- master.dbo.sysデータベース  
  
## <a name="establishing-a-connection-to-ase"></a>ASE への接続の確立

Adaptive Server に接続すると、SSMA はデータベースサーバー上のデータベースメタデータを読み取り、このメタデータをプロジェクトファイルに追加します。 このメタデータは、SSMA がオブジェクトをまたは SQL Azure 構文に変換するとき、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] およびデータをまたは SQL Azure に移行するときに使用され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 このメタデータは、Sybase の [メタデータエクスプローラー] ペインで参照でき、個々のデータベースオブジェクトのプロパティを確認できます。  
  
> [!IMPORTANT]  
> データベースサーバーに接続する前に、データベースサーバーが実行されていて、接続を受け入れることができることを確認してください。  
  
**Sybase ASE に接続するには**
  
1. [ **ファイル** ] メニューの [ **Sybase に接続**] を選択します。  
  
   以前に Sybase に接続していた場合は、コマンド名が **sybase に再接続** されます。  
  
2. [ **プロバイダー** ] ボックスで、Sybase server に接続するコンピューター上のインストールされているプロバイダーを選択します。  
  
3. [ **モード** ] ボックスで、[ **標準モード** ] または **[詳細設定モード**] を選択します。  
  
   標準モードを使用して、サーバー名、ポート、ユーザー名、およびパスワードを指定します。 接続文字列を指定するには、詳細設定モードを使用します。 このモードは、通常、トラブルシューティングまたはテクニカルサポートの使用にのみ使用されます。  
  
4. [標準] **モード** を選択した場合は、次の値を指定します。  
  
    1. [ **サーバー名** ] ボックスで、データベースサーバーの名前または IP アドレスを入力または選択します。  
    2. データベースサーバーが既定のポート (5000) で接続を受け入れるように構成されていない場合は、[ **サーバーポート** ] ボックスに Sybase 接続に使用するポート番号を入力します。  
    3. [ **ユーザー名** ] ボックスに、必要なアクセス許可を持つ Sybase アカウントを入力します。  
    4. [ **パスワード** ] ボックスに、指定したユーザー名のパスワードを入力します。  
  
5. [ **詳細設定モード**] を選択した場合は、[ **接続文字列** ] ボックスに接続文字列を指定します。  
  
    さまざまな接続文字列の例を次に示します。  
  
    1. **Sybase OLE DB プロバイダーの接続文字列:**  
  
        Sybase ASE OLE DB 12.5 の場合、接続文字列の例は次のようになります。  
  
        `Server Name=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider=Sybase.ASEOLEDBProvider;`  
  
        Sybase ASE OLE DB 15 の場合、接続文字列の例は次のようになります。  
  
        `Server=sybserver;User ID=MyUserID;Password=MyP@$$word;Provider= ASEOLEDB;Port=5000;`  
  
    2. **Sybase ODBC プロバイダーの接続文字列:**  
  
       `Driver=Adaptive Server Enterprise;Server=sybserver;uid=MyUserID;pwd=MyP@$$word;Port=5000;`  
  
    3. **Sybase ADO.NET プロバイダーの接続文字列:**  
  
       `Server=sybserver;Port=5000;uid=MyUserID;pwd=MyP@$$word;`  
  
    詳細については、「 [Connect To Sybase &#40;SybaseToSQL&#41;](../../ssma/sybase/connect-to-sybase-sybasetosql.md)」を参照してください。  
  
## <a name="reconnecting-to-sybase-ase"></a>Sybase ASE への再接続

データベースサーバーへの接続は、プロジェクトを閉じるまでアクティブなままになります。 プロジェクトを再度開いたときに、アダプティブサーバーへのアクティブな接続が必要な場合は、再接続する必要があります。 メタデータを更新したり、データベースオブジェクトをまたは SQL Azure に読み込んだり、データを移行したりするまで、オフラインで作業することができ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
## <a name="refreshing-sybase-ase-metadata"></a>Sybase ASE メタデータの更新

ASE データベースに関するメタデータは自動的には更新されません。 Sybase メタデータエクスプローラーのメタデータは、最初にアダプティブサーバーに接続したとき、またはメタデータを手動で更新したときのメタデータのスナップショットです。 1つのデータベース、単一のデータベーススキーマ、またはすべてのデータベースのメタデータを手動で更新できます。  
  
**メタデータを更新するには**
  
1. Adaptive Server に接続していることを確認します。  
  
2. Sybase Metadata Explorer で、更新するデータベースまたはデータベーススキーマの横にあるチェックボックスをオンにします。  
  
3. [データベース] または個々のデータベースまたはデータベーススキーマを右クリックし、[ **データベースから更新**] を選択します。  
  
4. 現在のオブジェクトを確認するように求められたら、[ **はい**] をクリックします。  
  
## <a name="next-step"></a>次の手順  
  
- 移行プロセスの次の手順は、のインスタンスに接続して[SQL Server](connecting-to-sql-server-sybasetosql.md)のインスタンスに接続することです  /  [SQL Azure](connecting-to-azure-sql-db-sybasetosql.md)  
  
## <a name="see-also"></a>参照

[Sybase ASE データベースを SQL Server Azure SQL Database &#40;SybaseToSQL&#41;に移行する ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
