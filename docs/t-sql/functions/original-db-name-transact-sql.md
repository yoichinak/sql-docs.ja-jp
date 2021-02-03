---
description: ORIGINAL_DB_NAME (Transact-SQL)
title: ORIGINAL_DB_NAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: reference
f1_keywords:
- ORIGINAL_DB_NAME
- ORIGINAL_DB_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ORIGINAL_DB_NAME function
ms.assetid: 7dadc40a-1287-4f31-8487-434ee477144d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6d84ffff979de59fae34a204e3a87ca8619ca17b
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99200561"
---
# <a name="original_db_name-transact-sql"></a>ORIGINAL_DB_NAME (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  ユーザーがデータベース接続文字列で指定したデータベース名を返します。 このデータベースは、**sqlcmd-d** オプション (USE *database*) を使用して指定します。 Open Database Connectivity (ODBC) のデータ ソース式を使用して指定することもできます (initial catalog =*databasename*)。  
  
 このデータベースは、既定のユーザー データベースとは異なります。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```syntaxsql
ORIGINAL_DB_NAME ()  
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>解説  
 初期データベースが指定されていない場合、この関数は空文字列を返します。  
  
## <a name="see-also"></a>参照  
 [sqlcmd ユーティリティ](../../tools/sqlcmd-utility.md)   
 [osql ユーティリティ](../../tools/osql-utility.md)   
 [SQL Server Native Client (ODBC)](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
