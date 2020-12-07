---
description: fn_net_changes_ &lt; capture_instance &gt; (transact-sql)
title: fn_net_changes_ &lt; capture_instance &gt; (transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_net_changes_TSQL
- fn_net_changes_TSQL
- fn_net_changes
- sys.fn_net_changes
dev_langs:
- TSQL
helpviewer_keywords:
- fn_net_changes_<capture_instance>
- sys.fn_net_changes_<capture_instance>
ms.assetid: 342fa030-9fd9-4b74-ae4d-49f6038a5073
author: rothja
ms.author: jroth
ms.openlocfilehash: 59d8214083046510d9c4d71724d1aab1c96b1e1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427764"
---
# <a name="sysfn_net_changes_ltcapture_instancegt-transact-sql"></a>fn_net_changes_ &lt; capture_instance &gt; (transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **差分変更**クエリ関数のラッパー。 これらの関数を作成するために必要なスクリプトは、sys.sp_cdc_generate_wrapper_function ストアド プロシージャで生成されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
fn_net_changes_<capture_instance> ('start_time', 'end_time', '<row_filter_option>' )  
  
<capture_instance> ::= The name of the capture instance.  
<row_filter_option> ::=  
{ all  
  | all with mask  
  | all with merge  
}  
```  
  
## <a name="arguments"></a>引数  
 *start_time*  
 結果セットに含める変更テーブルエントリの範囲の下端を表す **datetime** 値です。  
  
 結果セットに含まれるのは、関連付けられたコミット時間が *start_time* よりも大きい変更テーブル>_CT capture_instance <の行だけです。  
  
 この引数に NULL 値を指定した場合、クエリ範囲の下限は、キャプチャ インスタンスの有効な範囲の下限に対応します。  
  
 *end_time*  
 結果セットに含める変更テーブルエントリの範囲の上限を表す **datetime** 値です。  
  
 このパラメーターには、次の2つの意味のいずれかを指定できます @closed_high_end_point 。 sp_cdc_generate_wrapper_function を呼び出して、ラッパー関数を作成するスクリプトを生成します。  
  
-   @closed_high_end_point = 1  
  
     $Start _lsn に値があり、対応するコミット時間が start_time 以下の <capture_instance>_CT テーブルの行だけ \_ \_ が結果セットに含まれ**start_time**ています。  
  
-   @closed_high_end_point = 0  
  
     $Start _lsn に値があり、 \_ \_ 対応するコミット時間が**start_time**よりも厳密に小さい場合は、<>_CT capture_instance 内の行だけが結果セットに含まれます。  
  
 この引数に NULL 値が指定されている場合、クエリ範囲の上端は、キャプチャインスタンスの有効な範囲の上限に対応します。  
  
 *<row_filter_option>* :: = {all | mask | all with merge}  
 メタデータ列の内容と、結果セットで返される行を制御するオプション。 次のいずれかのオプションを指定できます。  
  
 all  
 変更された行の最終的な内容がコンテンツ列に返され、その行を適用するために必要な操作がメタデータ列 __CDC_OPERATION に返されます。  
  
 すべてマスク付き  
 変更されたすべての行の最終的な内容がコンテンツ列に返され、その各行を適用するために必要な操作がメタデータ列 __CDC_OPERATION に返されます。 ラッパー関数の作成スクリプトの生成時に更新フラグの一覧を指定した場合、このオプションを使用して更新マスクを設定する必要があります。  
  
 merge を使用したすべて  
 変更されたすべての行の最終的な内容がコンテンツ列に返されます。  
  
 __CDC_OPERATION 列の値は、次の 2 つのいずれかになります。  
  
-   行を削除する必要がある場合は D  
  
-   行を挿入または更新する必要がある場合は M  
  
 変更を適用するために挿入と更新のどちらが必要であるかを特定するロジックでは、クエリが複雑になってしまいます。 このオプションは、挿入操作と更新操作を区別する必要がない場合に、パフォーマンスを向上させるために使用します。 この方法は、環境など、マージ操作を直接利用できるターゲット環境で最適に機能し [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ます。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|列の型|説明|  
|-----------------|-----------------|-----------------|  
|\<columns from @column_list>|**状況に応じて異なる**|ラッパーを作成するスクリプトを生成するために呼び出されたときに、 **column_list** 引数で指定された sp_cdc_generate_wrapper_function の列。 *Column_list*が NULL の場合、すべての追跡対象のソース列が結果セットに表示されます。|  
|__CDC_OPERATION|**nvarchar (2)**|ターゲット環境に行を適用するために必要な操作を示す操作コード。 操作は、次の呼び出しで指定された引数 *row_filter_option* の値によって異なります。<br /><br /> *row_filter_option* = ' all ', ' all with mask '<br /><br /> ' D '-削除操作<br /><br /> ' I '-挿入操作<br /><br /> 'UN' : 更新操作<br /><br /> *row_filter_option* = ' all with merge '<br /><br /> ' D '-削除操作<br /><br /> 'M' : 挿入操作または更新操作|  
|\<columns from @update_flag_list>|**bit**|列名の後に "_uflag" が付加されている、ビット フラグです。 フラグが null 以外の値を使用するのは、 *row_filter_option* **= ' all with mask '** および \_ _CDC_OPERATION **= ' UN '** の場合のみです。 対応する列がクエリウィンドウ内で変更された場合は、1に設定されます。 それ以外の場合は、0 に設定されます。|  
  
## <a name="remarks"></a>解説  
 Fn_net_changes_<capture_instance> 関数は、cdc. fn_cdc_get_net_changes_<capture_instance のクエリ関数のラッパーとして機能します。 ラッパーのスクリプトを作成するには、sys.sp_cdc_generate_wrapper ストアド プロシージャを使用します。  
  
 ラッパー関数が自動的に作成されることはありません。 ラッパー関数を作成するには、次の 2 つを行う必要があります。  
  
1.  ラッパーの作成スクリプトを生成するストアド プロシージャを実行します。  
  
2.  スクリプトを実行して、実際にラッパー関数を作成します。  
  
 ラッパー関数を使用すると、LSN 値ではなく **datetime** 値によって制限された間隔内で発生した変更を体系的にクエリできます。 ラッパー関数は、指定された **datetime** 値と、クエリ関数の引数として内部的に必要な LSN 値の間に必要なすべての変換を実行します。 ラッパー関数を順番に使用して変更データのストリームを処理する場合、次の規則に従うと、データが失われたり、繰り返されたりすることはありません。 @end_time 1 回の呼び出しに関連付けられている間隔の値は、 @start_time 後続の呼び出しに関連付けられた期間の値として指定されます。  
  
 パラメーターを使用してスクリプトを作成すると @closed_high_end_point 、指定されたクエリウィンドウで閉じた上限または開いた上限をサポートするラッパーを生成できます。 つまり、コミット時間が抽出範囲の上限と等しくなるエントリを間隔に含めるかどうかを決定できます。 既定では、上限が含まれます。  
  
 **Net changes**ラッパー関数によって返される結果セットは、ラッパーが生成されたときにに含まれていた追跡対象列のみを返し @column_list ます。 @column_listが NULL の場合、追跡対象のすべてのソース列が返されます。 ソース列に続いて、操作列 __CDC_OPERATION が返されます。これは、操作を表す 1 文字か 2 文字の列です。  
  
 次に、パラメーターで識別された各列の結果セットに、ビットフラグが追加され @update_flag_list ます。 **Net changes**ラッパーの場合、 @row_filter_option ラッパー関数の呼び出しで使用されるが ' all ' または ' all with merge ' である場合、ビットフラグは常に NULL になります。 @row_filter_optionが "all with mask" に設定されていて、__CDC_OPERATION が "d" または "I" の場合、フラグの値も NULL になります。 \__CDC_OPERATION が ' UN ' の場合、 **net**更新操作によって列が変更されたかどうかに応じて、フラグが1または0に設定されます。  
  
 変更データキャプチャの構成テンプレート ' インスタンス化 CDC Wrapper Tvf for Schema ' では、sp_cdc_generate_wrapper_function ストアドプロシージャを使用して、スキーマの定義済みクエリ関数に対するすべてのラッパー関数の作成スクリプトを取得する方法を示しています。 その後、テンプレートによってこれらのスクリプトが作成されます。 テンプレートの詳細については、「 [テンプレートエクスプローラー](../../ssms/template/template-explorer.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [sp_cdc_generate_wrapper_function &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc. fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-sql&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)  
  
  
