---
description: PWDENCRYPT (Transact-SQL)
title: PWDENCRYPT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- PWDENCRYPT
- PWDENCRYPT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PWDENCRYPT function [Transact-SQL]
ms.assetid: 333e9a43-1099-4b9b-b941-4b0b016f47f3
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2bc5c778ea6dc591099538b974bf71f4d85c4f0a
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99182355"
---
# <a name="pwdencrypt-transact-sql"></a>PWDENCRYPT (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  現在のバージョンのパスワード ハッシュ アルゴリズムを使用して、入力値の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パスワード ハッシュを返します。  
  
 PWDENCRYPT は古い関数であり、将来の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リリースではサポートされない可能性があります。 代わりに、[HASHBYTES](../../t-sql/functions/hashbytes-transact-sql.md) を使用します。 HASHBYTES にはさらに多くのハッシュ アルゴリズムが用意されています。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
PWDENCRYPT ( 'password' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>引数
 *password*  
 暗号化されるパスワードです。 *パスワード* は **sysname** です。  
  
## <a name="return-types"></a>戻り値の型  
 **varbinary (128)**  
  
## <a name="permissions"></a>アクセス許可  
 PWDENCRYPT はパブリックに使用できます。  
  
## <a name="see-also"></a>参照  
 [セキュリティ関数 &#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)   
 [PWDCOMPARE &#40;Transact-SQL&#41;](../../t-sql/functions/pwdcompare-transact-sql.md)  
  
  
