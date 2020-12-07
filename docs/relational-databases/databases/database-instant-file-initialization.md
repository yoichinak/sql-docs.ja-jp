---
title: データベースのファイルの瞬時初期化
description: ファイルの瞬時初期化と、それを SQL Server データベースで有効にする方法について説明します。
ms.custom: contperfq4
ms.date: 07/24/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- initializing files [SQL Server]
- instant file initialization [SQL Server]
- fast file initialization [SQL Server]
- file initialization [SQL Server]
- IFI [SQL Server]
- database instant file initialization [SQL Server]
ms.assetid: 1ad468f5-4f75-480b-aac6-0b01b048bd67
author: stevestein
ms.author: sstein
ms.openlocfilehash: ed2781c82b2479087012ff6c761a0497b2d56444
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192183"
---
# <a name="database-instant-file-initialization"></a>データベースのファイルの瞬時初期化
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
この記事では、ファイルの瞬時初期化と、それを有効にして SQL Server データベース ファイルの拡張を高速化する方法について説明します。  

デフォルトでは、データおよびログ ファイルの初期化は、ディスクに以前削除したファイルのデータが残っている場合にそれを上書きするために行います。 次の操作を実行すると、データとログ ファイルは、まずファイルのゼロイング (ゼロを書き込む処理) で初期化されます。  
  
- データベースを作成します。  
- 既存のデータベースへのデータ ファイルまたはログ ファイルの追加。  
- 既存のファイルのサイズを大きくする (自動拡張操作を含む)。  
- データベースまたはファイル グループの復元。  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、ファイルの瞬時初期化 (IFI) によって、前述のファイル操作を高速に実行できます。これは、使用されているディスク領域をゼロで埋めることなく再利用するためです。 代わりに、新しいデータがファイルに書き込まれるときに、ディスクの内容が上書きされます。 ログ ファイルを瞬時に初期化することはできません。


## <a name="enable-instant-file-initialization"></a>ファイルの瞬時初期化の有効化

