リソース ガバナー ワークロード グループを作成し、そのワークロード グループをリソース ガバナー リソース プールに関連付けます。 リソース ガバナーは、[!INCLUDE[msCoName](msconame-md.md)][!INCLUDE[ssNoVersion](ssnoversion-md.md)] のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。

:::image type="icon" source="../database-engine/configure-windows/media/topic-link.gif"::: [Transact-SQL 構文表記規則](../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。

## <a name="syntax"></a>構文

```syntaxsql
CREATE WORKLOAD GROUP group_name
[ WITH
    ( [ IMPORTANCE = { LOW | MEDIUM | HIGH } ]
      [ [ , ] REQUEST_MAX_MEMORY_GRANT_PERCENT = value ]
      [ [ , ] REQUEST_MAX_CPU_TIME_SEC = value ]
      [ [ , ] REQUEST_MEMORY_GRANT_TIMEOUT_SEC = value ]
      [ [ , ] MAX_DOP = value ]
      [ [ , ] GROUP_MAX_REQUESTS = value ] )
 ]
[ USING {
    [ pool_name | "default" ]
    [ [ , ] EXTERNAL external_pool_name | "default" ] ]
    } ]
[ ; ]
```

## <a name="arguments"></a>引数

*group_name*</br>
ワークロード グループのユーザー定義の名前を指定します。 *group_name* には、英数字を最大 128 文字まで使用できます。[!INCLUDE[ssNoVersion](ssnoversion-md.md)] のインスタンス内で一意である必要があり、 [識別子](../relational-databases/databases/database-identifiers.md)のルールに従っている必要があります。

IMPORTANCE = { LOW | **MEDIUM** | HIGH }</br>
ワークロード グループでの要求の相対的な重要度を指定します。 重要度は次のいずれかで、MEDIUM が既定値です。

- LOW
- MEDIUM (既定)
- HIGH

> [!NOTE]
> 各重要度の設定は、内部に計算用の数値として格納されます。

IMPORTANCE は、リソース プールに対してローカルです。同じリソース プール内の異なる重要度のワークロード グループは互いに影響しますが、別のリソース プールのワークロード グループには影響しません。

REQUEST_MAX_MEMORY_GRANT_PERCENT = *value*</br>
1 つの要求にプールから割り当てられる最大メモリ量を指定します。 *value* は、MAX_MEMORY_PERCENT で指定したリソース プールのサイズが基準になります。

*value* は、[!INCLUDE[ssSQL17](sssql17-md.md)] までは整数であり、[!INCLUDE[sql-server-2019](sssqlv15-md.md)] 以降と Azure SQL Managed Instance では float です。 既定値は 25 です。 *value* の許容範囲は 1 ～ 100 です。

> [!IMPORTANT]  
> 指定した量のみがクエリの実行時に許可されるメモリとして割り当てられます。
>
> *value* を 0 に設定すると、ユーザー定義のワークロード グループでは SORT と HASH JOIN 操作を含むクエリが実行されなくなります。
>
> 同時に他のクエリが実行されているとサーバーが空きメモリを十分に確保できない可能性があるため、 *value* を 70 より大きな値に設定することはお勧めしません。 これによってやがては、クエリの時間切れエラー 8645 が発生します。
>
> クエリのメモリ要求がこのパラメーターによって指定されている制限を超えると、サーバーは次のように対応します。
>
> - ユーザー定義のワークロード グループでは、メモリ要求が制限より低くなるか、並列処理の次数が 1 になるまで、サーバーはクエリの並列処理の次数を下げます。 それでもクエリのメモリ要求が制限を超える場合は、エラー 8657 が発生します。
>
> - 内部および既定のワークロード グループでは、そのクエリに必要なメモリの確保がサーバーによって許可されます。
>
> サーバーに十分な物理メモリがない場合は、どちらの場合も時間切れエラー 8645 が発生する可能性があります。

REQUEST_MAX_CPU_TIME_SEC = *value*</br>
要求が使用できる最大 CPU 時間を秒単位で指定します。 *value* は、0 または正の整数にする必要があります。 *value* の既定の設定が 0 の場合は、無制限を示します。

> [!NOTE]
> 既定では、リソース ガバナーでは最大時間を超過しても、要求は継続されます。 ただし、イベントが生成されます。 詳細については、「[CPU Threshold Exceeded イベント クラス](../relational-databases/event-classes/cpu-threshold-exceeded-event-class.md)」を参照してください。
> [!IMPORTANT]
> [!INCLUDE[ssSQL15](sssql15-md.md)] SP2 および [!INCLUDE[ssSQL17](sssql17-md.md)] CU3 以降では、[トレース フラグ 2422](../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) を使用すると、最大時間を超えたときにリソース ガバナーが要求を中止します。

REQUEST_MEMORY_GRANT_TIMEOUT_SEC = *value*</br>
メモリ許可 (作業バッファー メモリ) が使用可能になるのをクエリが待機できる最大時間を秒単位で指定します。 *value* は、0 または正の整数にする必要があります。 *value* の既定の設定である 0 の場合、クエリ コストに基づく内部の計算を使用して、最大時間が決定されます。

> [!NOTE]
> メモリ許可のタイムアウトに達しても、常にクエリが失敗するとは限りません。 クエリが失敗するのは、同時実行クエリ数が多すぎる場合だけです。 それ以外の場合、クエリは最小限のメモリ許可しか取得できないので、クエリのパフォーマンスが低下します。

MAX_DOP = *value*</br>
並列クエリ実行に対する **並列処理の最大限度 (MAXDOP)** を指定します。 *value* は、0 または正の整数にする必要があります。 *value* の許容範囲は 0 から 64 です。 *value* の既定の設定は 0 で、グローバル設定が使用されます。 MAX_DOP は次のように処理されます。

> [!NOTE]
> ワークロード グループの MAX_DOP では、 [並列処理の最大限度に対するサーバー構成](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)と、 **MAXDOP** [データベース スコープ構成](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)がオーバーライドされます。

> [!TIP]
> これをクエリ レベルで行うには、 **MAXDOP** [クエリ ヒント](../t-sql/queries/hints-transact-sql-query.md)を使用します。 ワークロード グループの MAX_DOP を超えない限り、クエリ ヒントとして並列処理の最大限度を設定することは有効です。 MAXDOP クエリ ヒントの値が Resource Governor を使用して構成されている値を超える場合、[!INCLUDE[ssDEnoversion](ssdenoversion-md.md)] ではリソース ガバナーの `MAX_DOP` の値が使用されます。 MAXDOP [クエリ ヒント](../t-sql/queries/hints-transact-sql-query.md)では常に、[並列処理の最大限度のサーバー構成](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)がオーバーライドされます。
>
> データベース レベルでこれを行うには、 **MAXDOP** [データベース スコープ構成](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)を使用します。
>
> これをサーバー レベルで行うには、 **並列処理の最大限度 (MAXDOP)** [サーバー構成オプション](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)を使用します。

GROUP_MAX_REQUESTS = *value*</br>
ワークロード グループで実行を許可する同時要求の最大数を指定します。 *value* には、0 または正の整数を指定する必要があります。 *value* の既定の設定は 0 であり、これでは無制限の要求が許可されます。 同時要求の最大数に達した場合、そのグループのユーザーはログインできますが、同時要求数が指定した値を下回るまで待機状態になります。

USING { *pool_name* |  **"default"** }</br>
ワークロード グループを *pool_name* で識別されるユーザー定義のリソース プールに関連付けます。 実質的には、これによってワークロード グループがグループ リソースに配置されます。 *pool_name* を指定していない場合、または USING 引数を使用していない場合、ワークロード グループは事前に定義されたリソース ガバナーの既定のプールに配置されます。

予約語の "default" を USING で使用する場合は、引用符 ("") または角かっこ ([]) で囲む必要があります。

> [!NOTE]
> 定義済みのワークロード グループおよびリソース プールではすべて、"default" などの小文字の名前が使用されています。 大文字と小文字を区別する照合順序を使用するサーバーでは、これを考慮する必要があります。 SQL_Latin1_General_CP1_CI_AS など、大文字と小文字を区別しない照合順序を使用するサーバーでは、"default" と "Default" が同じものと見なされます。

EXTERNAL external_pool_name | "default"</br>
**適用対象** : [!INCLUDE[ssNoVersion](ssnoversion-md.md)] ([!INCLUDE[ssSQL15](sssql15-md.md)] 以降)。

ワークロード グループには、外部リソース プールを指定できます。 ワークロード グループを定義し、2 つのプールに関連付けることができます。

- [!INCLUDE[ssNoVersion](ssnoversion-md.md)] ワークロードおよびクエリのリソース プール
- 外部プロセス用の外部リソース プール 詳細については、「[sp_execute_external_script &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)」を参照してください。

## <a name="remarks"></a>解説

`REQUEST_MEMORY_GRANT_PERCENT` が使用される場合、インデックスの作成では、パフォーマンスの改善のために最初に付与されたのよりも多くのワークスペース メモリを使用できます。 この特別な処理は、[!INCLUDE[ssCurrent](sscurrent-md.md)] のリソース ガバナーでサポートされています。 ただし、最初のメモリ許可も追加のメモリ許可も、リソース プール設定およびワークロード グループ設定によって制限されます。

`MAX_DOP` の制限は、[タスク](../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)ごとに設定されます。 この設定は、[要求](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)ごとまたはクエリ制限ごとではありません。 つまり、並列クエリ実行中に、1 つの要求で、[スケジューラ](../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)に割り当てられてた複数のタスクを生成することができます。 詳細については、「[スレッドおよびタスクのアーキテクチャ ガイド](../relational-databases/thread-and-task-architecture-guide.md)」を参照してください。

`MAX_DOP` が使用されていて、コンパイル時にクエリが直列としてマークされている場合は、ワークロード グループまたはサーバー構成の設定にかかわらず、実行時に並列に変更することはできません。 構成後の `MAX_DOP` は、メモリの不足時にのみ低くすることができます。 ワークロード グループの再構成は、許可メモリ キューで待機している間は認識されません。

### <a name="index-creation-on-a-partitioned-table"></a>パーティション テーブルのインデックス作成

非固定パーティション テーブルのインデックス作成によって消費されるメモリは、含まれるパーティションの数に比例します。 必要なメモリの合計が、Resource Governor のワークロード グループの設定によって課せられているクエリごとの制限 `REQUEST_MAX_MEMORY_GRANT_PERCENT` を超えると、このインデックス作成の実行に失敗します。 *"default"* ワークロード グループでは、クエリごとの制限を超えてもクエリの開始に必要な最低限のメモリを使用できるようになっているので、そのようなクエリを実行するのに十分な量のメモリが *"default"* リソース プールに対して構成されていれば、同じインデックス作成を *"default"* ワークロード グループで実行できる可能性があります。

## <a name="permissions"></a>アクセス許可

`CONTROL SERVER` 権限が必要です。

## <a name="example"></a>例

Resource Governor の既定の設定を使用し、Resource Governor の既定のプールに配置される、`newReports` という名前のワークロード グループを作成します。 この例では `default` プールを指定していますが、必須ではありません。

```sql
CREATE WORKLOAD GROUP newReports
WITH
    (REQUEST_MAX_MEMORY_GRANT_PERCENT = 2.5
      , REQUEST_MAX_CPU_TIME_SEC = 100
      , MAX_DOP = 4)    
USING "default" ;
GO
```

## <a name="see-also"></a>参照

- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-workload-group-transact-sql.md)
- [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/drop-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../t-sql/statements/alter-resource-governor-transact-sql.md)