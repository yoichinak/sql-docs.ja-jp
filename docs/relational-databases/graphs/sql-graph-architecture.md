---
description: SQL グラフのアーキテクチャ
title: SQL Graph のアーキテクチャ |Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: language-reference
helpviewer_keywords:
- SQL graph
- SQL graph, architecture
ms.assetid: ''
author: shkale-msft
ms.author: shkale
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c742ebd930066c4e242cabff781b0c61af5f566f
ms.sourcegitcommit: 442fbe1655d629ecef273b02fae1beb2455a762e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93235579"
---
# <a name="sql-graph-architecture"></a>SQL グラフのアーキテクチャ  
[!INCLUDE[sqlserver2017-asdb](../../includes/applies-to-version/sqlserver2017-asdb.md)]

SQL Graph の設計方法について説明します。 基本を理解することで、他の SQL グラフの記事を理解しやすくなります。
 
## <a name="sql-graph-database"></a>SQL グラフデータベース
ユーザーは、データベースごとに1つのグラフを作成できます。 グラフは、ノードテーブルとエッジテーブルのコレクションです。 ノードテーブルまたはエッジテーブルは、データベース内の任意のスキーマで作成できますが、すべて1つの論理グラフに属します。 ノードテーブルは、類似した種類のノードのコレクションです。 たとえば、ユーザーノードテーブルには、グラフに属するすべての Person ノードが格納されます。 同様に、エッジテーブルは同様のエッジのコレクションです。 たとえば、友人のエッジテーブルには、人物を別の人に接続するすべてのエッジが含まれています。 ノードとエッジはテーブルに格納されるため、通常のテーブルでサポートされている操作のほとんどは、ノードテーブルまたはエッジテーブルでサポートされています。 
 
 
![SQL Graph データベースアーキテクチャを示す図。](../../relational-databases/graphs/media/sql-graph-architecture.png "Sql graph データベースのアーキテクチャ")   

図 1: SQL Graph データベースのアーキテクチャ
 
## <a name="node-table"></a>ノードテーブル
ノードテーブルは、グラフスキーマ内のエンティティを表します。 ユーザー定義の列と共にノードテーブルが作成されるたびに、暗黙的な `$node_id` 列が作成されます。この列は、データベース内の特定のノードを一意に識別します。 の値は `$node_id` 自動的に生成され、 `object_id` そのノードテーブルと内部的に生成された bigint 値の組み合わせとなります。 ただし、列が選択されている場合 `$node_id` は、JSON 文字列形式の計算値が表示されます。 また、 `$node_id` は擬似列で、16進数の文字列を含む内部名にマップされます。 テーブルから選択すると、 `$node_id` 列名がとして表示され `$node_id_<hex_string>` ます。 クエリで擬似列名を使用する場合は、内部列に対してクエリを実行 `$node_id` し、16進文字列で内部名を使用することを避けることをお勧めします。

ユーザーは、ノードテーブルの作成時に列に一意の制約またはインデックスを作成することをお勧めしますが、作成されて `$node_id` いない場合は、既定の一意の非クラスター化インデックスが自動的に作成されます。 ただし、グラフ擬似列のインデックスは、基になる内部列に作成されます。 つまり、列に作成されたインデックスは、 `$node_id` 内部列に表示され `graph_id_<hex_string>` ます。   


## <a name="edge-table"></a>エッジテーブル
エッジテーブルは、グラフ内のリレーションシップを表します。 エッジは常に転送され、2つのノードに接続します。 エッジテーブルを使用すると、ユーザーはグラフ内の多対多リレーションシップをモデル化できます。 エッジテーブルには、ユーザー定義属性が含まれている場合と、存在しない場合があります。 エッジテーブルが作成されるたびに、ユーザー定義の属性と共に、エッジテーブルに3つの暗黙的な列が作成されます。

