---
title: "KEY_GUID (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/06/2017
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
- Key_GUID_TSQL
- Key_GUID
dev_langs: TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], GUIDs
- KEY_GUID function
- GUIDs [SQL Server]
ms.assetid: 9246c7b2-7098-42c4-a222-cbf30267c46a
caps.latest.revision: "20"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 723186a0489186baa1afeda87d53a71c4d303423
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="keyguid-transact-sql"></a>KEY_GUID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  データベースの対称キーの GUID を返します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
Key_GUID( 'Key_Name' )  
```  
  
## <a name="arguments"></a>引数  
 **'** *Key_Name* **'**  
 データベース内の対称キーの名前を指定します。  
  
## <a name="return-types"></a>戻り値の型  
 **uniqueidentifier**  
  
## <a name="remarks"></a>解説  
 キーが作成されたときに ID 値が指定された場合、GUID はその ID 値の MD5 ハッシュです。 ID 値が指定されなかった場合は、サーバーが GUID を生成します。  
  
 キーが一時キーの場合、キー名は番号記号 (#) で始める必要があります。  
  
## <a name="permissions"></a>権限  
 一時キーは、そのキーが作成されたセッションでのみ使用できます。したがって、アクセスに必要な権限はありません。 一時的ではないキーにアクセスするには、呼び出し元がキーに関する権限を持っている必要があり、キーの VIEW 権限が拒否されていないことが必要です。  
  
## <a name="examples"></a>使用例  
 次の例では、`ABerglundKey1` という対称キーの GUID を返します。  
  
```  
SELECT Key_GUID('ABerglundKey1');  
```  
  
## <a name="see-also"></a>参照  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [sys.symmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)   
 [sys.key_encryptions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)  
  
  
