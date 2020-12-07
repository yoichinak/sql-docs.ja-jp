---
description: sp_addextendedproc (Transact-sql)
title: sp_addextendedproc (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addextendedproc_TSQL
- sp_addextendedproc
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addextendedproc
ms.assetid: c0d4b47b-a855-451e-90e5-5fb2d836ebfa
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 4e8c7ffebae9f082a6a579a6cb6643ad2fc44d1b
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548399"
---
# <a name="sp_addextendedproc-transact-sql"></a>sp_addextendedproc (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  新しい拡張ストアドプロシージャの名前をに登録 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] します。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 代わりに [CLR 統合](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_addextendedproc [ @functname = ] 'procedure' ,   
     [ @dllname = ] 'dll'  
```  
  
## <a name="arguments"></a>引数  
`[ @functname = ] 'procedure'` ダイナミックリンクライブラリ (DLL) 内で呼び出す関数の名前を指定します。 *プロシージャ* は **nvarchar (517)**,、既定値はありません。 *必要に* 応じて、owner *. 関数*の形式で所有者名を含めることができます。  
  
`[ @dllname = ] 'dll'` 関数を含む DLL の名前を指定します。 *dll* は **varchar (255)**,、既定値はありません。 DLL の完全なパスを指定することをお勧めします。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 拡張ストアドプロシージャを作成した後は、sp_addextendedproc を使用してに追加する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 **sp_addextendedproc** 詳細については、「 [SQL Server への拡張ストアドプロシージャの追加](../../relational-databases/extended-stored-procedures-programming/adding-an-extended-stored-procedure-to-sql-server.md)」を参照してください。  
  
 このプロシージャは、 **master** データベースでのみ実行できます。 **Master**以外のデータベースから拡張ストアドプロシージャを実行するには、拡張ストアドプロシージャの名前を**master**で修飾します。  
  
 **sp_addextendedproc** によって、新しい拡張ストアドプロシージャの名前がに登録された、 [sys. objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) カタログビューにエントリが追加され [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 また、 [extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) カタログビューにエントリが追加されます。  
  
> [!IMPORTANT]  
>  完全パスで登録されなかった既存の DLL は、[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] へのアップグレード後、機能しなくなります。 この問題を解決するには、 **sp_dropextendedproc** を使用して DLL の登録を解除した後、完全なパスを指定して **sp_addextendedproc**に再登録します。  
  
## <a name="permissions"></a>アクセス許可  
 **Sp_addextendedproc**を実行できるのは、 **sysadmin**固定サーバーロールのメンバーだけです。  
  
## <a name="examples"></a>例  
 次の例では、 **xp_hello** 拡張ストアドプロシージャを追加します。  
  
```  
USE master;  
GO  
EXEC sp_addextendedproc xp_hello, 'c:\xp_hello.dll';  
```  
  
## <a name="see-also"></a>参照  
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
