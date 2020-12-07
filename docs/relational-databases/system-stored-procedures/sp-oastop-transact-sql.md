---
description: sp_OAStop (Transact-SQL)
title: sp_OAStop (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAStop
- sp_OAStop_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAStop
ms.assetid: aa9eab66-c4f7-4ec7-9f0d-5d24d16da654
author: markingmyname
ms.author: maghan
ms.openlocfilehash: d30bd1bfc143f18f67465b2d1ec71f7c4c97a9d2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89534923"
---
# <a name="sp_oastop-transact-sql"></a>sp_OAStop (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  サーバー全体の OLE オートメーションストアドプロシージャの実行環境を停止します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_OAStop      
```  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または0以外の数 (失敗)。これは、OLE オートメーションオブジェクトによって返される HRESULT の整数値です。  
  
 HRESULT のリターンコードの詳細については、「 [OLE オートメーションのリターンコードとエラー情報](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)」を参照してください。  
  
## <a name="remarks"></a>解説  
 1つの実行環境は、OLE オートメーションストアドプロシージャを使用するすべてのクライアントによって共有されます。 1つのクライアントがを呼び出すと **sp_OAStop** すべてのクライアントに対して共有実行環境が停止します。 実行環境が停止した後、 **sp_OACreate** を呼び出すと、実行環境が再起動されます。  
  
## <a name="permissions"></a>アクセス許可  
 **Sysadmin**固定サーバーロールのメンバーシップ、またはこのストアドプロシージャに対して直接実行権限が必要です。 `Ole Automation Procedures` OLE オートメーションに関連するシステムプロシージャを使用するには、構成を **有効** にする必要があります。  
  
## <a name="examples"></a>例  
 次の例では、共有 OLE オートメーション実行環境を停止します。  
  
```  
EXEC sp_OAStop;  
GO  
```  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;の OLE オートメーションストアドプロシージャ ](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE オートメーションのサンプル スクリプト](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
