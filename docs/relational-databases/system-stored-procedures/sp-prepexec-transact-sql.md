---
description: sp_prepexec (Transact-sql)
title: sp_prepexec (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_prepexec
- sp_cursor_prepexec_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_prepexec
ms.assetid: f9141850-a62b-43bf-8e46-b2f92b75ca56
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c5df94e84c602e03d5ead3e2ce36a29d5d314791
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535037"
---
# <a name="sp_prepexec-transact-sql"></a>sp_prepexec (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  パラメーター化されたステートメントを準備して実行 [!INCLUDE[tsql](../../includes/tsql-md.md)] します。 sp_prepexec sp_prepare と sp_execute の機能を組み合わせたものです。 このアクションは、ID = 13 によって表形式のデータストリーム (TDS) パケットで呼び出されます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_prepexec handle OUTPUT, params , stmt  
    [ , bound param ] [ ,...n]]  
```  
  
## <a name="arguments"></a>引数  
 *扱え*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]生成された*ハンドル*識別子です。 *handle* は、 **int** 戻り値を持つ必須パラメーターです。  
  
 *params*  
 パラメーター化されたステートメントを指定します。 変数の *params* 定義は、ステートメントのパラメーターマーカーに置き換えられます。 *params* は、 **ntext**、 **nchar**、または **nvarchar** の入力値を呼び出す必須のパラメーターです。 ステートメントがパラメーター化されていない場合は、NULL 値を入力します。  
  
 *stmt*  
 カーソル結果セットを定義します。 *Stmt*パラメーターは必須であり、 **ntext**、 **nchar**、または**nvarchar**の入力値に対してを呼び出します。  
  
 *bound_param*  
 追加パラメーターをオプションで使用することを示します。 *bound_param* は、使用する追加パラメーターを指定するために、任意のデータ型の入力値を呼び出します。  
  
## <a name="examples"></a>例  
 次の例では、単純なステートメントを準備して実行します。  
  
```  
Declare @Out int;  
EXEC sp_prepexec @Out output,   
    N'@P1 nvarchar(128), @P2 nvarchar(100)',  
    N'SELECT database_id, name  
      FROM sys.databases  
      WHERE name=@P1 AND state_desc = @P2',   
          @P1 = 'tempdb', @P2 = 'ONLINE';   
EXEC sp_unprepare @Out;  
```  
  
## <a name="see-also"></a>関連項目  
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_execute &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-execute-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
