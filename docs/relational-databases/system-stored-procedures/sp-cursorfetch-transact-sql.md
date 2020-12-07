---
description: sp_cursorfetch (Transact-sql)
title: sp_cursorfetch (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorfetch
- sp_cursorfetch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorfetch
ms.assetid: 14513c5e-5774-4e4c-92e1-75cd6985b6a3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 45621f2b99616085a2543972df7109b2f2fe8e3c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543595"
---
# <a name="sp_cursorfetch-transact-sql"></a>sp_cursorfetch (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベースから1つ以上の行のバッファーをフェッチします。 このバッファー内の行のグループを、カーソルの *フェッチバッファー*と呼びます。 sp_cursorfetch は、ID = 7 を指定した場合に表形式のデータストリーム (TDS) パケットで呼び出されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cursorfetch cursor  
    [ , fetchtype[ , rownum [ , nrows] ]]   
```  
  
## <a name="arguments"></a>引数  
 *cursor*  
 によっ*handle*て生成され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_cursoropen によって返されるハンドル値です。 *cursor* は、 **int** 入力値を必要とする必須パラメーターです。 詳細については、このトピックで後述する「解説」を参照してください。  
  
 *fetchtype*  
 フェッチするカーソル バッファーを指定します。 *fetchtype* は省略可能なパラメーターで、次のいずれかの整数入力値を必要とします。  
  
|[値]|名前|説明|  
|-----------|----------|-----------------|  
|0x0001|FIRST|*Nrows* rows の最初のバッファーをフェッチします。 *Nrows*が0の場合、カーソルは結果セットの前に配置され、行は返されません。|  
|0x0002|NEXT|*Nrows* rows の次のバッファーをフェッチします。|  
|0x0004|前|*Nrows* rows の前のバッファーをフェッチします。<br /><br /> 注: FORWARD_ONLY カーソルに対して PREV を使用すると、FORWARD_ONLY は一方向のスクロールしかサポートされないため、エラーメッセージが返されます。|  
|0x0008|LAST|*Nrows*行の最後のバッファーをフェッチします。 *Nrows*が0の場合、カーソルは結果セットの後に配置され、行は返されません。<br /><br /> 注: FORWARD_ONLY カーソルに対して LAST を使用するとエラーメッセージが返されます。 FORWARD_ONLY では、1方向のスクロールしかサポートされていないためです。|  
|0x10|ABSOLUTE|*Rownum*行から始まる*nrows*行のバッファーをフェッチします。<br /><br /> 注: FORWARD_ONLY では、動的カーソルまたは FORWARD_ONLY カーソルに対して ABSOLUTE を使用するとエラーメッセージが返されます。これは、1方向でのスクロールのみがサポートされるためです。|  
|0x20|RELATIVE|現在のブロックの最初の行の行の*rownum*値として指定された行で始まる*nrows*行のバッファーをフェッチします。 この場合、 *rownum* には負の数を指定できます。<br /><br /> 注: FORWARD_ONLY カーソルに対して相対を使用するとエラーメッセージが返されます。 FORWARD_ONLY では、1方向でのスクロールのみがサポートされているためです。|  
|0x80|REFRESH|基になるテーブルのデータをバッファーに再読み込みします。|  
|0x100|INFO|カーソルに関する情報を取得します。 この情報は、 *rownum* および *nrows* パラメーターを使用して返されます。 したがって、INFO を指定した場合、 *rownum* と *nrows* は出力パラメーターになります。|  
|0x200|PREV_NOADJUST|PREV と同じように使用されます。 ただし、途中で結果セットの先頭に到達した場合に結果が変わる可能性があります。|  
|0x400|SKIP_UPDT_CNCY|INFO 以外の *fetchtype* 値のいずれかで使用する必要があります。|  
  
> [!NOTE]  
>  値0x40 はサポートされていません。  
  
 詳細については、このトピックで後述する「解説」を参照してください。  
  
 *番*  
 は、入力または出力に整数値のみを使用するか、両方とも使用して、ABSOLUTE および INFO *fetchtype* 値の行の位置を指定するために使用される省略可能なパラメーターです。 *rownum* は、 *fetchtype* ビット値の相対行オフセットとして機能します。 他のすべての値では、 *rownum*は無視されます。 詳細については、このトピックで後述する「解説」を参照してください。  
  
 *nrows*  
 フェッチする行数を指定するために使用される省略可能なパラメーターです。 場合 *nrows* が指定されていない、既定値は20行です。 データを返さずに位置を設定するには、値0を指定します。 *Nrows*が*fetchtype* INFO クエリに適用されると、そのクエリ内の行の合計数が返されます。  
  
> [!NOTE]  
>  *nrows* は、REFRESH *fetchtype* ビット値によって無視されます。  
>   
>  詳細については、このトピックで後述する「解説」を参照してください。  
  
## <a name="return-code-values"></a>リターン コードの値  
 ビット値の情報を指定すると、次の表に示すような値が返されます。  
  
> [!NOTE]  
>     行が返されない場合、バッファーの内容は元のままになります。  
  
|*\<rownum>*|設定値|  
|------------------|------------|  
|開いていない場合|0|  
|結果セットより前の場合|0|  
|結果セットの後に配置されている場合|-1|  
|キーセットと静的カーソルの場合|結果セット内の現在位置の絶対行番号|  
|動的カーソルの場合|1|  
|絶対|-1 は、セット内の最後の行を返します。<br /><br /> -2 を指定すると、セット内の最後から 2 番目の行が返されます (以降、同様に続きます)。<br /><br /> 注: この場合、複数の行をフェッチするように要求すると、結果セットの最後の2行が返されます。|  
  
|*\<nrows>*|設定値|  
|-----------------|------------|  
|開いていない場合|0|  
|キーセットと静的カーソルの場合|通常、現在のキーセットのサイズ。<br /><br /> カーソルが非同期に作成され、この時点までに見つかっ*た行がある場合*は **、-m** 。|  
|動的カーソルの場合|-1|  
  
## <a name="remarks"></a>解説  
  
## <a name="cursor-parameter"></a>cursor パラメーター  
 フェッチ操作が行われる前は、カーソルの既定の位置が結果セットの最初の行の前になります。  
  
## <a name="fetchtype-parameter"></a>fetchtype パラメーター  
 SKIP_UPD_CNCY を除き、 *fetchtype* 値は相互に排他的です。  
  
 SKIP_UPDT_CNCY を指定した場合、行がフェッチまたは更新されるときに timestamp 列の値は keyset テーブルに書き込まれません。 Keyset 行が更新されている場合、timestamp 列の値は前の値のままになります。 行が挿入された場合は timestamp 列の値が未定義になります。  
  
 その結果、KEYSET カーソルでは、keyset テーブルの値が、前回通常の FETCH が実行されたときに設定された値か (通常の FETCH が実行されている場合)、 そうでない場合は、作成時に値が設定されます。  
  
 動的カーソルの場合は、更新を使用してスキップを実行すると、キーセットと同じ結果が生成されることを意味します。 その他のフェッチの種類では、keyset テーブルは切り捨てられます。 これは、行が挿入されており、timestamp 列の値が定義されていないことを意味します。 このため、DYNAMIC カーソルで sp_cursorfetch を実行する際には、REFRESH 以外の操作に対して SKIP_UPDT_CNCY を使用しないようにしてください。  
  
 要求したカーソル位置が結果セットの範囲を超えていたためにフェッチ操作が失敗した場合は、カーソル位置が最後の行の直後に設定されます。 要求したカーソル位置が結果セットより前だったためにフェッチ操作が失敗した場合は、カーソル位置が最初の行の前に設定されます。  
  
## <a name="rownum-parameter"></a>rownum パラメーター  
 *Rownum*を使用すると、指定された行からバッファーがいっぱいになります。  
  
 *Fetchtype*値 ABSOLUTE は、結果セット全体における*rownum*の位置を表します。 負の値を絶対値に指定すると、操作は結果セットの末尾から行をカウントします。  
  
 *Fetchtype*値相対は、現在のバッファーの先頭にあるカーソルの位置に関連する*rownum*の位置を示します。 相対値を持つ負の値は、カーソルが現在のカーソル位置から戻ることを指定します。  
  
## <a name="nrows-parameter"></a>nrows パラメーター  
 *Fetchtype*値の更新と情報は、このパラメーターを無視します。  
  
 *Fetchtype*値の最初の値を指定すると、 *nrow*値が0の場合、カーソルは、フェッチバッファー内の行を持たない結果セットの前に配置されます。  
  
 *Fetchtype*の値を指定すると、最後の*行の n 行*の値が0の場合、カーソルは、現在のフェッチバッファー内の行を持たない結果セットの後に配置されます。  
  
 *Fetchtype*値 NEXT、PREV、ABSOLUTE、相対、および PREV_NOADJUST の場合、 *n 行*の値0は無効です。  
  
## <a name="rpc-considerations"></a>RPC に関する考慮事項  
 RPC の戻りステータスでは、キーセット サイズのパラメーターが final かどうか (keyset テーブル (一時テーブル) が非同期に作成されるかどうか) が示されます。  
  
 RPC 状態パラメーターは、次の表に示すいずれかの値に設定されています。  
  
|[値]|説明|  
|-----------|-----------------|  
|0|プロシージャが正常に実行されました。|  
|0x0001|プロシージャが失敗しました。|  
|0x0002|負の方向のフェッチにより、カーソル位置が結果セットの先頭に設定されました (論理的には、結果セットの前でフェッチが行われるはずでした)。|  
|0x10|高速順方向カーソルが自動的に閉じられました。|  
  
 行は、通常の結果セットとして返されます。つまり、列形式 (0x2a)、rows (0xd1)、done (0xfd) の順に続きます。 メタデータトークンは sp_cursoropen に対して指定されたものと同じ形式で送信されます。これは、SQL Server 7.0 ユーザーの場合は0x81、0xa5、および0xa5 です。 行の状態インジケーターは、ブラウズ モードのように、各行の末尾の非表示の列として送信されます (列名は rowstat、データ型は INT4)。 この rowstat 列には、次のいずれかの値が含まれます。  
  
|[値]|説明|  
|-----------|-----------------|  
|0x0001|FETCH_SUCCEEDED|  
|0x0002|FETCH_MISSING|  
  
 TDS プロトコルでは、前の列を送信せずに末尾の状態列だけを送信することはできないため、欠けている行に対してはダミー データが送信されます (NULL 値許容フィールドは NULL に設定され、固定長フィールドは 0、空白、または列の既定値に設定されます)。  
  
 DONE rowcount は常に0になります。 DONE メッセージに結果セットの実際の行数が含まれます。TDS メッセージの間にエラー メッセージや情報メッセージが表示される場合もあります。  
  
 TDS ストリームでカーソルの選択リストに関するメタデータを返すように要求するには、RPC RETURN_METADATA 入力フラグを1に設定します。  
  
## <a name="examples"></a>例  
  
### <a name="a-using-prev-to-change-a-cursor-position"></a>A. PREV を使用してカーソル位置を変更する  
 カーソル h2 が、次の内容を含む結果セットを生成するとします。  
  
```  
row 1 contents      
row 2 contents  
row 3 contents  
row 4 contents  <-- current position  
row 5 contents   
row 6 contents  
```  
  
 次に、 *nrows* 値が5の前の sp_cursorfetch では、カーソルが結果セットの最初の行の2行前に論理的に配置されます。 このような場合、カーソルが最初の行で開始されるように調整されて、要求した数の行が返されます。 その結果、通常は、前のフェッチ バッファーに含まれていた行が返されることになります。  
  
> [!NOTE]  
>  これは、RPC 状態パラメーターが2に設定されている完全なケースです。  
  
### <a name="b-using-prev_noadjust-to-return-fewer-rows-than-prev"></a>B. PREV_NOADJUST を使用して、PREV よりも小さい行数を返す  
 PREV_NOADJUST は、返された行のブロック内の現在のカーソル位置の行またはその後の行は一切含まれません。 PREV が現在の位置より後の行を返す場合、PREV_NOADJUST は *nrows*で要求された数よりも多くの行を返します。 たとえば、前の例 A の現在位置で PREV を適用した場合、sp_cursorfetch(h2, 4, 1, 5) で次の行がフェッチされます。  
  
```  
row1 contents   
row2 contents  
row3 contents  
row4 contents  
row5 contents  
```  
  
 一方、PREV_NOADJUST を適用した場合は、sp_cursorfetch(h2, 512, 6, 5) で次の行のみがフェッチされます。  
  
```  
row1 contents   
row2 contents  
row3 contents   
```  
  
## <a name="see-also"></a>参照  
 [sp_cursoropen &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
