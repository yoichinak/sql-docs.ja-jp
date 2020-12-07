---
description: sys.sp_cdc_enable_table (Transact-SQL)
title: sp_cdc_enable_table (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_enable_table_TSQL
- sp_cdc_enable_table_TSQL
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], enabling tables
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
ms.assetid: 26150c09-2dca-46ad-bb01-3cb3165bcc5d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5832381bab59aff32c039d4f26b648c62802d5d1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541099"
---
# <a name="syssp_cdc_enable_table-transact-sql"></a>sys.sp_cdc_enable_table (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のデータベース内の指定したソース テーブルを対象に変更データ キャプチャを有効にします。 テーブルで変更データキャプチャが有効になっている場合、テーブルに適用された各データ操作言語 (DML) 操作のレコードがトランザクションログに書き込まれます。 変更データキャプチャプロセスでは、この情報をログから取得し、一連の関数を使用してアクセスする変更テーブルに書き込みます。  
  
 変更データ キャプチャは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディッションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.sp_cdc_enable_table   
  [ @source_schema = ] 'source_schema',   
  [ @source_name = ] 'source_name' ,  [,[ @capture_instance = ] 'capture_instance' ]  
  [,[ @supports_net_changes = ] supports_net_changes ]  
  , [ @role_name = ] 'role_name'  
  [,[ @index_name = ] 'index_name' ]  
  [,[ @captured_column_list = ] 'captured_column_list' ]  
  [,[ @filegroup_name = ] 'filegroup_name' ]  
  [,[ @allow_partition_switch = ] 'allow_partition_switch' ]  
  [;]  
