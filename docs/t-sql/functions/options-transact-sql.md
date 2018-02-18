---
title: "@@OPTIONS (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@OPTIONS'
- '@@OPTIONS_TSQL'
dev_langs: TSQL
helpviewer_keywords:
- SET statement, current SET options
- '@@OPTIONS function'
- current SET options
ms.assetid: 3d5c7f6e-157b-4231-bbb4-4645a11078b3
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 75919b6d27b2a81a9aba3575d3a9f3c54f0e0850
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="x40x40options-transact-sql"></a>&#x40;&#x40;OPTIONS (TRANSACT-SQL)。
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  現在の SET オプションに関する情報を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
@@OPTIONS  
```  
  
## <a name="return-types"></a>戻り値の型  
 **integer**  
  
## <a name="remarks"></a>解説  
 オプションは **SET** コマンドまたは **sp_configure user options** 値の使用により発生します。 **SET** コマンドを使用して構成されたセッション値は **sp_configure** オプションをオーバーライドします。 多くのツール ([!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] など) はセット オプションを自動的に構成します。 各ユーザーには、構成を表す @@OPTIONS 関数が用意されます。  
  
 SET ステートメントを使用することにより、特定のユーザー セッションの言語とクエリ処理オプションを変更できます。 **@@OPTIONS** は ON または OFF に設定されるオプションのみを検出できます。  
  
 **@@OPTIONS** 関数は、オプションのビットマップをベース 10 (10 進数) の整数に変換して返します。 ビット設定はトピック「[user options サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)」で説明している場所に格納されます。  
  
 **@@OPTIONS** 値をデコードするには、 **@@OPTIONS** によって返される整数をバイナリに変換し、「[user options サーバー構成構成オプション](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)」のテーブルで値を検索します。 たとえば、`SELECT @@OPTIONS;` が値 `5496` を返す場合、Windows のプログラマ電卓 (**calc.exe**) を使用して、10 進数の `5496` をバイナリに変換します。 結果は `1010101111000` です。 左端の文字 (バイナリ 1、2、および 4) は 0 で、**IMPLICIT_TRANSACTIONS** および **CURSOR_CLOSE_ON_COMMIT** がオフであることを示します。 次の項目 (`1000` 位置の **ANSI_WARNINGS**) はオンです。 ビットマップで右方向に、オプションの一覧で下方向に、作業を続けます。 右端のオプションが 0 の場合、型変換により切り捨てられます。 ビットマップ `1010101111000` は実際には `001010101111000` で、15 のすべてのオプションを表します。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-demonstration-of-how-changes-affect-behavior"></a>A. 変更が動作に与える影響の例  
 以下の例は、**CONCAT_NULL_YIELDS_NULL** オプションの 2 つの異なる設定による、連結動作における違いを示しています。  
  
```  
SELECT @@OPTIONS AS OriginalOptionsValue;  
SET CONCAT_NULL_YIELDS_NULL OFF;  
SELECT 'abc' + NULL AS ResultWhen_OFF, @@OPTIONS AS OptionsValueWhen_OFF;  
  
SET CONCAT_NULL_YIELDS_NULL ON;  
SELECT 'abc' + NULL AS ResultWhen_ON, @@OPTIONS AS OptionsValueWhen_ON;  
```  
  
### <a name="b-testing-a-client-nocount-setting"></a>B. クライアントの NOCOUNT 設定のテスト  
 次の例では、`NOCOUNT ON` を設定し、`@@OPTIONS` の値を調べます。 `NOCOUNT ON` オプションは、セッションで実行するすべてのステートメントごとに、要求するクライアントに対して影響を受ける行数に関するメッセージを戻さないようにします。 `@@OPTIONS` の値は、`512` (0x0200) に設定されます。 これは `NOCOUNT` オプションを表します。 この例では、クライアントで NOCOUNT オプションが有効になっているかどうかを調べます。 たとえば、これはクライアントにおけるパフォーマンスの違いを調べるのに役立ちます。  
  
```  
SET NOCOUNT ON  
IF @@OPTIONS & 512 > 0   
RAISERROR ('Current user has SET NOCOUNT turned on.', 1, 1)  
```  
  
## <a name="see-also"></a>参照  
 [構成関数 &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [user options サーバー構成オプションの構成](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)  
  
  
