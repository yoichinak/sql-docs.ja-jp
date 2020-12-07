---
description: sp_cursoroption (Transact-sql)
title: sp_cursoroption (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursoroption_TSQL
- sp_cursoroption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoroption
ms.assetid: 88fc1dba-f4cb-47c0-92c2-bf398f4a382e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: bb85ff45fcb9ebe35920ca858cc9dc6336475cb8
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543569"
---
# <a name="sp_cursoroption-transact-sql"></a>sp_cursoroption (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  カーソルオプションを設定するか、sp_cursoropen ストアドプロシージャによって作成されたカーソル情報を返します。 sp_cursoroption は、ID = 8 を指定した場合に表形式のデータストリーム (TDS) パケットで呼び出されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cursoroption cursor, code, value  
```  
  
## <a name="arguments"></a>引数  
 *cursor*  
 は、 *handle*によって生成され、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sp_cursoropen ストアドプロシージャによって返されるハンドル値です。 *カーソル* の実行には **int** 入力値が必要です。  
  
 *code*  
 カーソル戻り値のさまざまな要因を指定するために使用されます。 *コード* には、次のいずれかの **int** 入力値が必要です。  
  
|[値]|名前|説明|  
|-----------|----------|-----------------|  
|0x0001|TEXTPTR_ONLY|指定された特定の text 列または image 列の実際のデータではなくテキスト ポインターを返します。<br /><br /> TEXTPTR_ONLY を使用すると、テキストポインターを blob オブジェクトへの *ハンドル* として使用できるようになり [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。このオブジェクトは、後でまたは dbwritetext など機能 (READTEXT やなど) を使用して選択的に取得または更新することができ [!INCLUDE[tsql](../../includes/tsql-md.md)] ます。<br /><br /> 値 0 が割り当てられている場合は、選択リスト内のすべての text 列および image 列がデータではなくテキスト ポインターを返します。|  
|0x0002|CURSOR_NAME|*Value*で指定された名前をカーソルに割り当てます。 これにより、ODBC では、 [!INCLUDE[tsql](../../includes/tsql-md.md)] sp_cursoropen によって開かれたカーソルに対して位置指定更新/削除ステートメントを使用できます。<br /><br /> 文字列は任意の文字または Unicode データ型として指定できます。<br /><br /> 配置された [!INCLUDE[tsql](../../includes/tsql-md.md)] update/delete ステートメントは、既定では fat カーソルの最初の行で動作するため、位置指定の update/delete ステートメントを実行する前に、SP_CURSOR SETPOSITION を使用してカーソルを配置する必要があります。|  
|0x0003|TEXTDATA|以降のフェッチで、特定の text 列または image 列のテキスト ポインターではなく実際のデータを返します (これにより、TEXTPTR_ONLY の効力が取り消されます)。<br /><br /> 特定の列で TEXTDATA が有効になると、行は再フェッチ (更新) されます。後で TEXTPTR_ONLY に戻すことができます。 TEXTPTR_ONLY と同様に、value パラメーターは列番号を指定する整数で、値が 0 の場合はすべての text 列および image 列が返されます。|  
|0x0004|SCROLLOPT|スクロール オプションです。 詳細については、このトピックで後述する「返されるコード値」を参照してください。|  
|0x0005|CCOPT|同時実行制御オプション。 詳細については、このトピックで後述する「返されるコード値」を参照してください。|  
|0x0006|ROWCOUNT|結果セットに現在含まれている行の数。<br /><br /> 注: sp_cursoropen によって返された値から、非同期の作成が使用されている場合、行数が変更された可能性があります。 行の数が不明な場合は、値-1 が返されます。|  
  
 *value*  
 *コード*によって返される値を指定します。 *value* は、0x0001、0x0002、または0x0003 の *コード* 入力値を呼び出す必須パラメーターです。  
  
> [!NOTE]  
>  *コード*値2は文字列データ型です。 その他の *コード* 値の入力または値によって返される *値* は整数です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 *Value*パラメーターは、次のいずれかの*コード*値を返す場合があります。  
  
|戻り値|説明|  
|------------------|-----------------|  
|0x0004|SCROLLOPT|  
|0X0005|CCOPT|  
|0X0006|ROWCOUNT|  
  
 *Value*パラメーターは、次のいずれかの SCROLLOPT 値を返します。  
  
|戻り値|説明|  
|------------------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
  
 *Value*パラメーターは、次のいずれかの CCOPT 値を返します。  
  
|戻り値|説明|  
|------------------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS|  
|0x0004 または0x0008|OPTIMISTIC|  
  
## <a name="see-also"></a>参照  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cursor &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursor-transact-sql.md)   
 [sp_cursoropen &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
  
  