```  
  
## <a name="arguments"></a>引数  
`[ @source_schema = ] 'source_schema'` ソーステーブルが属しているスキーマの名前を指定します。 *source_schema* は **sysname**であり、既定値はありません。 NULL にすることはできません。  
  
`[ @source_name = ] 'source_name'` 変更データキャプチャを有効にするソーステーブルの名前を指定します。 *source_name* は **sysname**であり、既定値はありません。 NULL にすることはできません。  
  
 *source_name* は、現在のデータベースに存在している必要があります。 **Cdc**スキーマのテーブルでは、変更データキャプチャを有効にできません。  
  
`[ @role_name = ] 'role_name'` 変更データへのアクセスをゲートするために使用するデータベースロールの名前を指定します。 *role_name* は **sysname** であるため、指定する必要があります。 明示的に NULL に設定した場合、変更データへのアクセスを制限する際にゲーティング ロールは使用されません。  
  
 ロールが現在存在する場合は、そのロールが使用されます。 指定されたロールが存在しない場合は、その名前でデータベース ロールの作成が試行されます。 ロール名は、ロールの作成を試行する前に、文字列の右側にある空白の領域から削除されます。 呼び出し元がデータベース内のロールを作成する権限を持っていない場合、ストアドプロシージャの操作は失敗します。  
  
`[ @capture_instance = ] 'capture_instance'` インスタンス固有の変更データキャプチャオブジェクトに名前を指定するために使用されるキャプチャインスタンスの名前を指定します。 *capture_instance* は **sysname** であり、NULL にすることはできません。  
  
 指定しない場合、ソーススキーマ名とソーステーブル名を *schemaname_sourcename*の形式で取得した名前になります。 *capture_instance* は100文字を超えることはできず、データベース内で一意である必要があります。 指定されたまたは派生したかどうかにかかわらず、 *capture_instance* 文字列の右側にある空白文字が切り捨てられます。  
  
 ソーステーブルには、最大2つのキャプチャインスタンスを含めることができます。 詳細については、「 [sp_cdc_help_change_data_capture &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)」を参照してください。  
  
`[ @supports_net_changes = ] supports_net_changes` 差分変更のクエリのサポートをこのキャプチャインスタンスで有効にするかどうかを示します。 テーブルに主キーがある場合、またはテーブルにパラメーターを使用して識別された一意のインデックスがある場合、 *supports_net_changes*は**ビット**の既定値は1です @index_name 。 それ以外の場合、既定値は 0 になります。  
  
 0の場合は、すべての変更をクエリするサポート関数のみが生成されます。  
  
 1の場合、差分変更のクエリを実行するために必要な関数も生成されます。  
  
 *Supports_net_changes*が1に設定されている場合は、 *index_name*を指定するか、ソーステーブルに主キーが定義されている必要があります。  
  
`[ @index_name = ] 'index_name_'` ソーステーブル内の行を一意に識別するために使用する一意のインデックスの名前。 *index_name* は **sysname** であり、NULL にすることができます。 指定した場合、 *index_name* ソーステーブルの有効な一意のインデックスである必要があります。 *Index_name*が指定されている場合、特定のインデックス列は、テーブルの一意の行識別子として、定義されている主キー列よりも優先されます。  
  
`[ @captured_column_list = ] 'captured_column_list'` 変更テーブルに含めるソーステーブルの列を指定します。 *captured_column_list* は **nvarchar (max)** であり、NULL を指定できます。 NULL の場合、すべての列が変更テーブルに追加されます。  
  
 列名は、ソーステーブル内の有効な列である必要があります。 主キーインデックスで定義されている列、または *index_name* によって参照されるインデックスで定義されている列を含める必要があります。  
  
 *captured_column_list* は、列名のコンマ区切りの一覧です。 リスト内の個々の列名は、二重引用符 ("") または角かっこ ([]) のいずれかを使用して、オプションで引用符で囲むことができます。 列名にコンマが埋め込まれている場合は、列名を引用符で囲む必要があります。  
  
 *captured_column_list* には、次の予約された列名を含めることはできません: **__ $ start_lsn**、 **__ $ end_lsn**、 **__ $ seqval**、 **__ $ operation**、 **__ $ update_mask**。  
  
`[ @filegroup_name = ] 'filegroup_name'` キャプチャインスタンスに対して作成された変更テーブルに使用するファイルグループを指定します。 *filegroup_name* は **sysname** であり、NULL にすることができます。 指定した場合、現在のデータベースに対して *filegroup_name* が定義されている必要があります。 NULL の場合、既定のファイルグループが使用されます。  
  
 変更データ キャプチャの変更テーブル用に、別個のファイル グループを作成することをお勧めします。  
  
`[ @allow_partition_switch = ] 'allow_partition_switch'` 変更データキャプチャが有効になっているテーブルに対して ALTER TABLE の SWITCH PARTITION コマンドを実行できるかどうかを示します。 *allow_partition_switch* は **ビット**,、既定値は1です。  
  
 非パーティションテーブルの場合、スイッチの設定は常に1であり、実際の設定は無視されます。 非パーティション テーブルで切り替え設定を明示的に 0 に設定すると、切り替え設定が無視されたことを示す警告 22857 が生成されます。 パーティション テーブルで切り替え設定を明示的に 0 に設定すると、ソース テーブルに対するパーティションの切り替え操作が許可されなくなることを示す警告 22356 が生成されます。 最後に、スイッチ設定が明示的に1に設定されているか、既定で1に設定されていて、有効になっているテーブルがパーティション分割されている場合は、パーティションスイッチがブロックされないことを示す警告22855が発行されます。 パーティションの切り替えが発生した場合、変更データキャプチャでは、スイッチによって生じる変更は追跡されません。 これにより、変更データの使用時にデータの不整合が発生します。  
  
> [!IMPORTANT]  
>  SWITCH PARTITION はメタデータの操作ですが、データの変更が発生します。 この操作に関連付けられているデータの変更は、変更データキャプチャの変更テーブルにはキャプチャされません。 3つのパーティションがあり、このテーブルに変更が加えられたテーブルについて考えてみます。 キャプチャ プロセスでは、このテーブルに対して実行されるユーザーの挿入操作、更新操作、および削除操作を追跡します。 ただし、パーティションが別のテーブルに切り替えられた場合 (一括削除の実行など)、この操作の一部として移動された行は、変更テーブルには削除された行としてキャプチャされません。 同様に、既に行が作成されている新しいパーティションがテーブルに追加された場合、これらの行は変更テーブルには反映されません。 このため、変更がアプリケーションで使用され、変更先に適用されると、データの不整合が生じる可能性があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 テーブルで変更データキャプチャを有効にするには、その前にデータベースを有効にする必要があります。 データベースで変更データキャプチャが有効になっているかどうかを確認するには、[データベースカタログビューの](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) **is_cdc_enabled**列に対してクエリを実行します。 データベースを有効にするには、 [sp_cdc_enable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md) ストアドプロシージャを使用します。  
  
 テーブルに対して変更データ キャプチャを有効にすると、変更テーブルと 1 つまたは 2 つのクエリ関数が生成されます。 変更テーブルは、キャプチャ プロセスによってトランザクション ログから抽出されたソース テーブルの変更に関するリポジトリとして機能します。 クエリ関数は、変更テーブルからデータを抽出するために使用されます。 これらの関数の名前は、次の方法で *capture_instance* パラメーターから派生します。  
  
-   すべての変更関数: **cdc. fn_cdc_get_all_changes_<capture_instance>**  
  
-   差分変更機能: **cdc. fn_cdc_get_net_changes_<capture_instance>**  
  
 また、ソーステーブルが変更データキャプチャを有効にするデータベース内の最初のテーブルであり、データベースにトランザクションパブリケーションが存在しない場合は、データベースのキャプチャジョブとクリーンアップジョブも作成され**ます sp_cdc_enable_table。** この例では、 **is_tracked_by_cdc**列を1に設定[します。](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)  
  
> [!NOTE]  
>  テーブルで変更データ キャプチャが有効になっている場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントが実行されている必要はありません。 ただし、エージェントが実行されていない場合、キャプチャプロセスではトランザクションログを処理し、変更テーブルにエントリを書き込むことはありません [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="permissions"></a>アクセス許可  
 **Db_owner**固定データベースロールのメンバーシップが必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-enabling-change-data-capture-by-specifying-only-required-parameters"></a>A. 必須パラメーターのみを指定して変更データキャプチャを有効にする  
 次の例では、テーブルに対して変更データキャプチャを有効にし `HumanResources.Employee` ます。 必須のパラメーターのみが指定されています。  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Employee'  
  , @role_name = N'cdc_Admin';  
GO  
```  
  
### <a name="b-enabling-change-data-capture-by-specifying-additional-optional-parameters"></a>B. 追加の省略可能なパラメーターを指定して変更データキャプチャを有効にする  
 次の例では、テーブルに対して変更データキャプチャを有効にし `HumanResources.Department` ます。 を除くすべてのパラメーターが指定されてい `@allow_partition_switch` ます。  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Department'  
  , @role_name = N'cdc_admin'  
  , @capture_instance = N'HR_Department'   
  , @supports_net_changes = 1  
  , @index_name = N'AK_Department_Name'   
  , @captured_column_list = N'DepartmentID, Name, GroupName'   
  , @filegroup_name = N'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_cdc_disable_table &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md)   
 [sp_cdc_help_change_data_capture &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [cdc. fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [cdc. fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [sp_cdc_help_jobs &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)  
  
  
