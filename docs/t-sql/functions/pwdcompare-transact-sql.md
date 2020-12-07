---
description: PWDCOMPARE (Transact-SQL)
title: PWDCOMPARE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PWDCOMPARE
- PWDCOMPARE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sa account
- passwords [SQL Server], blank
- PWDCOMPARE function [Transact-SQL]
ms.assetid: 5f84ff9e-c1ec-46aa-8501-50f854ebcc3a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 38c35f039701d68eddfee86f4fb558a3689033d8
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/26/2020
ms.locfileid: "91380719"
---
# <a name="pwdcompare-transact-sql"></a>PWDCOMPARE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  パスワードをハッシュし、そのハッシュを既存のパスワードのハッシュと比較します。 PWDCOMPARE を使用すると、空白の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン パスワードや、よくある脆弱なパスワードを検索できます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
PWDCOMPARE ( 'clear_text_password'  
   , password_hash   
   [ , version ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 **'** *clear_text_password* **'**  
 暗号化されていないパスワードです。 *clear_text_password* is **sysname** (**nvarchar(128)**).  
  
 *password_hash*  
 パスワードの暗号化ハッシュです。 *password_hash* が **varbinary (128)** です。  
  
 *version*  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以降に移行されたが [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] システムには変換されていない [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 以前のログインからの値を *password_hash* が表している場合に、1 に設定される可能性がある、古いパラメーターです。 *バージョン* は **int** です。  
  
> [!CAUTION]  
>  このパラメーターは旧バージョンとの互換性を維持するために提供されていますが、パスワード ハッシュ BLOB は独自のバージョンの説明を含んでいるため、無視されます。 [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)]  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
 場合 1 を返しますのハッシュ、*clear_text_password* と一致する、 *password_hash* パラメーター、および、そうでない場合は 0 です。  
  
## <a name="remarks"></a>注釈  
 PWDCOMPARE 関数は、パスワード ハッシュの強度に対する脅威にはなりません。このテストは、最初のパラメーターとして渡されるパスワードを使用してログインしようとした場合に実行されるテストと同じテストです。  
  
 **PWDCOMPARE** 包含データベース ユーザーのパスワードを使用することはできません。 包含データベースに相当するものがありません。  
  
## <a name="permissions"></a>アクセス許可  
 PWDENCRYPT はパブリックに使用できます。  
  
 sys.sql_logins の password_hash 列を調べるには CONTROL SERVER 権限が必要です。  
  
## <a name="examples"></a>例  
  
### <a name="a-identifying-logins-that-have-no-passwords"></a>A. パスワードがないログインを特定する  
 次の例では、パスワードがない [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを特定します。  
  
```sql  
SELECT name FROM sys.sql_logins   
WHERE PWDCOMPARE('', password_hash) = 1 ;  
```  
  
### <a name="b-searching-for-common-passwords"></a>B. よくあるパスワードを検索する  
 よくあるパスワードを見つけて変更できるように検索するには、そのパスワードを最初のパラメーターとして指定します。 たとえば、次のステートメントを実行すると、`password` として指定されているパスワードが検索されます。  
  
```sql  
SELECT name FROM sys.sql_logins   
WHERE PWDCOMPARE('password', password_hash) = 1 ;  
```  
  
## <a name="see-also"></a>関連項目  
 [PWDENCRYPT &#40;Transact-SQL&#41;](../../t-sql/functions/pwdencrypt-transact-sql.md)   
 [セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