|列名    |説明  |
|---   |---  |
|`$edge_id`   |データベース内の特定のエッジを一意に識別します。 これは生成された列で、値はエッジテーブルの object_id と内部で生成された bigint 値の組み合わせです。 ただし、列が選択されている場合 `$edge_id` は、JSON 文字列形式の計算値が表示されます。 `$edge_id` は、16進数の文字列を含む内部名にマップされる擬似列です。 テーブルから選択すると、 `$edge_id` 列名がとして表示され `$edge_id_\<hex_string>` ます。 クエリで擬似列名を使用する場合は、内部列に対してクエリを実行 `$edge_id` し、16進文字列で内部名を使用することを避けることをお勧めします。 |
|`$from_id`   |エッジの発生元のノードのを格納し `$node_id` ます。  |
|`$to_id`   |`$node_id`エッジが終了するノードのを格納します。 |

特定のエッジが接続できるノードは、列および列に挿入されたデータによって管理され `$from_id` `$to_id` ます。 最初のリリースでは、エッジテーブルに制約を定義して、2種類のノードの接続を制限することはできません。 つまり、エッジは、その種類に関係なく、グラフ内の任意の2つのノードを接続できます。

列と同様に `$node_id` 、エッジテーブルを作成するときに、ユーザーが列に一意のインデックスまたは制約を作成することをお勧めしますが、作成されて `$edge_id` いない場合は、既定の一意の非クラスター化インデックスがこの列に自動的に作成されます。 ただし、グラフ擬似列のインデックスは、基になる内部列に作成されます。 つまり、列に作成されたインデックスは、 `$edge_id` 内部列に表示され `graph_id_<hex_string>` ます。 また、OLTP シナリオでは、ユーザーが (,) 列にインデックスを作成し、 `$from_id` `$to_id` エッジの方向をより高速に参照できるようにすることもお勧めします。  

図2は、ノードテーブルとエッジテーブルがデータベースにどのように格納されるかを示しています。 

![ノードとエッジテーブルの表示を示す図。](../../relational-databases/graphs/media/person-friends-tables.png "Person ノードと友人のエッジテーブル")   

図 2: ノードとエッジテーブルの表示



## <a name="metadata"></a>Metadata
ノードまたはエッジテーブルの属性を表示するには、これらのメタデータビューを使用します。
 
### <a name="systables"></a>sys.tables
次の新しい bit 型の列が SYS に追加されます。テーブル. が1に設定されている場合は、 `is_node` テーブルがノードテーブルであることを示し、が1に設定されている場合は、 `is_edge` テーブルがエッジテーブルであることを示します。
 
|列名 |データ型 |説明 |
|--- |---|--- |
|is_node |bit |1 = これはノードテーブルです |
|is_edge |bit |1 = エッジテーブル |
 
### <a name="syscolumns"></a>sys.columns
ビューには、 `sys.columns` `graph_type` `graph_type_desc` ノードテーブルとエッジテーブルの列の型を示す追加の列とが含まれています。
 
|列名 |データ型 |説明 |
|--- |---|--- |
|graph_type |int |値のセットを含む内部列。 値は、グラフの列の場合は1-8、それ以外の場合は NULL になります。  |
|graph_type_desc |nvarchar(60)  |値のセットを含む内部列 |
 
次の表に、列の有効な値の一覧を示します。 `graph_type`

|列の値  |説明  |
|---   |---   |
|1  |GRAPH_ID  |
|2  |GRAPH_ID_COMPUTED  |
|3  |GRAPH_FROM_ID  |
|4  |GRAPH_FROM_OBJ_ID  |
|5  |GRAPH_FROM_ID_COMPUTED  |
|6  |GRAPH_TO_ID  |
|7  |GRAPH_TO_OBJ_ID  |
|8  |GRAPH_TO_ID_COMPUTED  |


`sys.columns` では、ノードまたはエッジテーブルで作成された暗黙的な列に関する情報も格納されます。 次の情報は、sys. 列から取得できますが、ユーザーはノードまたはエッジテーブルからこれらの列を選択できません。 

ノードテーブルの暗黙的な列

