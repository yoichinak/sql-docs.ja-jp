---
description: sp_changemergepublication (Transact-sql)
title: sp_changemergepublication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergepublication_TSQL
- sp_changemergepublication
helpviewer_keywords:
- sp_changemergepublication
ms.assetid: 81fe1994-7678-4852-980b-e02fedf1e796
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e909e343a22ca1a249e5de03bc5eb64948e982cd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541907"
---
# <a name="sp_changemergepublication-transact-sql"></a>sp_changemergepublication (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マージパブリケーションのプロパティを変更します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changemergepublication [ @publication= ] 'publication'  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` パブリケーションの名前です。 *publication* は **sysname**,、既定値はありません。  
  
`[ @property = ] 'property'` 指定されたパブリケーションの変更対象となるプロパティです。 *プロパティ* は **sysname**で、次の表に示すいずれかの値を指定できます。  
  
`[ @value = ] 'value'` 指定したプロパティの新しい値。 *値* は **nvarchar (255)**,、次の表に一覧表示されているいずれかの値を指定できます。  
  
 次の表では、変更できるパブリケーションのプロパティについて説明し、それらのプロパティの値に対する制限について説明します。  
  
|プロパティ|[値]|説明|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|匿名サブスクリプションを許可します。|  
||**false**|匿名サブスクリプションは許可されません。|  
|**allow_partition_realignment**|**true**|サブスクライバーのパーティションの一部ではなくなったデータを削除することによって、パーティション変更の結果を反映するために、削除がサブスクライバーに送信されます。 これは既定の動作です。|  
||**false**|古いパーティションのデータはサブスクライバー側に残ります。パブリッシャーでこのデータに変更を加えてもこのサブスクライバーにはレプリケートされません。 代わりに、サブスクライバーで行われた変更がパブリッシャーにレプリケートされます。 これは、履歴目的でデータにアクセスできる必要がある場合に、古いパーティションからサブスクリプションのデータを保持するために使用されます。|  
|**allow_pull**|**true**|指定されたパブリケーションでは、プルサブスクリプションが許可されます。|  
||**false**|指定したパブリケーションに対してプル サブスクリプションを許可しません。|  
|**allow_push**|**true**|指定したパブリケーションに対してプッシュ サブスクリプションを許可します。|  
||**false**|指定したパブリケーションに対してプッシュ サブスクリプションを許可しません。|  
|**allow_subscriber_initiated_snapshot**|**true**|サブスクライバーはスナップショット処理を開始できます。|  
||**false**|サブスクライバーはスナップショット処理を開始できません。|  
|**allow_subscription_copy**|**true**|このパブリケーションをサブスクライブするサブスクリプション データベースをコピーすることができます。|  
||**false**|このパブリケーションをサブスクライブするサブスクリプション データベースをコピーすることはできません。|  
|**allow_synctoalternate**|**true**|代替同期パートナーがこのパブリッシャーと同期できるようにします。|  
||**false**|代替同期パートナーがこのパブリッシャーと同期することを許可しません。|  
|**allow_web_synchronization**|**true**|サブスクリプションは HTTPS 上で同期できます。|  
||**false**|サブスクリプションは HTTPS 上で同期できません。|  
|**alt_snapshot_folder**||スナップショットの代替フォルダーの場所を示します。|  
|**automatic_reinitialization_policy**|**1**|サブスクライバーから変更をアップロードしてからサブスクリプションを再初期化します。|  
||**0**|最初に変更をアップロードせずにサブスクリプションを再初期化します。|  
|**centralized_conflicts**|**true**|すべての競合レコードはパブリッシャーに格納されます。 このプロパティを変更する場合は、既存のサブスクライバーを再初期化する必要があります。|  
||**false**|競合レコードは、競合の解決で失われたサーバーに格納されます。 このプロパティを変更する場合は、既存のサブスクライバーを再初期化する必要があります。|  
|**compress_snapshot**|**true**|代替スナップショット フォルダー内のスナップショットは CAB 形式に圧縮されます。 既定のスナップショットフォルダー内のスナップショットは圧縮できません。 このプロパティを変更するには、新しいスナップショットが必要です。|  
||**false**|既定では、スナップショットは圧縮されません。 このプロパティを変更するには、新しいスナップショットが必要です。|  
|**conflict_logging**|**publisher**|競合レコードはパブリッシャーに格納されます。|  
||**サブスクライバ**|競合レコードは、競合の原因となったサブスクライバーに保存されます。 サブスクライバーではサポートされていません [!INCLUDE[ssEW](../../includes/ssew-md.md)] *。*|  
||**両方とも**|競合レコードは、パブリッシャーとサブスクライバーの両方に保存されます。|  
|**conflict_retention**||競合を保持する保有期間を日数で指定する **int** です。 *Conflict_retention*を**0**に設定すると、競合のクリーンアップは必要ありません。|  
|**description**||パブリケーションの説明です。|  
|**dynamic_filters**|**true**|パブリケーションは動的な句に基づいてフィルター処理されます。|  
||**false**|パブリケーションは動的にフィルター選択されません。|  
|**enabled_for_internet**|**true**|パブリケーションがインターネットに対して有効になっています。 ファイル転送プロトコル (FTP) を使用して、スナップショット ファイルをサブスクライバーに転送できます。 パブリケーションの同期ファイルは、C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\ftp ディレクトリに格納されます。|  
||**false**|パブリケーションはインターネットに対応していません。|  
|**ftp_address**||ディストリビューター用の FTP サービスのネットワークアドレス。 パブリケーションのスナップショット ファイルを格納する場所を指定します。|  
|**ftp_login**||FTP サービスへの接続に使用されるユーザー名です。|  
|**ftp_password**||FTP サービスへの接続に使用するユーザーパスワード。|  
|**ftp_port**||ディストリビューターの FTP サービスのポート番号。 パブリケーションのスナップショット ファイルが格納される FTP サイトの TCP ポート番号を指定します。|  
|**ftp_subdirectory**||パブリケーションが FTP を使用したスナップショットの配布をサポートしている場合にスナップショットファイルを作成する場所を指定します。|  
|**generation_leveling_threshold**|**int**|生成に含まれる変更の数を指定します。 生成とは、パブリッシャーまたはサブスクライバーに配信される変更のコレクションです。|  
|**keep_partition_changes**|**true**|同期は最適化され、変更されたパーティション内の行を持つサブスクライバーだけが影響を受けます。 このプロパティを変更するには、新しいスナップショットが必要です。|  
||**false**|同期は最適化されず、サブスクライバーに送信されるパーティションは、パーティション内のデータが変更されたときに検証されます。 このプロパティを変更するには、新しいスナップショットが必要です。|  
|**max_concurrent_merge**||これは、パブリケーションに対して実行できる同時マージプロセスの最大数を表す **int** です。 0の場合、制限はありません。この数を超えるマージプロセスが同時に実行されるようにスケジュールされている場合、余分なジョブは、マージプロセスが終了するまでキューに入れられます。|  
|**max_concurrent_dynamic_snapshots**||これは、パラメーター化された行フィルターを使用するマージパブリケーションに対して同時に実行できる、フィルター選択されたデータスナップショットを生成するためのスナップショットセッションの最大数を表す **int** です。 **0**の場合、制限はありません。 ここで指定した数を超えるスナップショット処理が同時に実行されるようにスケジュールすると、超過したジョブはキューに保存されて、現在実行中のマージ処理が終了するまで待機します。|  
|**post_snapshot_script**||**.Sql**ファイルの場所へのポインターを指定します。 ディストリビューションエージェントまたはマージエージェントは、他のすべてのレプリケートされたオブジェクトスクリプトとデータが初期同期中に適用された後に、ポストスナップショットスクリプトを実行します。 このプロパティを変更するには、新しいスナップショットが必要です。|  
|**pre_snapshot_script**||**.Sql**ファイルの場所へのポインターを指定します。 マージエージェントは、サブスクライバーでスナップショットを適用するときに、レプリケートされたオブジェクトスクリプトの前にプリスナップショットスクリプトを実行します。 このプロパティを変更するには、新しいスナップショットが必要です。|  
|**publication_compatibility_level**|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
||**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**publish_to_activedirectory**|**true**|このパラメーターは非推奨とされており、スクリプトの旧バージョンとの互換性のためにのみサポートされています。 Active Directory にパブリケーション情報を追加できなくなりました。|  
||**false**|Active Directory からパブリケーション情報を削除します。|  
|**replicate_ddl**|**1**|パブリッシャーで実行されるデータ定義言語 (DDL) ステートメントはレプリケートされます。|  
||**0**|DDL ステートメントはレプリケートされません。|  
|**保有**||指定したパブリケーションの変更を保存する*retention_period_unit*単位の数を表す**int**です。 保有期間内にサブスクリプションが同期されず、受信した保留中の変更がディストリビューター側でクリーンアップ操作によって削除された場合、サブスクリプションは有効期限切れとなり、再初期化する必要があります。 許容される最大保有期間は、9999年12月31日から現在の日付までの日数です。<br /><br /> 注: マージパブリケーションの保有期間には、異なるタイムゾーンのサブスクライバーに対応するために、24時間の猶予期間があります。|  
|**retention_period_unit**|**day**|保有期間は日数で指定します。|  
||**week**|保有期間は週単位で指定します。|  
||**month**|保有期間は月単位で指定します。|  
||**year**|保有期間は年単位で指定します。|  
|**snapshot_in_defaultfolder**|**true**|スナップショットファイルは、既定のスナップショットフォルダーに格納されます。|  
||**false**|スナップショットファイルは、 *alt_snapshot_folder*によって指定された別の場所に格納されます。 この組み合わせでは、スナップショットファイルが既定の場所と代替の場所の両方に格納されることを指定します。|  
|**snapshot_ready**|**true**|パブリケーションのスナップショットを使用できます。|  
||**false**|パブリケーションのスナップショットは使用できません。|  
|**status**|**active**|パブリケーションはアクティブな状態です。|  
||**inactive**|パブリケーションは非アクティブな状態です。|  
|**sync_mode**|**ネイティブ** または<br /><br /> **bcp ネイティブ**|すべてのテーブルのネイティブモードの一括コピープログラム出力は、初期スナップショットに使用されます。|  
||**character**<br /><br /> または **bcp 文字**|すべての非サブスクライバーに必要な初期スナップショットには、すべてのテーブルのキャラクターモードの一括コピープログラム出力が使用され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
|**use_partition_groups**<br /><br /> 注: partition_groups を使用すると、 **setupbelongs**使用されるように復帰し、 **changemergearticle**で**use_partition_groups = false**に設定した場合、スナップショットの取得後に正しく反映されない可能性があります。 スナップショットによって生成されるトリガーは、パーティショングループに準拠しています。<br /><br /> このシナリオの回避策は、状態を非アクティブに設定し、 **use_partition_groups**を変更して、状態をアクティブに設定することです。|**true**|パブリケーションは事前計算済みパーティションを使用します。|  
||**false**|パブリケーションは事前計算済みパーティションを使用しません。|  
|**validate_subscriber_info**||サブスクライバー情報の取得に使用する関数を一覧表示します。 次に、情報のパーティション分割が一貫性を保っていることをサブスクライバーが確認するときに使用する動的フィルター選択の基準の妥当性を検証します。|  
|**web_synchronization_url**||Web 同期に使用されるインターネット URL の既定値です。|  
|NULL (既定値)||*プロパティ*に対してサポートされている値の一覧を返します。|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` このストアドプロシージャによって実行される操作によって既存のスナップショットが無効になる可能性があることを確認します。 *force_invalidate_snapshot* は **ビット**,、既定値は **0**です。  
  
 **0** を指定すると、パブリケーションの変更によってスナップショットが無効になることはありません。 変更に新しいスナップショットが必要であることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1** は、パブリケーションの変更によってスナップショットがとされる可能性があることを指定します。 新しいスナップショットを必要とする既存のサブスクリプションがある場合は、既存のスナップショットに古いスナップショットをマークし、新しいスナップショットを生成するためのアクセス許可を付与します。  
  
 変更時に新しいスナップショットを生成する必要があるプロパティについては、「解説」を参照してください。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` このストアドプロシージャによって実行されるアクションで、既存のサブスクリプションの再初期化が必要になる可能性があることを確認します。 *force_reinit_subscription* は **ビット** で、既定値は **0**です。  
  
 **0** を指定すると、パブリケーションを変更しても、サブスクリプションを再初期化する必要がありません。 変更によって既存のサブスクリプションが再初期化される必要があることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1** を指定すると、パブリケーションの変更によって既存のサブスクリプションが再初期化され、サブスクリプションの再初期化を行う権限が与えられます。  
  
 変更によって既存のサブスクリプションの再初期化が必要になるプロパティについては、「解説」を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_changemergepublication** は、マージレプリケーションで使用します。  
  
 次のプロパティを変更するには、新しいスナップショットを生成する必要があります。 *Force_invalidate_snapshot*パラメーターには値**1**を指定する必要があります。  
  
-   **alt_snapshot_folder**  
  
-   **compress_snapshot**  
  
-   **dynamic_filters**  
  
-   **ftp_address**  
  
-   **ftp_login**  
  
-   **ftp_password**  
  
-   **ftp_port**  
  
-   **ftp_subdirectory**  
  
-   **post_snapshot_script**  
  
-   **publication_compatibility_level** ( **80sp3** のみ)  
  
-   **pre_snapshot_script**  
  
-   **snapshot_in_defaultfolder**  
  
-   **sync_mode**  
  
-   **use_partition_groups**  
  
 次のプロパティを変更するには、既存のサブスクリプションを再初期化する必要があります。 *Force_reinit_subscription*パラメーターには値**1**を指定する必要があります。  
  
-   **dynamic_filters**  
  
-   **validate_subscriber_info**  
  
 *Publish_to_active_directory*を使用して Active Directory するパブリケーションオブジェクトの一覧を表示するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトが Active Directory で既に作成されている必要があります。  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_changemergepublication](../../relational-databases/replication/codesnippet/tsql/sp-changemergepublicatio_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changemergepublication**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [パブリケーション プロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [パブリケーションとアーティクルのプロパティの変更](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
