---
description: sp_cursorexecute (Transact-sql)
title: sp_cursorexecute (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorexecute
- sp_cursorexecute_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_execute
ms.assetid: 6a204229-0a53-4617-a57e-93d4afbb71ac
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 07795588a4c1d6df43a7041f9254a661e527be14
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543602"
---
# <a name="sp_cursorexecute-transact-sql"></a>sp_cursorexecute (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  sp_cursorprepare によって作成された実行プランに基づいてカーソルを作成してデータを格納します。 このプロシージャは、sp_cursorprepare と組み合わせて sp_cursoropen と同じ機能を持ちますが、2つのフェーズに分割されています。 sp_cursorexecute は、ID = 4 を指定した場合に表形式のデータストリーム (TDS) パケットで呼び出されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cursorexecute prepared_handle, cursor  
    [ , scrollopt[ OUTPUT ]  
    [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,bound param][,...n]]]]]  
```  
  
## <a name="arguments"></a>引数  
 *prepared_handle*  
 Sp_cursorprepare によって返される、準備されたステートメント *ハンドル* の値を指定します。 *prepared_handle* は、 **int** 入力値を必要とする必須パラメーターです。  
  
 *cursor*  
 SQL Server 生成されたカーソル識別子を示します。 *cursor* は、カーソルに対して動作する後続のすべてのプロシージャ (など) で指定する必要がある必須のパラメーターです sp_cursorfetch  
  
 *scrollopt*  
 スクロール オプションです。 *scrollopt* は、 **int** 入力値を必要とする省略可能なパラメーターです。 Sp_cursorexecute*scrollopt* パラメーターには、sp_cursoropen と同じ値オプションがあります。  
  
> [!NOTE]  
>  PARAMETERIZED_STMT 値はサポートされていません。  
  
> [!IMPORTANT]  
>  *Scrollopt*値が指定されていない場合、既定値は、sp_cursorprepare で指定された*scrollopt*値に関係なく、KEYSET になります。  
  
 *ccopt*  
 通貨制御オプション。 *ccopt* は、 **int 型** の入力値を必要とする省略可能なパラメーターです。 Sp_cursorexecute*ccopt* パラメーターには、sp_cursoropen と同じ値オプションがあります。  
  
> [!IMPORTANT]  
>  *Ccopt*の値が指定されていない場合、sp_cursorprepare で指定された*ccopt*の値に関係なく、既定値はオプティミスティックになります。  
  
 *行*  
 AUTO_FETCH で使用するフェッチバッファー行の数を示す省略可能なパラメーターです。 既定値は20行です。 *rowcount* の動作は、入力値と戻り値として割り当てられた場合に異なります。  
  
|入力値として|戻り値として|  
|--------------------|---------------------|  
|FAST_FORWARD cursor で AUTO_FETCH が指定されている場合、 *rowcount* はフェッチバッファーに格納する行の数を表します。|結果セット内の行の数を表します。 *Scrollopt* AUTO_FETCH 値を指定すると、 *rowcount*はフェッチバッファーにフェッチされた行の数を返します。|  
  
 *bound_param*  
 追加パラメーターをオプションで使用することを示します。  
  
> [!NOTE]  
>  5番目以降のパラメーターは、入力パラメーターとしてステートメントプランに渡されます。  
  
## <a name="code-return-value"></a>コードの戻り値  
 *rowcount* は次の値を返す場合があります。  
  
|[値]|説明|  
|-----------|-----------------|  
|-1|不明な行の数。|  
|-n|非同期設定が有効になっています。|  
  
## <a name="remarks"></a>解説  
  
## <a name="scrollopt-and-ccopt-parameters"></a>scrollopt パラメーターと ccopt パラメーター  
 *scrollopt* と *ccopt* は、キャッシュされたプランがサーバーキャッシュに対して割り込まれる場合に役立ちます。つまり、ステートメントを識別する準備済みハンドルを再コンパイルする必要があります。 *Scrollopt*および*ccopt*パラメーターの値は、元の要求で sp_cursorprepare に送信された値と一致している必要があります。  
  
> [!NOTE]  
>  PARAMETERIZED_STMT を *scrollopt*に割り当てることはできません。  
  
 一致する値を指定しなかった場合、プランの再コンパイルが行われ、準備操作と実行操作が否定されます。  
  
## <a name="rpc-and-tds-considerations"></a>RPC と TDS に関する考慮事項  
 RPC の RETURN_METADATA 入力フラグを 1 に設定すると、カーソル選択リストのメタデータを TDS ストリームで返すように要求できます。  
  
## <a name="see-also"></a>参照  
 [sp_cursoropen &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
