既存のユーザー定義の Resource Governor ワークロード グループを削除します。

:::image type="icon" source="../database-engine/configure-windows/media/topic-link.gif"::: [Transact-SQL 構文表記規則](../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。

## <a name="syntax"></a>構文

```syntaxsql
DROP WORKLOAD GROUP group_name
[;]
```

## <a name="arguments"></a>引数

*group_name* : 既存のユーザー定義のワークロード グループの名前を指定します。

## <a name="remarks"></a>解説

Resource Governor の内部グループや既定のグループに対して、DROP WORKLOAD GROUP ステートメントを使用することはできません。

DDL ステートメントを実行する場合、Resource Governor の状態について詳しく理解しておくことをお勧めします。 詳細については、「[リソース ガバナー](../relational-databases/resource-governor/resource-governor.md)」を参照してください。

アクティブなセッションが含まれているワークロード グループを削除したり別のリソース プールに移動したりした場合、その変更を適用するために ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを呼び出すと失敗します。 この問題を回避するには、次のいずれかの操作を実行します。

- そのグループからすべてのセッションが切断されるまで待ってから、ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを再実行します。

- そのグループ内のセッションを KILL コマンドで明示的に停止してから、ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを再実行します。

- サーバーを再起動します。 再起動プロセスの完了後、削除したグループは作成されず、移動したグループは新しいリソース プール割り当てを使用します。

- DROP WORKLOAD GROUP ステートメントを実行してから、変更適用のためにセッションを明示的に停止するのは不適切であると判断した場合、DROP ステートメントの実行前と同じ名前でグループを再作成し、このグループを元のリソース プールに移動することができます。 変更を適用するには、ALTER RESOURCE GOVERNOR RECONFIGURE ステートメントを実行します。

## <a name="permissions"></a>アクセス許可

CONTROL SERVER 権限が必要です。

## <a name="examples"></a>例

次の例では、`adhoc` という名前のワークロード グループを削除します。

```
DROP WORKLOAD GROUP adhoc;
GO
ALTER RESOURCE GOVERNOR RECONFIGURE;
GO
```

## <a name="see-also"></a>参照

- [リソース ガバナー](../relational-databases/resource-governor/resource-governor.md)
- [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/create-workload-group-transact-sql.md)  
- [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../t-sql/statements/alter-workload-group-transact-sql.md)
- [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/create-resource-pool-transact-sql.md)
- [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/alter-resource-pool-transact-sql.md)
- [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../t-sql/statements/drop-resource-pool-transact-sql.md)
- [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../t-sql/statements/alter-resource-governor-transact-sql.md)  