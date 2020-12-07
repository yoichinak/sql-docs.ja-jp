---
title: '[データベースの復元] ([全般] ページ) | Microsoft Docs'
description: SQL Server でデータベースを復元するときに、[全般] ページを使用して、データベースの復元操作における対象データベースとソース データベースに関する情報を指定します。
ms.custom: ''
ms.date: 09/28/2020
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restoredb.general.f1
ms.assetid: 160cf58c-b06a-475f-9a69-2b051e5767ab
author: cawrites
ms.author: chadam
ms.openlocfilehash: cda87fffca686f8e86c7b617e502952341bd459f
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125548"
---
# <a name="restore-database-general-page"></a>[データベースの復元] ([全般] ページ)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

**[全般]** ページを使用すると、データベースの復元操作における対象データベースとソース データベースに関する情報を指定できます。  
    
-   [SSMS を使用してデータベース バックアップを復元する](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [テープ ドライブの論理バックアップ デバイスの定義 &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
> [!NOTE]  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して復元タスクを指定する場合、 **[スクリプト]** をクリックしてスクリプトの保存先を選択することにより、対応する [!INCLUDE[tsql](../../includes/tsql-md.md)] [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) スクリプトを生成できます。  
  
## <a name="permissions"></a>アクセス許可  
存在しないデータベースを RESTORE するには、ユーザーは CREATE DATABASE 権限を持っている必要があります。 既存のデータベースの場合、既定では、RESTORE 権限が **sysadmin** および **dbcreator** 固定サーバー ロールのメンバーと、データベースの所有者 (**dbo**) に与えられています。  

RESTORE 権限を持つロールのメンバーシップ情報は、インスタンスで常に利用できます。

破損していないアクセス可能なデータベースでは、固定データベース ロールのメンバーシップを確認できます。 **db_owner** 固定データベース ロールのメンバーには、RESTORE 権限が付与されません。  

固定データベース ロールのメンバーシップを確認できるのは、データベースがアクセス可能で破損していない場合のみです。 これは、RESTORE の実行時には、常に該当するとは限りませんが、**db_owner** 固定データベース ロールのメンバーには RESTORE 権限が付与されません。  

RESTORE 権限は、サーバーでメンバーシップ情報を常に確認できるロールに与えられます。 固定データベース ロールのメンバーシップを確認できるのは、データベースがアクセス可能で破損していない場合のみです。 定期的な RESTORE の実行時には、**db_owner** 固定データベース ロールのメンバーには RESTORE 権限が付与されません。  

暗号化されたバックアップから復元するには、バックアップ時の暗号化に使用された証明書または非対称キーに対する **VIEW DEFINITION** 権限が必要です。  
  
## <a name="options"></a>Options  
  
### <a name="source"></a>source  

これらのオプションによって、データベースのバックアップ セットの場所と復元するバックアップ セットが特定されます。  
  
|期間|定義|  
|----------|----------------|  
|**[データベース]**|復元するデータベースをドロップダウン リストから選択します。 このリストには、**msdb** バックアップ履歴に基づいてバックアップされたデータベースのみが含まれます。|  
|**[デバイス]**|復元対象のバックアップを含む論理バックアップ デバイスまたは物理バックアップ デバイス (テープ、URL、またはファイル) を選択します。 このデバイスは、データベース バックアップが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の別のインスタンスで作成された場合に必須となります。<br /><br /> 1 つ以上の論理バックアップ デバイスまたは物理バックアップ デバイスを選択するには、参照ボタンを選択して、 **[バックアップ デバイスの選択]** ダイアログ ボックスを開きます。 このダイアログ ボックスで、1 つのメディア セットに属する最大 64 個のデバイスを選択できます。 テープ デバイスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスが動作しているコンピューターに物理的に接続している必要があります。 バックアップ ファイルは、ローカルまたはリモートのディスク デバイスに配置できます。 詳細については、「 [バックアップ デバイス &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)」を参照してください。 Azure Storage に格納されるバックアップ ファイルのデバイスの種類として、 **[URL]** を選択することもできます。<br /><br /> **[バックアップ デバイスの選択]** ダイアログ ボックスを終了すると、選択したデバイスが **[デバイス]** の一覧に読み取り専用の値として表示されます。|  
|**[データベース]**|ドロップダウン リストから、バックアップを復元するデータベース名を選択します。<br /><br /> 注:この一覧は **[デバイス]** を選択した場合にのみ使用できます。 選択されたデバイスにバックアップを持つデータベースのみが使用できるようになります。|  
  
### <a name="destination"></a>宛先  
 **[復元先]** パネルのオプションでは、データベースと復元ポイントを指定します。  
  
|期間|定義|  
|----------|----------------|  
|**[データベース]**|復元するデータベースを一覧に入力します。 新しいデータベースを入力するか、ドロップダウン リストから既存のデータベースを選択します。 このリストには、システム データベース **master** および **tempdb** を除いた、サーバー上のすべてのデータベースが表示されます。<br /><br /> 注:パスワードで保護されたバックアップを復元するには、 [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) ステートメントを使用する必要があります。|  
|**[復元先]**|既定では、 **[復元先]** ボックスが [最後に作成されたバックアップ] に設定されます。 **[タイムライン]** を選択して、 **[バックアップのタイムライン]** ダイアログ ボックスを表示することもできます。これによって、データベースのバックアップ履歴がタイムラインの形式で表示されます。 **[タイムライン]** をクリックして、データベースを復元する特定の **日付時刻** を選択します。 データベースは、この指定された時点での状態に復元されます。 「 [Backup Timeline](../../relational-databases/backup-restore/backup-timeline.md)」を参照してください。|  
  
### <a name="restore-plan"></a>復元プラン  
  
|期間|定義|値|  
|----------|----------------|------------|  
|**復元するバックアップ セット**|指定した場所にあるバックアップ セットを表示します。 バックアップ操作により、メディア セット内のすべてのデバイスに分散されるバックアップ セットが作成されます。 既定では、必要なバックアップ セットの選択に基づいて、復元操作の目的を達成するための復旧プランが提案されます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]により、**msdb** 内のバックアップ履歴が使用されます。 履歴を使用して、データベースの復元に必要なバックアップが識別され、復元プランが作成されます。 たとえば、データベースの復元の場合、最新の完全データベース バックアップを選択した後、(存在する場合は) 最新の差分バックアップを選択する復元プランが作成されます。 完全復旧モデルの復元プランの場合は、すべてのログ バックアップが選択されます。<br /><br /> 推奨された復元計画を変更するには、グリッドの選択を変更します。 バックアップの選択を解除すると、それに依存するその他のバックアップも自動的に選択が解除されます。<br /><br /> **[手動での選択]** がオンになっている場合にのみ、チェック ボックスを使用できるようになります。 復元されるバックアップ セットを選択できます。<br /><br /> **[手動での選択]** がオンになっていると、復元プランが変更されるたびに、その正確性が確認されます。 バックアップのシーケンスが正しくない場合は、エラー メッセージが表示されます。|**復元**: <br />                          このチェック ボックスをオンにすると、バックアップ セットが復元されます。<br /><br /> **Name**: <br />                          バックアップ セットの名前です。<br /><br /> **Component**:バックアップされるコンポーネント: **[データベース]** 、 **[ファイル]** 、または **\<blank>** (トランザクション ログ用)。<br /><br /> **[種類]** :バックアップの種類: **[完全]** 、 **[差分]** 、 **[トランザクション ログ]** 。<br /><br /> **[サーバー]** :バックアップ操作を実行した [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスの名前。<br /><br /> **データベース**: <br />                          バックアップ操作に呼び出されるデータベース名です。<br /><br /> **[位置]** :ボリューム内でのバックアップ セットの位置。<br /><br /> **[最初の LSN]** : <br />                          バックアップ セット内の先頭のトランザクションのログ シーケンス番号。 ファイル バックアップの場合は空白。<br /><br /> **[最後の LSN]** : <br />                          バックアップ セット内の末尾のトランザクションのログ シーケンス番号。 ファイル バックアップの場合は空白。<br /><br /> **[チェックポイントの LSN]** : <br />                          バックアップが作成された時点で最新のチェックポイントのログ シーケンス番号 (LSN)。<br /><br /> **[全 LSN]** : <br />                          最新のデータベース全体のバックアップのログ シーケンス番号。<br /><br /> **[開始日]** : <br />                          バックアップ操作が開始した日時で、クライアントの地域設定で表示されます。<br /><br /> **[完了日]** : <br />                          バックアップ操作が完了したときの日付と時刻。クライアントの地域設定で表示されます。<br /><br /> **Size**: <br />                          バックアップ セットのサイズ (バイト単位) です。<br /><br /> **User Name**: <br />                          バックアップ操作を実行したユーザーの名前。<br /><br /> **[有効期限]** : <br />                          バックアップ セットの期限が切れる日付と時刻。|  
|**[バックアップ メディアの検証]**|選択したバックアップ セットに対して RESTORE VERIFY_ONLY ステートメントを呼び出します。<br /><br /> 注: 検証は時間がかかる操作なので、ダイアログ フレームワークの進行状況モニターを使用して進行状況の追跡や、実行の取り消しを行うことができます。<br /><br /> このボタンを使用すると、選択したバックアップ ファイルの整合性を、復元前にチェックできます。<br /><br /> バックアップ セットの整合性のチェック中は、ダイアログ ボックスの左下の進行状況が、"実行しています" ではなく "検証しています" になります。||  
  
## <a name="compatibility-support"></a>互換性サポート  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]では、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降のバージョンを使用して作成したデータベース バックアップからユーザー データベースを復元できます。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] から [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] を使用して作成された **master**、**model**、**msdb** のバックアップを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で復元することはできません。 また、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で作成されたバックアップを以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]で復元することもできません。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、以前のバージョンとは異なる既定パスが使用されます。 以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の既定の場所に作成されたデータベースを復元するには、MOVE オプションを使用する必要があります。  
  
 以前のバージョンのデータベースを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]に復元すると、データベースが自動的にアップグレードされます。 通常、データベースは直ちに使用可能になります。 ただし、 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] データベースにフルテキスト インデックスがある場合、アップグレード プロセスでは、 **[フルテキスト アップグレード オプション]** サーバー プロパティの設定に応じて、インポート、リセット、または再構築が行われます。 アップグレード オプションが **[インポート]** または **[再構築]** に設定されている場合、アップグレード中はフルテキスト インデックスを使用できなくなります。 インデックスを作成するデータ量によって、インポートには数時間、再構築には最大でその 10 倍の時間がかかることがあります。 なお、アップグレード オプションが **[インポート]** に設定されており、フルテキスト カタログが使用できない場合は、関連付けられたフルテキスト インデックスが再構築されます。  
  