|列名    |データ型  |is_hidden  |コメント  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |内部 `graph_id` 列  |
|$node id (_c)\<hex_string> |NVARCHAR   |0  |外部ノード `node_id` 列  |

エッジテーブル内の暗黙的な列

|列名    |データ型  |is_hidden  |コメント  |
|---  |---|---|---  |
|graph_id_\<hex_string> |bigint |1  |内部 `graph_id` 列  |
|$edge id (_c)\<hex_string> |NVARCHAR   |0  |外部 `edge_id` 列  |
|from_obj_id_\<hex_string>  |INT    |1  |ノードからの内部 `object_id`  |
|from_id_\<hex_string>  |bigint |1  |ノードからの内部 `graph_id`  |
|$from id (_c)\<hex_string> |NVARCHAR   |0  |ノードからの外部 `node_id`  |
|to_obj_id_\<hex_string>    |INT    |1  |内部からノード `object_id`  |
|to_id_\<hex_string>    |bigint |1  |内部からノード `graph_id`  |
|$to id (_c)\<hex_string>   |NVARCHAR   |0  |外部ノード `node_id`  |
 
### <a name="system-functions"></a>システム関数
次の組み込み関数が追加されました。 これらは、ユーザーが生成された列から情報を抽出するのに役立ちます。 これらのメソッドでは、ユーザーからの入力が検証されないことに注意してください。 ユーザーが無効なを指定した場合 `sys.node_id` 、メソッドは適切な部分を抽出して返します。 たとえば、OBJECT_ID_FROM_NODE_ID はを `$node_id` 入力として受け取り、このノードが属しているテーブルの object_id を返します。 
 
|組み込み   |説明  |
|---  |---  |
|OBJECT_ID_FROM_NODE_ID |から object_id を抽出します。 `node_id`  |
|GRAPH_ID_FROM_NODE_ID  |から graph_id を抽出します。 `node_id`  |
|NODE_ID_FROM_PARTS |とから node_id を構築 `object_id` します。 `graph_id`  |
|OBJECT_ID_FROM_EDGE_ID |抽出 `object_id` 元 `edge_id`  |
|GRAPH_ID_FROM_EDGE_ID  |Id の抽出元 `edge_id`  |
|EDGE_ID_FROM_PARTS |`edge_id`および id からのコンストラクト `object_id`  |



## <a name="transact-sql-reference"></a>Transact-SQL リファレンス 
[!INCLUDE[tsql-md](../../includes/tsql-md.md)]SQL Server と Azure SQL Database で導入された拡張機能について説明します。これにより、グラフオブジェクトの作成とクエリが可能になります。 クエリ言語拡張機能は、クエリを実行し、ASCII アート構文を使用してグラフを走査するのに役立ちます。
 
### <a name="data-definition-language-ddl-statements"></a>データ定義言語 (DDL) ステートメント

