---
description: sp_cursoropen (Transact-SQL)
title: sp_cursoropen (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursoropen
- sp_cursoropen_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoropen
ms.assetid: 16462ede-4393-4293-a598-ca88c48ca70b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2942c06e5d63c0be25a05cd34e871447a29e7d6d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543590"
---
# <a name="sp_cursoropen-transact-sql"></a>sp_cursoropen (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  カーソルを開きます。 sp_cursoropen は、カーソルオプションおよびカーソルオプションに関連付けられた SQL ステートメントを定義し、カーソルを設定します。 sp_cursoropen は、ステートメント DECLARE_CURSOR とを組み合わせたものと同じです [!INCLUDE[tsql](../../includes/tsql-md.md)] 。 このプロシージャは、ID = 2 を指定した場合に表形式のデータストリーム (TDS) パケットで呼び出されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cursoropen cursor OUTPUT, stmt  
    [, scrollopt[ OUTPUT ] [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,boundparam][,...n]]] ]]  
```  
  
## <a name="arguments"></a>引数  
 *cursor*  
 SQL Server で生成されたカーソル識別子。 *cursor* は、カーソルに関連する後続のすべてのプロシージャ (sp_cursorfetch など) で指定する必要がある *ハンドル* 値です。 *cursor* は、 **int** 戻り値を持つ必須パラメーターです。  
  
 *カーソル* を使用すると、1つのデータベース接続で複数のカーソルをアクティブにすることができます。  
  
 *stmt*  
 カーソル結果セットを定義する必須パラメーターです。 任意の文字列型 (Unicode、サイズなどに関係なく) の有効なクエリ文字列 (構文およびバインド) は、有効な *stmt* 値型として使用できます。  
  
 *scrollopt*  
 スクロール オプションです。 *scrollopt* は省略可能なパラメーターで、次のいずれかの **int** 入力値を必要とします。  
  
|[値]|説明|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 要求された値が *stmt*によって定義されたカーソルに適していない可能性があるため、このパラメーターは入力と出力の両方として機能します。 このような場合は、SQL Server によって適切な値が割り当てられます。  
  
 *ccopt*  
 同時実行制御オプション。 *ccopt* は省略可能なパラメーターで、次のいずれかの **int** 入力値を必要とします。  
  
|[値]|説明|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (以前の LOCKCC)|  
|0x0004|**オプティミスティック** (以前は optcc と呼ばれていました)|  
|0x0008|オプティミスティック (以前の OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 *Scrollopt*と同様に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は要求された*ccopt*値をオーバーライドできます。  
  
 *行*  
 AUTO_FETCH で使用するフェッチバッファー行の数。 既定値は20行です。 *rowcount* の動作は、入力値と戻り値として割り当てられた場合に異なります。  
  
|入力値として|戻り値として|  
|--------------------|---------------------|  
|AUTO_FETCH *scrollopt* 値が指定されている場合、 *rowcount* はフェッチバッファーに格納する行の数を表します。<br /><br /> 注: AUTO_FETCH を指定した場合、>0 は有効な値ですが、それ以外の場合は無視されます。|*Scrollopt* AUTO_FETCH 値が指定されている場合を除き、結果セット内の行の数を表します。|  
  
-  
  
 *boundparam*  
 追加のパラメーターを使用することを示します。 *boundparam* は省略可能なパラメーターで、 *scrollopt* PARAMETERIZED_STMT 値が ON に設定されている場合に指定する必要があります。  
  
## <a name="return-code-values"></a>リターン コードの値  
 エラーが発生しなかった場合、sp_cursoropen は次のいずれかの値を返します。  
  
 0  
 プロシージャが正常に実行されました。  
  
 0x0001  
 実行中にエラーが発生しました (操作でエラーを生成するのに十分な重大ではない、軽度のエラーです)。  
  
 0x0002  
 非同期操作が進行中です。  
  
 0x0002  
 フェッチ操作が進行中です。  
  
 A  
 このカーソルはによって割り当て解除されて [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] おり、使用できません。  
  
 エラーが発生した場合、戻り値は不整合になる可能性があり、精度は保証できません。  
  
 *Rowcount*パラメーターが戻り値として指定されている場合、次の結果セットが発生します。  
  
 -1  
 行数が不明または適用外の場合に返されます。  
  
 -n  
 非同期設定が有効になっている場合に返されます。 *Scrollopt* AUTO_FETCH 値が指定されたときにフェッチバッファーに格納された行の数を表します。  
  
 RPC が使用されている場合、戻り値は次のようになります。  
  
 0  
 プロシージャが正常に実行されました。  
  
 1  
 プロシージャが失敗しました。  
  
 2  
 キーセット カーソルが非同期に生成されています。  
  
 16  
 高速順方向カーソルが自動的に閉じられました。  
  
> [!NOTE]  
>  Sp_cursoropen プロシージャが正常に実行された場合、RPC の戻りパラメーターと TDS 列形式の情報 (0xa0 & 0xa1 messages) を含む結果セットが送信されます。 失敗した場合は、1つまたは複数の TDS エラーメッセージが送信されます。 どちらの場合も、行データは返されず、 *done* メッセージカウントはゼロになります。 7.0 より前のバージョンを使用している場合 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、0xa0、0xa1 (SELECT ステートメントの標準) は、0xa5 および0xa5 のトークンストリームと共に返されます。 7.0 を使用している場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、0xa5 および0xa5 のトークンストリームと共に0x81 が返されます (SELECT ステートメントの標準)。  
  
## <a name="remarks"></a>解説  
  
## <a name="stmt-parameter"></a>stmt パラメーター  
 *Stmt*でストアドプロシージャの実行を指定する場合、入力パラメーターは、 *stmt*文字列の一部として、または*boundparam*引数として指定することによって、定数として定義することができます。 宣言された変数は、この方法でバインドされたパラメーターとして渡すことができます。  
  
 *Stmt*パラメーターの許可される内容は、 *ccopt* ALLOW_DIRECT の戻り値が、またはその他の*ccopt*値にリンクされているかどうかによって異なります。つまり、次のようになります。  
  
-   ALLOW_DIRECT が指定されていない場合、 [!INCLUDE[tsql](../../includes/tsql-md.md)] 1 つの select ステートメントを含むストアドプロシージャに対してを呼び出す select ステートメントまたは EXECUTE ステートメントを使用する必要があります。 さらに、SELECT ステートメントはカーソルとして修飾する必要があります。つまり、キーワード SELECT INTO または FOR BROWSE を含めることはできません。  
  
-   ALLOW_DIRECT が指定されている場合、1つ以上のステートメントが発生する可能性があります。これには、 [!INCLUDE[tsql](../../includes/tsql-md.md)] 複数のステートメントを使用して他のストアドプロシージャを実行することもできます。 Select 以外のステートメント、またはキーワード SELECT INTO または FOR BROWSE を含む SELECT ステートメントは、単純に実行され、カーソルの作成にはなりません。 複数のステートメントのバッチに含まれている SELECT ステートメントについても同様です。 SELECT ステートメントに、カーソルのみに関連する句が含まれている場合、それらの句は無視されます。 たとえば、 *ccopt* の値が0x2002 の場合、これはの要求です。  
  
    -   スクロール ロックを使用するカーソル (カーソルの条件を満たしている単一の SELECT ステートメントだけがある場合)。  
  
    -   複数のステートメント、単一の非 SELECT ステートメント、またはカーソルとして修飾されていない SELECT ステートメントがある場合は、直接ステートメントを実行します。  
  
## <a name="scrollopt-parameter"></a>scrollopt パラメーター  
 最初の5つの *scrollopt* 値 (KEYSEY、DYNAMIC、FORWARD_ONLY、STATIC、および FAST_FORWARD) は、同時には指定できません。  
  
 PARAMETERIZED_STMT と CHECK_ACCEPTED_TYPES は、または最初の5つの値のいずれかにリンクできます。  
  
 AUTO_FETCH と AUTO_CLOSE は、または FAST_FORWARD にリンクできます。  
  
 CHECK_ACCEPTED_TYPES がオンになっている場合は、最後の5つの *scrollopt* 値 (KEYSET_ACCEPTABLE `,` DYNAMIC_ACCEPTABLE、FORWARD_ONLY_ACCEPTABLE、STATIC_ACCEPTABLE、または FAST_FORWARD_ACCEPTABLE) の少なくとも1つが on である必要があります。  
  
 静的カーソルは常に READ_ONLY として開かれます。 したがって、このカーソルを使用して基になるテーブルを更新することはできません。  
  
## <a name="ccopt-parameter"></a>ccopt パラメーター  
 最初の4つの *ccopt* 値 (READ_ONLY、SCROLL_LOCKS、および両方のオプティミスティック値) は相互に排他的です。  
  
> [!NOTE]  
>  最初の4つの *ccopt* 値のいずれかを選択すると、カーソルが読み取り専用かどうか、またはロックまたはオプティミスティックメソッドを使用して更新が失われないようにするかどうかが決まります。 *Ccopt*の値が指定されていない場合、既定値はオプティミスティックです。  
  
 ALLOW_DIRECT と CHECK_ACCEPTED_TYPES は、または最初の4つの値のいずれかにリンクできます。  
  
 UPDT_IN_PLACE は、READ_ONLY、SCROLL_LOCKS、またはいずれかのオプティミスティック値によってリンクできます。  
  
 CHECK_ACCEPTED_TYPES がオンの場合、最後の4つの *ccopt* 値 (READ_ONLY_ACCEPTABLE、SCROLL_LOCKS_ACCEPTABLE、またはいずれかの OPTIMISTIC_ACCEPTABLE 値) の少なくとも1つが on である必要があります。  
  
 位置指定更新および削除関数は、フェッチバッファー内でのみ実行できます。 *ccopt* の値が SCROLL_LOCKS またはオプティミスティックに等しい場合にのみ実行されます。 SCROLL_LOCKS が指定された値の場合、操作は確実に成功します。 オプティミスティックが指定された値の場合、最後にフェッチされてから行が変更された場合、操作は失敗します。  
  
 指定されている値が OPTIMISTIC の場合に操作が失敗することがあるのは、タイムスタンプかチェックサム値 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって決定されます) を比較することによってオプティミスティック同時実行制御機能が実行されるためです。 一致しない行があると操作が失敗します。  
  
 戻り値として UPDT_IN_PLACE を指定すると、次の結果が制御されます。  
  
-   一意のインデックスを持つテーブルで位置指定更新を実行するときに設定しなかった場合、カーソルによってその行がその作業テーブルから削除され、カーソルによって使用されるキー列の最後に挿入され、その結果、列が変更されます。  
  
-   ON に設定した場合、カーソルは単に作業テーブルの元の行のキー列を更新します。  
  
## <a name="bound_param-parameter"></a>bound_param パラメーター  
 パラメーター名は、コード内のエラーメッセージに従って PARAMETERIZED_STMT が指定されている場合は *paramdef* である必要があります。 PARAMETERIZED_STMT が指定されていない場合は、エラーメッセージに名前が指定されていません。  
  
## <a name="rpc-considerations"></a>RPC に関する考慮事項  
 RPC RETURN_METADATA 入力フラグを0x0001 に設定して、カーソル選択リストのメタデータを TDS ストリームで返すように要求することができます。  
  
## <a name="examples"></a>例  
  
### <a name="bound_param-parameter"></a>bound_param パラメーター  
 5番目以降のパラメーターは、入力パラメーターとしてステートメントプランに渡されます。 最初のパラメーターは、次の形式の文字列である必要があります。  
  
 *{ローカル変数名データ型}[,...非該当*  
  
 後続のパラメーターは、ステートメントで *ローカル変数名* の代わりに使用する値を渡すために使用されます。  
  
## <a name="see-also"></a>参照  
 [sp_cursorfetch &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
