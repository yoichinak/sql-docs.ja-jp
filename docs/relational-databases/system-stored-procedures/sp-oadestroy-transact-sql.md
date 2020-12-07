---
description: sp_OADestroy (Transact-SQL)
title: sp_OADestroy (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OADestroy_TSQL
- sp_OADestroy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OADestroy
ms.assetid: 0bd1cff4-ceff-4095-9ae4-e1e65a80f5d6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 075218121149528185b4adcddda7393433ff69a0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549582"
---
# <a name="sp_oadestroy-transact-sql"></a>sp_OADestroy (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  作成された OLE オブジェクトを破棄します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_OADestroy objecttoken      
```  
  
## <a name="arguments"></a>引数  
 *objecttoken*  
 以前に **sp_OACreate**を使用して作成された OLE オブジェクトのオブジェクトトークンです。  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または0以外の数 (失敗)。これは、OLE オートメーションオブジェクトによって返される HRESULT の整数値です。  
  
 HRESULT のリターンコードの詳細については、「 [OLE オートメーションのリターンコードとエラー情報](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)」を参照してください。  
  
## <a name="remarks"></a>解説  
 **Sp_OADestroy**が呼び出されていない場合、作成された OLE オブジェクトはバッチの最後に自動的に破棄されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールのメンバーシップ、またはこのストアドプロシージャに対して直接実行権限が必要です。 `Ole Automation Procedures` OLE オートメーションに関連するシステムプロシージャを使用するには、構成を **有効** にする必要があります。  
  
## <a name="examples"></a>例  
 次の例では、以前に作成した **SQLServer** オブジェクトを破棄します。  
  
```  
EXEC @hr = sp_OADestroy @object;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;の OLE オートメーションストアドプロシージャ ](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE オートメーションのサンプル スクリプト](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
