---
description: sp_cursorprepare (Transact-sql)
title: sp_cursorprepare (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepare_TSQL
- sp_cursor_prepare
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor_prepare
ms.assetid: 6207e110-f4bf-4139-b3ec-b799c9cb3ad7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3418727f21a0132390a1c1334919b2be6dc36965
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539032"
---
# <a name="sp_cursorprepare-transact-sql"></a>sp_cursorprepare (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  カーソル ステートメントまたはバッチをコンパイルして実行プランを作成します。カーソルは作成しません。 コンパイルされたステートメントは、後で sp_cursorexecute で使用できます。 このプロシージャは、sp_cursorexecute と組み合わせて sp_cursoropen と同じ機能を持ちますが、2つのフェーズに分割されています。 sp_cursorprepare は、ID = 3 を指定した場合に表形式のデータストリーム (TDS) パケットで呼び出されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cursorprepare prepared_handle OUTPUT, params , stmt , options  
    [ , scrollopt[ , ccopt]]  
```  
  
## <a name="arguments"></a>引数  
 *prepared_handle*  
 整数値を返す、SQL Server によって生成される準備済み *ハンドル* 識別子。  
  
> [!NOTE]  
>  その後、カーソルを開くために、 *prepared_handle*が sp_cursorexecute プロシージャに渡されます。 作成されたハンドルは、ログオフするか sp_cursorunprepare プロシージャを使用して明示的に削除するまで存在します。  
  
 *params*  
 パラメーター化されたステートメントを指定します。 変数の *params* 定義は、ステートメントのパラメーターマーカーに置き換えられます。 *params* は、 **ntext**、 **nchar**、または **nvarchar** の入力値を呼び出す必須のパラメーターです。 ステートメントがパラメーター化されていない場合は、NULL 値を入力します。  
  
> [!NOTE]  
>  *Stmt*がパラメーター化され、 *scrollopt* PARAMETERIZED_STMT 値が ON の場合、入力値として**ntext**文字列を使用します。  
  
 *stmt*  
 カーソル結果セットを定義します。 *Stmt*パラメーターが必要であり、 **ntext**、 **nchar** 、または**nvarchar**の入力値に対してを呼び出します。  
  
> [!NOTE]  
>  *Stmt*値を指定するためのルールは、sp_cursoropen の場合と同じですが、 *stmt* string データ型は**ntext**である必要があります。  
  
 *options*  
 カーソル結果セット列の説明を返す省略可能なパラメーターです。 *オプション* には、次の **int** 入力値が必要です。  
  
|[値]|説明|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 スクロールオプション。 *scrollopt* は省略可能なパラメーターで、次のいずれかの **int** 入力値を必要とします。  
  
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
  
 要求された値は、 *stmt*によって定義されたカーソルに適していない場合があるため、このパラメーターは入力と出力の両方として機能します。 このような場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって適切な値が割り当てられます。  
  
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
  
 *同様 scrollpt,* と同様に、では、要求されたものとは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 異なる値を割り当てることができます。  
  
## <a name="remarks"></a>解説  
 RPC 状態パラメーターは、次のいずれかになります。  
  
|[値]|説明|  
|-----------|-----------------|  
|0|成功|  
|0x0001|障害|  
|1FF6|メタデータを返せませんでした。<br /><br /> 注: これは、ステートメントによって結果セットが生成されないためです。たとえば、INSERT ステートメントや DDL ステートメントなどです。|  
  
## <a name="examples"></a>例  
  Sp_cursorprepare と sp_cursorexecute の使用例を次に示します。

```sql
declare @handle int , @p5 int, @p6 int
exec sp_cursorprepare @handle OUTPUT, 
    N'@dbid int', 
    N'select * from sys.databases where database_id < @dbid',
    1,
    @p5 output,
    @p6 output


declare @p1 int  
set @P1 = @handle 
declare @p2 int   
declare @p3 int  
declare @p4 int  
set @P6 = 4 
exec sp_cursorexecute @p1, @p2 OUTPUT, @p3 output , @p4 output, @p5 OUTPUT, @p6

exec sp_cursorfetch @P2

exec sp_cursorunprepare @handle
exec sp_cursorclose @p2
```
 
 *Stmt*がパラメーター化され、 *scrollopt* PARAMETERIZED_STMT 値が ON の場合、文字列の形式は次のようになります。  
  
 { *\<local variable name>**\<data type>* } [ ,...*n* ]  
  
## <a name="see-also"></a>参照  
 [sp_cursorexecute &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursoropen &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorunprepare &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorunprepare-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
