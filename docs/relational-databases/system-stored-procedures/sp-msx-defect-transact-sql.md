---
description: sp_msx_defect (Transact-SQL)
title: sp_msx_defect (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_msx_defect
- sp_msx_defect_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_msx_defect
ms.assetid: 0dfd963a-3bc5-4b58-94f7-aec976da2883
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a1b5ea1139e0cfc1b27d7b79df29e6c1b1381b4d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541550"
---
# <a name="sp_msx_defect-transact-sql"></a>sp_msx_defect (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  マルチサーバー操作から現在のサーバーを削除します。  
  
> [!CAUTION]  
>  **sp_msx_defect** によってレジストリが編集されます。 レジストリは手動で編集しないでください。不適切または不正確な変更を加えると、システム構成に重大な問題が生じる場合があります。 熟練したユーザーのみがレジストリ エディターを使用してレジストリを編集することをお勧めします。 詳細については、Microsoft Windows のドキュメントを参照してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_msx_defect [@forced_defection =] forced_defection  
```  
  
## <a name="arguments"></a>引数  
`[ @forced_defection = ] forced_defection` 致命的が破損した **msdb** データベースによって、または **msdb** データベースのバックアップが存在しないことが原因で、マスター SQLServerAgent が完全に失われた場合に、強制的に参加を解除するかどうかを指定します。 *forced_defection*の部分は **ビット**で、既定値は **0**です。これは、強制的な参加解除が行われないことを示します。 値が **1** の場合は強制的に参加を解除します。  
  
 **Sp_msx_defect**を実行して参加解除を強制した後、マスター SQLServerAgent の**sysadmin**固定サーバーロールのメンバーは、次のコマンドを実行して参加解除を完了する必要があります。  
  
```  
EXECUTE msdb.dbo.sp_delete_targetserver @server_name = 'tsx-server', @post_defection =  0;  
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 **0** (成功) または **1** (失敗)  
  
## <a name="result-sets"></a>結果セット  
 なし  
  
## <a name="remarks"></a>解説  
 **Sp_msx_defect**適切に完了すると、メッセージが返されます。  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャを実行するには、 **sysadmin** 固定サーバー ロールのメンバーであることが必要です。  
  
## <a name="see-also"></a>参照  
 [sp_msx_enlist &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