## <a name="restoring-from-an-encrypted-backup"></a>暗号化されたバックアップからの復元  
 復元するには、最初にバックアップの作成に使用された証明書または非対称キーを復元先のインスタンスで使用できる必要があります。 復元を実行するアカウントには、証明書または非対称キーに対する **VIEW DEFINITIONS** 権限が必要です。 バックアップの暗号化に使用する証明書は更新しないでください。  
  
## <a name="restoring-from-microsoft-azure-storage"></a>Microsoft Azure Storage からの復元  
**[バックアップ デバイスの選択]** ダイアログ ボックスの **[バックアップ メディアの種類:]** ドロップダウン リストから **[URL]** を選択します。  次に、 **[追加]** を選択して、 **[バックアップ ファイルの場所を選択]** を開きます。 既存の SQL Server 資格情報および Azure ストレージ コンテナーを選択します。 共有アクセス署名を使用して、新しい Azure ストレージ コンテナーを追加します。または、既存のストレージ コンテナーの共有アクセス署名と SQL Server 資格情報を生成します。 ストレージ アカウントに接続されると、バックアップ ファイルが **[Microsoft Azure でのバックアップ ファイルの位置指定]** ダイアログ ボックスに表示され、復元に使用するファイルを選択できます。  「 [Microsoft Azure サブスクリプションへの接続](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md)」も参照してください。
  
## <a name="see-also"></a>参照  
 [バックアップ デバイス &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [デバイスからのバックアップ復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)   
 [マークされたトランザクションへのデータベースの復元 &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [トランザクション ログ バックアップの復元 &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)   
 [バックアップ テープまたはバックアップ ファイルの内容の表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)   
 [論理バックアップ デバイスのプロパティと内容の表示 &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)   
 [メディア セット、メディア ファミリ、およびバックアップ セット &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [RESTORE の引数 &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [トランザクション ログ バックアップの適用 &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md)  
  
  