ファイルの瞬時初期化は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]サービス開始アカウントに *SE_MANAGE_VOLUME_NAME* が付与されている場合にのみ使用できます。 Windows Administrator グループのメンバーにはこの権限があり、他のユーザーを **ボリュームの保守タスクを実行** セキュリティ ポリシーに追加することにより、これらのユーザーにこの権限を許可することができます。  
> [!IMPORTANT]
> [Transparent Data Encryption (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) など、ファイルの瞬時初期化を使用できない機能の使用状況もあります。  

> [!NOTE]
> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降、インストール時、セットアップ中にサービス アカウントにこのアクセス許可を付与できます。 <br><br>[コマンド プロンプト インストール](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)を利用する場合、/SQLSVCINSTANTFILEINIT 引数を追加するか、[インストール ウィザード](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)で *[SQL Server データベース エンジン サービスにボリューム メンテナンス タスクを実行する特権を付与する]* ボックスを選択します。
  
アカウントに `Perform volume maintenance tasks` 権限を許可する方法。  
  
1.  データ ファイルを作成するコンピューター上で、**ローカル セキュリティ ポリシー** アプリケーション (`secpol.msc`) を開きます。  
  
1.  左側のペインで **[ローカル ポリシー]** を展開し、 **[ユーザー権利の割り当て]** をクリックします。  
  
1.  右側のペインで、 **[ボリュームの保守タスクを実行]** をダブルクリックします。  
  
1.  **[ユーザーまたはグループの追加]** をクリックして、SQL Server サービスを実行するアカウントを追加します。  
  
1.  **[適用]** をクリックし、 **[ローカル セキュリティ ポリシー]** ダイアログ ボックスをすべて閉じます。  

1. SQL Server サービスを再起動します。

1. 起動時に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エラー ログを確認します。
   
  
    **適用対象:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP4 以降、[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 および [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 以降)。
    1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス開始アカウントに *SE_MANAGE_VOLUME_NAME* が与えられる場合、次のような情報メッセージが記録されます。

        `Database Instant File Initialization: enabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`

    1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス開始アカウントに *SE_MANAGE_VOLUME_NAME* が与えられて**いない**場合、次のような情報メッセージが記録されます。

        `Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.`
    > [!NOTE]
    > [sys.dm_server_services](../../relational-databases/system-dynamic-management-views/sys-dm-server-services-transact-sql.md) DMV の *instant_file_initialization_enabled* 列を利用し、ファイルの瞬時初期化が有効になっているかどうかを判断することもできます。

## <a name="security-considerations"></a>セキュリティに関する考慮事項

メリットがセキュリティ リスクを上回る可能性があるため、ファイルの瞬時初期化を有効にすることを推奨します。

ファイルの瞬時初期化を使用する場合、削除されたディスクの内容は、新しいデータがファイルに書き込まれるときにのみ上書きされます。 そのため、他のデータがデータ ファイルのその領域に書き込まれるまで、許可されていないプリンシパルが削除された内容にアクセスする可能性があります。

データベース ファイルが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスにアタッチされている間は、ファイルに対する随意アクセス制御リスト (DACL) により、このような情報漏えいのリスクは軽減されます。 この DACL により、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントとローカル管理者のみにファイル アクセスが許可されます。 ただし、ファイルがデタッチされると、*SE_MANAGE_VOLUME_NAME* が付与されていないユーザーまたはサービスからアクセスされる可能性があります。

次の場合にも同じようなことを考慮する必要があります。

* *データベースがバックアップされています。* バックアップ ファイルが適切な DACL で保護されていない場合、許可されていないユーザーやサービスが削除された内容を利用できるようになることがあります。  

* *IFI を使用してファイルが拡張されています。* SQL Server 管理者が未加工のページ コンテンツにアクセスして、以前削除されたコンテンツを表示する可能性があります。

* *データベース ファイルが記憶域ネットワークにホストされています。* 記憶域ネットワークで常に新しいページが事前に初期化されているものとして示される可能性もあり、オペレーティング システムでページが再初期化されると不要なオーバーヘッドが発生する可能性があります。

削除された内容が公開される可能性が懸念される場合は、次のいずれか、または両方の対策を行う必要があります。  
  
- デタッチされたすべてのデータ ファイルおよびバックアップ ファイルに、常に限定的な DACL が設定されるようにする。  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスでデータ ファイルの瞬時初期化を無効にします。    これを行うには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス開始アカウントから *SE_MANAGE_VOLUME_NAME* を取り消します。
    
    > [!NOTE]
    > 無効化により、データ ファイルの割り当て時間が増加します。これは、ユーザー権限が禁止された後で作成またはサイズ増加されたファイルのみに影響します。
  
### <a name="se_manage_volume_name-user-right"></a>SE_MANAGE_VOLUME_NAME ユーザー権限

*SE_MANAGE_VOLUME_NAME* ユーザー特権は、**Windows 管理ツール**、**ローカル セキュリティ ポリシー** アプレットで割り当てることができます。 **[ローカル ポリシー]** で **[User Right Assignment]** \(ユーザー権限の割り当て\) を選択し、 **[ボリュームの保守タスクを実行]** プロパティを変更します。

## <a name="performance-considerations"></a>パフォーマンスに関する考慮事項

データベース ファイルの初期化プロセスでは、初期化中にファイルの新しい領域にゼロが書き込まれます。 このプロセスの実行時間は、初期化されるファイル部分のサイズと、ストレージ システムの応答時間と容量によって異なります。 初期化に時間がかかる場合は、SQL Server Errorlog とアプリケーション ログに次のメッセージが記録されている可能性があります。

```
Msg 5144
Autogrow of file '%.*ls' in database '%.*ls' was cancelled by user or timed out after %d milliseconds.  Use ALTER DATABASE to set a smaller FILEGROWTH value for this file or to explicitly set a new file size.
```

```
Msg 5145
Autogrow of file '%.*ls' in database '%.*ls' took %d milliseconds.  Consider using ALTER DATABASE to set a smaller FILEGROWTH for this file.
```

データベースやトランザクション ログ ファイルの長い自動拡張によって、クエリ パフォーマンスの問題が発生する可能性があります。 これは、ファイルの自動拡張を必要とする操作が、ファイルの拡張操作中にロックやラッチなどのリソースに対して保持されるためです。 割り当てページのラッチで長い待機が発生する場合があります。 長い自動拡張を必要とする操作では、PREEMPTIVE_OS_WRITEFILEGATHER の待機の種類が表示されます。





## <a name="see-also"></a>参照  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)