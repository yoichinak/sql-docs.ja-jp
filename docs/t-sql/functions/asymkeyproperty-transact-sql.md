---
title: "ASYMKEYPROPERTY (TRANSACT-SQL) |Microsoft ドキュメント"
ms.custom: 
ms.date: 07/24/2017
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
- ASYMKEYPROPERTY_TSQL
- ASYMKEYPROPERTY
dev_langs: TSQL
helpviewer_keywords: ASYMKEYPROPERTY
ms.assetid: a30581f2-e1b1-4996-93e6-527ff96b7c42
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 808f7c8d840f18d9e09fe9906e366fb7feb76cff
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2017
---
# <a name="asymkeyproperty-transact-sql"></a>ASYMKEYPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

非対称キーのプロパティを返します。
  
![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>構文  
  
```sql
ASYMKEYPROPERTY (Key_ID , 'algorithm_desc' | 'string_sid' | 'sid')  
```  
  
## <a name="arguments"></a>引数  
*Key_id*  
データベース内の非対称キーの Key_ID を指定します。 キー名しかわからない場合に Key_ID を調べるには、ASYMKEY_ID を使用します。 *Key_ID*のデータ型は **int**です。
  
**'**algorithm_desc**'**  
出力が非対称キーのアルゴリズムの説明を返すように指定します。 EKM モジュールから作成された非対称キーに対してのみ使用できます。
  
**'**string_sid**'**  
出力が非対称キーの SID を **nvarchar()** 形式で返すように指定します。
  
**'**sid**'**  
出力が非対称キーの SID をバイナリ形式で返すように指定します。
  
## <a name="return-types"></a>戻り値の型  
**sql_variant**
  
## <a name="permissions"></a>権限  
非対称キーに対する権限が必要です。呼び出し元で、非対称キーに対する VIEW 権限が拒否されていないことも必要になります。
  
## <a name="examples"></a>使用例  
次の例では、Key_ID が 256 の非対称キーのプロパティを返します。
  
```sql
SELECT   
ASYMKEYPROPERTY(256, 'algorithm_desc') AS Algorithm,  
ASYMKEYPROPERTY(256, 'string_sid') AS String_SID,  
ASYMKEYPROPERTY(256, 'sid') AS SID ;  
GO  
```  
  
## <a name="see-also"></a>参照
[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
[ALTER ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)  
[DROP ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)  
[SIGNBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)  
[VERIFYSIGNEDBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)  
[暗号化階層](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[sys.asymmetric_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md)  
[セキュリティ カタログ ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
[ASYMKEY_ID &#40;Transact-SQL&#41;](../../t-sql/functions/asymkey-id-transact-sql.md)  
[SYMKEYPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/symkeyproperty-transact-sql.md)
  
  
