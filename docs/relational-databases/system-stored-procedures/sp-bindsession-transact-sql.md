---
description: sp_bindsession (Transact-sql)
title: sp_bindsession (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_bindsession
- sp_bindsession_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_bindsession
ms.assetid: 1436fe21-ad00-4a98-aca1-1451a5e571d2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 900f6383a4a285cac36262096a66e64603467c79
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548234"
---
# <a name="sp_bindsession-transact-sql"></a>sp_bindsession (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  セッションをの同じインスタンス内の他のセッションにバインドまたはバインド解除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] します。 バインドセッションを使用すると、2つ以上のセッションを同じトランザクションに参加させ、ROLLBACK TRANSACTION または COMMIT TRANSACTION が実行されるまで、そのロックを共有できます。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]代わりに、複数のアクティブな結果セット (MARS) または分散トランザクションを使用してください。 詳細については、「[複数のアクティブな結果セット &#40;MARS&#41; の使用](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)」を参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_bindsession { 'bind_token' | NULL }  
```  
  
## <a name="arguments"></a>引数  
 **'** *bind_token* **'**  
 **Sp_getbindtoken**または Open Data Services **srv_getbindtoken**関数を使用して最初に取得したトランザクションを識別するトークンです。 *bind_token*は **varchar (255)** です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="remarks"></a>解説  
 バインドされている2つのセッションは、トランザクションとロックのみを共有します。 各セッションは独自の分離レベルを保持し、1つのセッションで新しい分離レベルを設定しても、もう一方のセッションの分離レベルには影響しません。 各セッションは、そのセキュリティアカウントによって識別され、アカウントにアクセス許可が付与されているデータベースリソースにのみアクセスできます。  
  
 **sp_bindsession** は、バインドトークンを使用して、2つ以上の既存のクライアントセッションをバインドします。 これらのクライアントセッションは、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] バインドトークンが取得されたの同じインスタンス上にある必要があります。 セッションとは、コマンドを実行するクライアントです。 バインドされたデータベースセッションは、トランザクションとロック領域を共有します。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の 1 つのインスタンスから取得したバインド トークンは、DTC トランザクションの場合でも、別のインスタンスに接続するクライアント セッションには使用できません。 バインドトークンは、各インスタンス内でのみローカルに有効であり、複数のインスタンス間で共有することはできません。 の別のインスタンスでクライアントセッションをバインドするには [!INCLUDE[ssDE](../../includes/ssde-md.md)] 、 **sp_getbindtoken**を実行して別のバインドトークンを取得する必要があります。  
  
 アクティブでないトークンが使用されている場合、 **sp_bindsession**はエラーで失敗します。  
  
 *Bind_token*を指定せずに**sp_bindsession**を使用するか*bind_token*で NULL を渡すことによって、セッションからバインドを解除します。  
  
## <a name="permissions"></a>アクセス許可  
 ロール **public** のメンバーシップが必要です。  
  
## <a name="examples"></a>例  
 次の例では、指定したバインドトークンを現在のセッションにバインドします。  
  
> [!NOTE]  
>  この例に示されているバインドトークンは、 **sp_bindsession**を実行する前に**sp_getbindtoken**を実行することによって取得されました。  
  
```  
USE master;  
GO  
EXEC sp_bindsession 'BP9---5---->KB?-V'<>1E:H-7U-]ANZ';  
GO  
```  
  
## <a name="see-also"></a>参照  
 [sp_getbindtoken &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql.md)   
 [srv_getbindtoken &#40;拡張ストアドプロシージャ API&#41;](../../relational-databases/extended-stored-procedures-reference/srv-getbindtoken-extended-stored-procedure-api.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
