---
description: sp_changemergearticle (Transact-sql)
title: sp_changemergearticle (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/09/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergearticle_TSQL
- sp_changemergearticle
helpviewer_keywords:
- sp_changemergearticle
ms.assetid: 0dc3da5c-4af6-45be-b5f0-074da182def2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 994efc8752017757bbced6df16fed2b6a4955eb1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541908"
---
# <a name="sp_changemergearticle-transact-sql"></a>sp_changemergearticle (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マージ アーティクルのプロパティを変更します。 このストアドプロシージャは、パブリッシャー側でパブリケーションデータベースに対して実行されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_changemergearticle [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>引数  
`[ @publication = ] 'publication'` アーティクルが存在するパブリケーションの名前を指定します。 *publication* は **sysname**,、既定値はありません。  
  
`[ @article = ] 'article'` 変更するアーティクルの名前を指定します。 *アーティクル* は **sysname**で、既定値はありません。  
  
`[ @property = ] 'property'` 指定されたアーティクルおよびパブリケーションの変更対象となるプロパティを指定します。 *プロパティ* は **nvarchar (30)**,、テーブルに一覧表示されている値のいずれかを指定することができます。  
  
`[ @value = ] 'value'` 指定したプロパティの新しい値を指定します。 *値* は **nvarchar (1000)**,、テーブルに一覧表示されている値のいずれかを指定することができます。  
  
 次の表では、アーティクルのプロパティとそれらのプロパティの値について説明します。  
  
|プロパティ|値|説明|  
|--------------|------------|-----------------|  
|**allow_interactive_resolver**|**true**|アーティクルに対してインタラクティブ競合回避モジュールの使用を有効にします。|  
||**false**|アーティクルに対してインタラクティブ競合回避モジュールの使用を無効にします。|  
|**article_resolver**||アーティクルのカスタム競合回避モジュール。 テーブルアーティクルにのみ適用されます。|  
|**check_permissions** (ビットマップ)|**0x00**|テーブルレベルの権限は確認されません。|  
||**0x10**|サブスクライバーで実行された INSERT ステートメントをパブリッシャーで適用する前に、テーブルレベルの権限がパブリッシャーで確認されます。|  
||**0x20**|サブスクライバーで作成された UPDATE ステートメントがパブリッシャーで適用される前に、パブリッシャー側でテーブルレベルの権限がチェックされます。|  
||**0x40**|サブスクライバーでの DELETE ステートメントがパブリッシャーで適用される前に、パブリッシャー側でテーブルレベルの権限がチェックされます。|  
|**column_tracking**|**true**|列レベルの追跡をオンにします。 テーブルアーティクルにのみ適用されます。<br /><br /> 注: 列レベルの追跡は、246列を超えるテーブルをパブリッシュする場合は使用できません。|  
||**false**|列レベルの追跡をオフにし、競合の検出を行レベルで行います。 テーブルアーティクルにのみ適用されます。|  
|**compensate_for_errors**|**true**|同期中にエラーが発生したときに、補正操作が実行されます。 詳細については、「 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)」を参照してください。|  
||**false**|補正アクションは実行されません。これは既定の動作です。 詳細については、「 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)」を参照してください。<br /><br /> 重要影響を受ける行のデータは収束していないように見えることがありますが、エラーに対処するとすぐに、変更を適用してデータを集約することができます。 ** \* \* \* \* ** アーティクルのソーステーブルが別のパブリケーションで既にパブリッシュされている場合、 *compensate_for_errors* の値は両方のアーティクルで同じである必要があります。|  
|**creation_script**||サブスクリプションデータベースでアーティクルを作成するために使用される、オプションのアーティクルスキーマスクリプトのパスと名前です。|  
|**delete_tracking**|**true**|DELETE ステートメントがレプリケートされます。これは既定の動作です。|  
||**false**|DELETE ステートメントはレプリケートされません。<br /><br /> ** \* \* 重要 \* delete_tracking \* ** **false**に設定すると、非収束になり、削除された行は手動で削除する必要があります。 **delete_tracking**|  
|**description**||記事の内容を示すエントリ。|  
|**destination_owner**||サブスクリプションデータベース内のオブジェクトの所有者の名前 ( **dbo**以外の場合)。|  
|**identity_range**||アーティクルの**identityrangemanagementoption**が**auto**に設定されている場合、または**auto_identity_range**が**true**に設定されている場合に、新しい id 値を割り当てるときに使用する範囲のサイズを指定する**bigint**です。 テーブルアーティクルにのみ適用されます。 詳細については、「 [Id 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)」の「マージレプリケーション」セクションを参照してください。|  
|**identityrangemanagementoption**|**手動**|自動での ID 範囲の管理を無効にします。 NOT FOR REPLICATION を使用して id 列にマークを付け、手動による id 範囲処理を有効にします。 詳細については、「[Replicate Identity Columns](../../relational-databases/replication/publish/replicate-identity-columns.md)」 (ID 列のレプリケート) を参照してください。|  
||"**なし**"|すべての ID 範囲の管理を無効にします。|  
|**logical_record_level_conflict_detection**|**true**|論理レコード内の任意の場所で変更が行われると、競合が検出されます。 **Logical_record_level_conflict_resolution**を**true**に設定する必要があります。|  
||**false**|既定の競合検出は、 **column_tracking**によって指定されたとおりに使用されます。|  
|**logical_record_level_conflict_resolution**|**true**|優先される論理レコード全体が、失われた論理レコードを上書きします。|  
||**false**|優先される行は、論理レコードに制約されません。|  
|**partition_options**|**0**|アーティクルのフィルター選択は静的であるか、またはパーティションごとに一意のデータのサブセットを生成しません。つまり、"重複する" パーティションになります。|  
||**1**|パーティションは重複しています。サブスクライバーで実行された DML 更新では、行が属するパーティションを変更できません。|  
||**2**|アーティクルのフィルター選択によって重複しないパーティションが生成されますが、複数のサブスクライバーが同じパーティションを受け取ることができます。|  
||**3**|アーティクルのフィルター選択により、各サブスクリプションに一意の重複しないパーティションが生成されます。<br /><br /> 注: **partition_options**に**3**を指定した場合、そのアーティクル内のデータの各パーティションに対して1つのサブスクリプションのみを使用できます。 第 2 のサブスクリプションを作成し、その新しいサブスクリプションのフィルター選択条件が既存のサブスクリプションと同じパーティションとして判別される場合、既存のサブスクリプションは削除されます。|  
|**pre_creation_command**|"**なし**"|テーブルがサブスクライバーに既に存在する場合、アクションは実行されません。|  
||**delete**|サブセットフィルターの WHERE 句に基づいて削除を発行します。|  
||**」**|テーブルを再作成する前に削除します。|  
||**truncate**|変換先テーブルを切り捨てます。|  
|**processing_order**||マージパブリケーション内のアーティクルの処理順序を示す**int**です。|  
|**pub_identity_range**||アーティクルの**identityrangemanagementoption**が**auto**に設定されている場合、または**auto_identity_range**が**true**に設定されている場合に、サーバーサブスクリプションを使用してサブスクライバーに割り当てられた範囲のサイズを指定する**bigint**です。 この ID 範囲は、再パブリッシュ元のサブスクライバーが自らのサブスクライバーに割り当てるために予約されています。 テーブルアーティクルにのみ適用されます。 詳細については、「 [Id 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)」の「マージレプリケーション」セクションを参照してください。|  
|**published_in_tran_pub**|**true**|アーティクルはトランザクションパブリケーションでもパブリッシュされます。|  
||**false**|アーティクルはトランザクション パブリケーションではパブリッシュされません。|  
|**resolver_info**||は、カスタム競合回避モジュールに必要な追加情報を指定するために使用されます。 一部の [!INCLUDE[msCoName](../../includes/msconame-md.md)] 競合回避モジュールには、入力として指定された列が必要です。 **resolver_info** は **nvarchar (255)**,、既定値は NULL です。 詳細については、「 [Microsoft COM ベースの競合回避モジュール](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)」を参照してください。|  
|**schema_option** (ビットマップ)||詳細については、このトピックで後述する「解説」を参照してください。|  
||**0x00**|スナップショットエージェントによるスクリプト作成を無効にし、 **creation_script**で提供されているスクリプトを使用します。|  
||**0x01**|オブジェクト作成スクリプト (CREATE TABLE、CREATE PROCEDURE など) を生成します。|  
||**0x10**|対応するクラスター化インデックスを生成します。|  
||**0x20**|サブスクライバーでユーザー定義データ型を基本データ型に変換します。 UDT 列が主キーの一部である場合、または計算列が UDT 列を参照している場合は、ユーザー定義型 (UDT) 列に CHECK 制約または DEFAULT 制約がある場合は、このオプションを使用できません。|  
||**0x40**|対応する非クラスター化インデックスを生成します。|  
||**0x80**|宣言された参照整合性を主キーに含めます。|  
||**0x100**|定義されている場合、テーブル アーティクル上のユーザー トリガーをレプリケートします。|  
||**0x200**|FOREIGN KEY 制約をレプリケートします。 参照先のテーブルがパブリケーションの一部でない場合、パブリッシュされたテーブルのすべての FOREIGN KEY 制約はレプリケートされません。|  
||**0x400**|CHECK 制約をレプリケートします。|  
||**0x800**|既定値をレプリケートします。|  
||**0x1000**|列レベルの照合順序をレプリケートします。|  
||**0x2000**|パブリッシュされたアーティクルのソースオブジェクトに関連付けられた拡張プロパティをレプリケートします。|  
||**0x4000**|テーブルアーティクルで定義されている場合は、一意キーをレプリケートします。|  
||**0x8000**|制約のスクリプトを作成するときに、ALTER TABLE ステートメントを生成します。|  
||**0x10000**|CHECK 制約を NOT FOR REPLICATION としてレプリケートし、同期中に制約が適用されないようにします。|  
||**0x20000**|では、制約が同期中に適用されないように、外部キー制約は NOT FOR REPLICATION としてレプリケートされます。|  
||**0x40000**|パーティション テーブルまたはインデックスに関連付けられているファイル グループをレプリケートします。|  
||**0x80000**|パーティション テーブルのパーティション構成をレプリケートします。|  
||**0x100000**|パーティションインデックスのパーティション構成をレプリケートします。|  
||**0x200000**|テーブルの統計をレプリケートします。|  
||**0x400000**|既定のバインドをレプリケートします|  
||**0x800000**|ルールのバインドをレプリケートします|  
||**0x1000000**|フルテキスト インデックスをレプリケートします。|  
||**0x2000000**|**Xml**列にバインドされている xml スキーマコレクションはレプリケートされません。|  
||**0x4000000**|**Xml**列のインデックスをレプリケートします。|  
||**0x8000000**|サブスクライバーにまだ存在しないスキーマを作成します。|  
||**0x10000000**|サブスクライバーで **xml** 列を **ntext** に変換します。|  
||**0x20000000**|で導入されたラージオブジェクトデータ型 (**nvarchar (max)**、 **varchar (max**)、 **varbinary (max)**) [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] を、でサポートされているデータ型に変換 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] します。|  
||**0x40000000**|権限をレプリケートします。|  
||**0x80000000**|パブリケーションに含まれていないオブジェクトへの依存関係を削除しようとしています。|  
||**0x100000000**|このオプションを使用すると、 **varbinary (max)** 列に FILESTREAM 属性が指定されている場合に、その属性をレプリケートできます。 テーブルをサブスクライバーにレプリケートする場合は、このオプションを指定しないでください [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 。 このスキーマオプションを設定する方法に関係なく、FILESTREAM 列を持つテーブルをサブスクライバーにレプリケートすること [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] はサポートされていません。 関連オプション **0x800000000**を参照してください。|  
||**0x200000000**|で導入された日付と時刻のデータ型 (**date**、 **time**、 **datetimeoffset**、および **datetime2**) [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] を、以前のバージョンのでサポートされているデータ型に変換し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。|  
||**0x400000000**|データとインデックスの圧縮オプションをレプリケートします。 詳細については、「 [Data Compression](../../relational-databases/data-compression/data-compression.md)」を参照してください。|  
||**0x800000000**|このオプションを設定すると、サブスクライバーの独自のファイル グループに FILESTREAM データを格納できます。 このオプションが設定されていない場合、FILESTREAM データは既定のファイルグループに格納されます。 レプリケーションでは、ファイルグループは作成されません。したがって、このオプションを設定する場合は、サブスクライバーでスナップショットを適用する前にファイルグループを作成する必要があります。 スナップショットを適用する前にオブジェクトを作成する方法の詳細については、「 [スナップショットが適用される前および後のスクリプトの実行](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)」を参照してください。<br /><br /> 関連オプション **0x100000000**を参照してください。|  
||**0x1000000000**|共通言語ランタイム (CLR) ユーザー定義型 (Udt) を **varbinary (max)** に変換します。これにより、udt 型の列を、を実行しているサブスクライバーにレプリケートできるようになり [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ます。|  
||**0x2000000000**|**Hierarchyid**データ型を**varbinary (max)** に変換します。これにより、 **hierarchyid**型の列を、を実行しているサブスクライバーにレプリケートできるようになり [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ます。 レプリケートされたテーブルで **hierarchyid** 列を使用する方法の詳細については、「 [hierarchyid &#40;transact-sql&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md)」を参照してください。|  
||**0x4000000000**|テーブルのフィルター選択されたインデックスをレプリケートします。 フィルター選択されたインデックスの詳細については、「 [フィルター選択](../../relational-databases/indexes/create-filtered-indexes.md)されたインデックスの作成」をご覧ください。|  
||**0x8000000000**|**Geography**および**geometry**データ型を**varbinary (max)** に変換して、これらの型の列を、を実行しているサブスクライバーにレプリケートできるようにし [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ます。|  
||**0x10000000000**|**Geography**型および**geometry**型の列のインデックスをレプリケートします。|  
||NULL|システムは、アーティクルに対して有効なスキーマオプションを自動生成します。|  
|**status**|**active**|テーブルをパブリッシュする初期処理スクリプトが実行されます。|  
||**unsynced**|テーブルをパブリッシュする初期処理スクリプトは、次にスナップショットエージェントを実行するときに実行されます。|  
|**stream_blob_columns**|**true**|バイナリ ラージ オブジェクトの列をレプリケートするときに、データ ストリームの最適化が使用されます。 ただし、論理レコードなどの特定のマージレプリケーション機能によって、ストリームの最適化が使用されない場合もあります。 FILESTREAM が有効になっている場合、 *stream_blob_columns*は true に設定されます。 これにより、FILESTREAM データのレプリケーションを最適な方法で実行し、メモリ使用量を減らすことができます。 FILESTREAM テーブルアーティクルで blob ストリーミングを使用しないように強制するには、 *stream_blob_columns* を false に設定します。<br /><br /> 重要このメモリ最適化を有効にすると、同期中にマージエージェントのパフォーマンスが低下する可能性があります。 ** \* \* \* \* ** このオプションは、mb 単位のデータを含む列をレプリケートする場合にのみ使用してください。|  
||**false**|バイナリラージオブジェクトの列をレプリケートする場合、最適化は使用されません。|  
|**subscriber_upload_options**|**0**|クライアントサブスクリプションを使用して、サブスクライバーで行われる更新に制限はありません。変更はパブリッシャーにアップロードされます。 このプロパティを変更する場合は、既存のサブスクライバーを再初期化する必要があります。|  
||**1**|変更は、クライアントサブスクリプションを使用するサブスクライバーで許可されますが、パブリッシャーにはアップロードされません。|  
||**2**|クライアントサブスクリプションを使用したサブスクライバーでの変更は許可されていません。|  
|**subset_filterclause**||行方向のフィルター選択を指定する WHERE 句。 テーブルアーティクルにのみ適用されます。<br /><br /> 重要パフォーマンス上の理由から、パラメーター化された行フィルター句 (など) では列名に関数を適用しないことをお勧めします。 ** \* \* \* \* ** `LEFT([MyColumn]) = SUSER_SNAME()` フィルター句で [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) を使用し、HOST_NAME の値をオーバーライドする場合は、 [convert](../../t-sql/functions/cast-and-convert-transact-sql.md)を使用してデータ型を変換する必要がある場合があります。 この場合のベストプラクティスの詳細については、「パラメーター化された [行フィルター](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」の「HOST_NAME () 値のオーバーライド」を参照してください。|  
|**threshold**||以前のバージョンのを実行しているサブスクライバーで使用される割合 [!INCLUDE[ssEW](../../includes/ssew-md.md)] の値 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 **しきい値** は、マージエージェントが新しい id 範囲を割り当てるタイミングを制御します。 [しきい値] で指定した値のパーセンテージが使用されると、マージエージェントによって新しい id 範囲が作成されます。 **Identityrangemanagementoption**が**auto**に設定されている場合、または**auto_identity_range**が**true**に設定されている場合に使用します。 テーブルアーティクルにのみ適用されます。 詳細については、「 [Id 列のレプリケート](../../relational-databases/replication/publish/replicate-identity-columns.md)」の「マージレプリケーション」セクションを参照してください。|  
|**verify_resolver_signature**|**1**|カスタム競合回避モジュールのデジタル署名を検証して、信頼できるソースからのものかどうかを確認します。|  
||**0**|カスタム競合回避モジュールのデジタル署名について、信頼されるソースからの署名であるかを判断するための検証を行いません。|  
|NULL (既定値)||*プロパティ*に対してサポートされている値の一覧を返します。|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` このストアドプロシージャによって実行される操作によって既存のスナップショットが無効になる可能性があることを確認します。 *force_invalidate_snapshot* は **ビット**,、既定値は **0**です。  
  
 **0** を指定すると、マージアーティクルへの変更によってスナップショットが無効になることはありません。 変更に新しいスナップショットが必要であることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1** に設定すると、マージアーティクルへの変更によってスナップショットが無効になる可能性があります。また、新しいスナップショットを必要とする既存のサブスクリプションが存在する場合は、既存のスナップショットに古いスナップショットとしてマークを付け、新しいスナップショットを生成する権限を与えます。  
  
 変更時に新しいスナップショットの生成が必要になるプロパティについては、「解説」を参照してください。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` このストアドプロシージャによって実行されるアクションで、既存のサブスクリプションの再初期化が必要になる可能性があることを確認します。 *force_reinit_subscription* は **ビット**,、既定値は **0**です。  
  
 **0** を指定すると、マージアーティクルへの変更によってサブスクリプションが再初期化されることはありません。 変更によって既存のサブスクリプションが再初期化される必要があることをストアドプロシージャが検出すると、エラーが発生し、変更は加えられません。  
  
 **1** を指定すると、マージアーティクルへの変更によって既存のサブスクリプションが再初期化され、サブスクリプションの再初期化を行う権限が与えられます。  
  
 変更によって既存のサブスクリプションの再初期化が必要になるプロパティについては、「解説」を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="remarks"></a>解説  
 **sp_changemergearticle** は、マージレプリケーションで使用します。  
  
 [Sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)を使用して最初に指定されたアーティクルのプロパティを変更するには**sp_changemergearticle**を使用します。これらのプロパティの詳細については、 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)を参照してください。  
  
 次のプロパティを変更するには、新しいスナップショットを生成する必要があります。また、 *force_invalidate_snapshot*パラメーターに値**1**を指定する必要があります。  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **schema_options**  
  
-   **subset_filterclause**  
  
 次のプロパティを変更するには、既存のサブスクリプションを再初期化する必要があります。また、 *force_reinit_subscription*パラメーターに値**1**を指定する必要があります。  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **identityrangemanagementoption**  
  
-   **subscriber_upload_options**  
  
-   **subset_filterclause**  
  
-   **creation_script**  
  
-   **schema_option**  
  
-   **logical_record_level_conflict_detection**  
  
-   **logical_record_level_conflict_resolution**  
  
 **Partition_options**に3を指定すると、マージエージェントが実行され、パーティションスナップショットの有効期限が短くなるたびにメタデータがクリーンアップされます。 このオプションを使用する場合は、サブスクライバーによって要求されたパーティションスナップショットを有効にすることを検討してください。 詳しくは、「 [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)」をご覧ください。  
  
 **Column_tracking**プロパティを設定するときに、他のマージパブリケーションでテーブルが既にパブリッシュされている場合、列の追跡は、このテーブルに基づく既存のアーティクルによって使用されている値と同じである必要があります。 このパラメーターは、テーブル アーティクルのみに固有のものです。  
  
 複数のパブリケーションが同じ基になるテーブルに基づいてアーティクルをパブリッシュする場合、1つのアーティクルの **delete_tracking** プロパティまたは **compensate_for_errors** プロパティを変更すると、同じテーブルに基づいている他のアーティクルに対して同じ変更が行われます。  
  
 マージ処理が使用するパブリッシャーのログインまたはユーザー アカウントが正しいテーブル権限を持っていない場合、無効な変更は競合としてログに記録されます。  
  
 **Schema_option**の値を変更しても、ビットごとの更新は実行されません。 つまり、 **sp_changemergearticle**を使用して**schema_option**を設定すると、既存のビット設定が無効になる場合があります。 既存の設定を保持するには、設定する値と*schema_option*の現在の値の間で[& (ビットごとの and)](../../t-sql/language-elements/bitwise-and-transact-sql.md)を実行する必要があります。これは[sp_helpmergearticle](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)を実行することで決定できます。  
  
> [!CAUTION]  
>  1つのパブリケーションに多く (数百) の記事があり、いずれかの記事に対して **sp_changemergearticle** を実行すると、実行が完了するまでに時間がかかることがあります。  
  
## <a name="valid-schema-option-table"></a>有効なスキーマオプションテーブル  
 次の表では、アーティクルの種類に応じて許可される *schema_option*値について説明します。  
  
|記事の種類|スキーマオプションの値|  
|------------------|--------------------------|  
|**func スキーマのみ**|**0x01** と **0x2000**|  
|**インデックス付きビュースキーマのみ**|**0x01**、 **0x040,**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x1000000**、および **0x200000**|  
|**proc スキーマのみ**|**0x01** と **0x2000**|  
|**テーブル**|すべてのオプション。|  
|**view schema only**|**0x01**、 **0x040,**、 **0x0100**、 **0x2000**、 **0x40000**、 **0x1000000**、および **0x200000**|  
  
## <a name="example"></a>例  
 [!code-sql[HowTo#sp_changemergearticle](../../relational-databases/replication/codesnippet/tsql/sp-changemergearticle-tr_1.sql)]  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_changemergearticle**を実行できるのは、固定サーバーロール**sysadmin**または固定データベースロール**db_owner**のメンバーだけです。  
  
## <a name="see-also"></a>参照  
 [アーティクルのプロパティの表示および変更](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [パブリケーションとアーティクルのプロパティの変更](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergearticle &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_dropmergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [レプリケーション ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
