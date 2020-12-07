---
description: sp_dbcmptlevel (Transact-sql)
title: sp_dbcmptlevel (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbcmptlevel
- sp_dbcmptlevel_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbcmptlevel
ms.assetid: 508c686d-2bd4-41ba-8602-48ebca266659
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2c03d436a85e174e1af17e47c8dc27d3ad2d6976
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541923"
---
# <a name="sp_dbcmptlevel-transact-sql"></a>sp_dbcmptlevel (Transact-sql)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  データベースの特定の動作に、指定したバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] との互換性を設定します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] 代わりに [ALTER Database 互換性レベル](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)を使用してください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_dbcmptlevel [ [ @dbname = ] name ]   
    [ , [ @new_cmptlevel = ] version ]  
```  
  
## <a name="arguments"></a>引数  
`[ @dbname = ] name` 互換性レベルを変更するデータベースの名前を指定します。 データベース名は、識別子の規則に従っている必要があります。 *名前* は **sysname**,、既定値は NULL です。  
  
`[ @new_cmptlevel = ] version` データベースに互換性を持たせるのバージョンを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 指定します。 *version* は **tinyint**,、既定値は NULL です。 値は、次のいずれかである必要があります。  
  
 **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
 **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
 **110** = [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
 **120** = [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 **130** = [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]  
  
## <a name="return-code-values"></a>リターン コードの値  
 0 (成功) または 1 (失敗)  
  
## <a name="result-sets"></a>結果セット  
 パラメーターが指定されていない場合、または *name* パラメーターが指定されていない場合、 **sp_dbcmptlevel** はエラーを返します。  
  
 *Name*が指定されて*いない場合、は*、指定された [!INCLUDE[ssDE](../../includes/ssde-md.md)] データベースの現在の互換性レベルを表示するメッセージを返します。  
  
## <a name="remarks"></a>解説  
 互換性レベルの詳細については、「 [ALTER Database Compatibility Level &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)」を参照してください。  
  
## <a name="permissions"></a>アクセス許可  
 このプロシージャを実行できるのは、データベース所有者、固定サーバーロール **sysadmin** のメンバー、および **db_owner** 固定データベースロール (現在のデータベースを変更している場合) だけです。  
  
## <a name="see-also"></a>参照  
 [Transact-sql&#41;&#40;のストアドプロシージャのデータベースエンジン ](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [予約済みキーワード &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
