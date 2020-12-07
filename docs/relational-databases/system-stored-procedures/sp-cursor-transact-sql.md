---
description: sp_cursor (Transact-SQL)
title: sp_cursor (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_TSQL
- sp_cursor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor
ms.assetid: 41ade0ca-5f11-469d-bd4d-c8302ccd93b3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 62a4904a608ccfd5ed02cbf21c3342619ea32e8f
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810168"
---
# <a name="sp_cursor-transact-sql"></a>sp_cursor (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  位置指定更新を要求します。 このプロシージャは、カーソルのフェッチ バッファー内にある 1 つ以上の行に対して操作を実行します。 sp_cursor は、ID = 1 を指定した場合に表形式のデータストリーム (TDS) パケットで呼び出されます。  
  
||  
|-|  
|**適用対象**: SQL Server ( [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] から [現在のバージョン](../../sql-server/what-s-new-in-sql-server-2016.md)まで)。|  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cursor  cursor, optype, rownum, table  
    [ , value[...n]]]  
```  
  
## <a name="arguments"></a>引数  
 *cursor*  
 カーソル ハンドルです。 *cursor* は、 **int** 入力値を必要とする必須パラメーターです。 *cursor* は SQL Server によって生成され、sp_cursoropen プロシージャによって返される *ハンドル* 値です。  
  
 *optype*  
 カーソルが実行する操作を指定する必須のパラメーターです。 *optype* には、次のいずれかの **int** 入力値が必要です。  
  
|Value|名前|説明|  
|-----------|----------|-----------------|  
|0X0001|UPDATE|は、フェッチバッファー内の1つ以上の行を更新するために使用されます。  *Rownum*で指定した行には、再度アクセスして更新します。|  
|0x0002|DELETE|は、フェッチバッファー内の1つ以上の行を削除するために使用されます。 *Rownum*で指定した行には、再度アクセスして削除します。|  
|0X0004|INSERT|SQL の **insert** ステートメントを作成せずにデータを挿入します。|  
|0X0008|REFRESH|は、基になるテーブルからバッファーを補充するために使用されます。オプティミスティック同時実行制御によって、または更新後に更新または削除が失敗した場合に、行を更新するために使用できます。|  
|0X10|LOCK|指定された行を含むページで SQL Server U ロックを取得します。 このロックは、S ロックと互換性がありますが、X ロックやその他の U ロックとは互換性がありません。 短期間のロックを実装する場合に使用できます。|  
|0X20|SETPOSITION|は、プログラムが後続の SQL Server 位置指定 DELETE または UPDATE ステートメントを実行する場合にのみ使用されます。|  
|0X40|ABSOLUTE|UPDATE または DELETE との組み合わせでのみ使用できます。  ABSOLUTE は KEYSET カーソルでのみ使用されます (DYNAMIC カーソルでは無視されます。STATIC カーソルは更新できません)。<br /><br /> 注: フェッチされていないキーセット内の行に対して ABSOLUTE が指定されている場合、この操作は同時実行チェックに失敗し、返される結果を保証できません。|  
  
 *番*  
 カーソルが操作、更新、または削除を実行するフェッチバッファー内の行を指定します。  
  
> [!NOTE]  
>  これは、相対、次、または前のフェッチ操作の開始位置、および sp_cursor を使用して実行される更新や削除には影響しません。  
  
 *rownum* は、 **int** 入力値を必要とする必須パラメーターです。  
  
 1  
 フェッチバッファーの最初の行を示します。  
  
 2  
 フェッチバッファーの2番目の行を示します。  
  
 3、4、5  
 3 番目、4 番目、5 番目の行を示します。  
  
 n  
 フェッチ バッファー内の n 番目の行を示します。  
  
 0  
 フェッチ バッファー内のすべての行を示します。  
  
> [!NOTE]  
>  は、UPDATE、DELETE、REFRESH、または LOCK *optype* 値と共に使用する場合にのみ有効です。  
  
 *テーブル*  
 *Optype*が適用されるテーブルを識別するテーブル名。カーソル定義が結合またはあいまいな列名を含む場合、*値*パラメーターによって返されます。 特定のテーブルを指定しない場合、既定値は FROM 句の最初のテーブルになります。 *table* は、文字列入力値を必要とする省略可能なパラメーターです。 文字列は任意の文字または UNICODE データ型として指定できます。 *テーブル* には、マルチパートテーブル名を指定できます。  
  
 *value*  
 値を挿入または更新する場合に使用します。 *値*の文字列パラメーターは、UPDATE および INSERT の*optype*値でのみ使用されます。 文字列は任意の文字または UNICODE データ型として指定できます。  
  
> [!NOTE]  
>  *Value*のパラメーター名は、ユーザーが割り当てることができます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 RPC を使用する場合、位置指定の DELETE または UPDATE 操作にバッファー番号0を指定すると、フェッチバッファー内のすべての行について、 *行数* が 0 (失敗) または 1 (成功) の完了メッセージが返されます。  
  
## <a name="remarks"></a>注釈  
  
## <a name="optype-parameter"></a>optype パラメーター  
 SETPOSITION と UPDATE、DELETE、REFRESH、または LOCK の組み合わせを除きます。または、UPDATE または DELETE のいずれかを使用する場合、 *optype* 値は相互に排他的です。  
  
 UPDATE 値の SET 句は、 *value* パラメーターから構築されます。  
  
 INSERT *optype* 値を使用する利点の1つは、文字以外のデータを挿入用の文字形式に変換しないようにすることです。 値は、UPDATE と同じように指定されます。 必須の列が含まれていない場合、INSERT は失敗します。  
  
-   SETPOSITION の値は、RELATIVE、NEXT、または PREVIOUS のフェッチ操作の開始位置や、sp_cursor インターフェイスを使用して実行される更新や削除には影響しません。 フェッチバッファーに行が指定されていない場合は、位置が1に設定され、エラーは返されません。 SETPOSITION を実行すると、次の sp_cursorfetch 操作、T-sql **FETCH** 操作、または同じカーソルを介した SP_CURSOR setposition 操作が行われるまで、その位置は有効のままになります。 後続の sp_cursorfetch 操作では、カーソルの位置が新しいフェッチバッファーの最初の行に設定されますが、他のカーソル呼び出しは位置の値に影響しません。 SETPOSITION は、更新、更新、削除、またはロックが設定された OR 句によってリンクすることができ、その位置の値を最後に変更された行に設定するために使用できます。  
  
 フェッチバッファー内の行が、 *rownum* パラメーターによって指定されていない場合、位置は1に設定され、エラーは返されません。 設定された位置は、同じカーソルを使用して次の sp_cursorfetch 操作、T-SQL FETCH 操作、または sp_cursor SETPOSITION 操作が行われるまで有効なままになります。  
  
 SETPOSITION は、UPDATE、UPDATE、DELETE、または LOCK を使用して、または句によってリンクされ、カーソル位置が最後に変更された行に設定されます。  
  
## <a name="rownum-parameter"></a>rownum パラメーター  
 指定した場合、 *rownum* パラメーターは、フェッチバッファー内の行番号ではなく、キーセット内の行番号として解釈できます。 コンカレンシー制御はユーザーが管理する必要があります。 したがって、SCROLL_LOCKS カーソルの場合はその行のロックを独自に保持し (トランザクションを使用できます)、 OPTIMISTIC カーソルの場合は、この操作を実行する前にその行をフェッチしておく必要があります。  
  
## <a name="table-parameter"></a>table パラメーター  
 *Optype*値が update または insert で、完全な UPDATE または insert ステートメントが*値*パラメーターとして送信された場合、 *table*に指定された値は無視されます。  
  
> [!NOTE]  
>  ビューに関しては、ビューに参加しているテーブルが1つだけ変更されることがあります。 *値*パラメーターの列名にはビューの列名が反映されている必要がありますが、テーブル名には基になるベーステーブルの名前を指定できます (この場合 sp_cursor はビュー名に置き換えられます)。  
  
## <a name="value-parameter"></a>値パラメーター  
 「引数」セクションで前述したように、 *値* を使用するための規則には、次の2つの方法があります。  
  
1.  任意の名前 \@ 付きの *値* パラメーターに対して、選択リスト内の列の名前に ' ' という名前を付けることができます。 この方法には、データ変換が不要になる可能性があるという利点があります。  
  
2.  パラメーターを使用して、完全な UPDATE または INSERT ステートメントを送信するか、複数のパラメーターを使用して UPDATE ステートメントまたは INSERT ステートメントの一部を送信します。このとき、SQL Server が完全なステートメントに組み込まれます。 この例については、このトピックで後述する「例」のセクションを参照してください。  
  
## <a name="examples"></a>例  
  
### <a name="alternative-value-parameter-uses"></a>代替値パラメーターの使用  
 更新プログラム:  
  
 1つのパラメーターを使用する場合は、次の構文を使用して UPDATE ステートメントを送信できます。  
  
 `[ [ UPDATE <table name> ] SET ] {<column name> = expression} [,...n]`  
  
> [!NOTE]  
>  UPDATE \<table name> を指定した場合、 *table* パラメーターに指定した値は無視されます。  
  
 複数のパラメーターを使用する場合、最初のパラメーターは次の形式の文字列である必要があります。  
  
 `[ SET ] <column name> = expression  [,...n]`  
  
 後続のパラメーターは、次の形式にする必要があります。  
  
 `<column name> = expression  [,...n]`  
  
 この場合、 \<table name> 構築された update ステートメント内のは、指定されたか、または *table* パラメーターによって既定値になります。  
  
 挿入の場合:  
  
 1 つのパラメーターを使用する場合は、次の構文を使用して INSERT ステートメントを送信できます。  
  
 `[ [ INSERT [INTO] <table name> ] VALUES ] ( <expression> [,...n] )`  
  
> [!NOTE]  
>  INSERT *\<table name>* を指定した場合、 *table* パラメーターに指定した値は無視されます。  
  
 複数のパラメーターを使用する場合、最初のパラメーターは次の形式の文字列である必要があります。  
  
 `[ VALUES ( ] <expression>  [,...n]`  
  
 後続のパラメーターは、次の形式にする必要があります。  
  
 `expression [,...n]`  
  
 値が指定されている場合を除き、最後の式の後に ")" が続く必要があります。 この場合、 *\<table name>* 構築された UPDATE ステートメント内のは、指定されたか、または *table* パラメーターによって既定値になります。  
  
> [!NOTE]  
>  1 つのパラメーターを名前付きパラメーターとして送信することもできます ("`@VALUES`" など)。 この場合は、他の名前付きパラメーターは使用できません。  
  
## <a name="see-also"></a>参照  
 [sp_cursoropen &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