|タスク   |関連記事  |メモ
|---  |---  |---  |
|CREATE TABLE |[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-sql-graph.md)|`CREATE TABLE` は、ノードまたはエッジとしてのテーブルの作成をサポートするように拡張されました。 エッジテーブルには、ユーザー定義の属性が含まれている場合とない場合があることに注意してください。  |
|ALTER TABLE    |[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)|ノードテーブルとエッジテーブルは、を使用して、リレーショナルテーブルと同じように変更でき `ALTER TABLE` ます。 ユーザーは、ユーザー定義の列、インデックス、または制約を追加または変更できます。 ただし、やなどの内部グラフ列を変更すると、エラーが発生 `$node_id` `$edge_id` します。  |
|CREATE INDEX   |[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  |ユーザーは、ノードテーブルとエッジテーブルの疑似列およびユーザー定義列に対してインデックスを作成できます。 クラスター化および非クラスター化列ストアインデックスを含む、すべてのインデックスの種類がサポートされています。  |
|エッジの制約の作成    |[エッジの制約 &#40;Transact-sql&#41;](../../relational-databases/tables/graph-edge-constraints.md)  |エッジテーブルにエッジ制約を作成して特定のセマンティクスを適用し、データの整合性を維持できるようになりました。  |
|DROP TABLE |[DROP TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-table-transact-sql.md)  |ノードテーブルとエッジテーブルは、を使用して、リレーショナルテーブルと同じ方法で削除でき `DROP TABLE` ます。 ただし、このリリースでは、ノードまたはノードテーブルを削除しても、削除されたノードを指し、エッジのカスケード削除が行われないようにするための制約はありません。 ノードテーブルを削除する場合は、そのノードテーブル内のノードに接続されているエッジをユーザーが手動で削除して、グラフの整合性を維持することをお勧めします。  |


### <a name="data-manipulation-language-dml-statements"></a>データ操作言語 (DML) ステートメント

|タスク   |関連記事  |メモ
|---  |---  |---  |
|INSERT |[INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-sql-graph.md)|ノードテーブルへの挿入は、リレーショナルテーブルへの挿入と同じです。 列の値 `$node_id` が自動的に生成されます。 列または列に値を挿入しようとすると `$node_id` `$edge_id` 、エラーが発生します。 `$from_id`エッジテーブルに挿入するときに、ユーザーが列と列の値を指定する必要があり `$to_id` ます。 `$from_id` と `$to_id` は、 `$node_id` 指定されたエッジが接続するノードの値です。  |
|DELETE | [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)|ノードまたはエッジテーブルからのデータは、リレーショナルテーブルから削除するのと同じ方法で削除できます。 ただし、このリリースでは、ノードを削除しても、削除されたノードを指し、エッジのカスケード削除がサポートされないようにするための制約はありません。 ノードが削除されるたびに、グラフの整合性を維持するために、そのノードに接続しているすべてのエッジも削除されることをお勧めします。  |
|UPDATE |[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md)  |ユーザー定義列の値は、UPDATE ステートメントを使用して更新できます。 内部グラフ列、、、およびを更新する `$node_id` `$edge_id` `$from_id` `$to_id` ことはできません。  |
|MERGE |[MERGE &#40;Transact-SQL&#41;](../../t-sql/statements/merge-transact-sql.md)  |`MERGE` ステートメントは、ノードまたはエッジテーブルでサポートされています。  |


### <a name="query-statements"></a>クエリステートメント

|タスク   |関連記事  |Notes
|---  |---  |---  |
|SELECT |[SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)|ノードとエッジは内部的にテーブルとして格納されるため、SQL Server または Azure SQL Database のテーブルでサポートされている操作のほとんどは、ノードテーブルとエッジテーブルでサポートされています。  |
|MATCH  | [Transact-sql&#41;と一致 &#40;](../../t-sql/queries/match-sql-graph.md)|一致する組み込みは、グラフのパターンマッチングとトラバーサルをサポートするために導入されています。  |



## <a name="limitations-and-known-issues"></a>制限事項と既知の問題  
このリリースでは、ノードテーブルとエッジテーブルにいくつかの制限があります。
* ローカル一時テーブルまたはグローバル一時テーブルをノードテーブルまたはエッジテーブルにすることはできません。
* テーブル型とテーブル変数をノードまたはエッジテーブルとして宣言することはできません。 
* ノードテーブルとエッジテーブルは、システムバージョン管理されたテンポラルテーブルとして作成することはできません。   
* ノードテーブルとエッジテーブルをメモリ最適化テーブルにすることはできません。  
* ユーザーは、 `$from_id` `$to_id` update ステートメントを使用して、エッジの列および列を更新することはできません。 エッジが接続するノードを更新するには、新しいノードをポイントする新しいエッジを挿入し、前のノードを削除する必要があります。
* グラフオブジェクトのデータベース間クエリはサポートされていません。 


## <a name="next-steps"></a>次の手順
新しい構文の使用を開始するには、「 [SQL グラフデータベース-サンプル](./sql-graph-sample.md)」を参照してください。
 

