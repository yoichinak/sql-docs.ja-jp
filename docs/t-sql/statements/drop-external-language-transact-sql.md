---
description: DROP EXTERNAL LANGUAGE (Transact-SQL) - SQL Server
title: DROP EXTERNAL LANGUAGE (Transact-SQL) - SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2019
ms.prod: sql
ms.technology: language-extensions
ms.topic: language-reference
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3eff9057307d06874237ccda6cb1f1ace518339d
ms.sourcegitcommit: 197a6ffb643f93592edf9e90b04810a18be61133
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2020
ms.locfileid: "91378177"
---
# <a name="drop-external-language-transact-sql"></a>DROP EXTERNAL LANGUAGE (Transact-SQL)  
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

既存の外部言語を削除します。

## <a name="syntax"></a>構文

```syntaxsql
DROP EXTERNAL LANGUAGE <language_name>
```

### <a name="arguments"></a>引数

**language_name**

言語は、データベース スコープのオブジェクトです。 言語名は、データベース内で一意であることが必要です。

## <a name="permissions"></a>アクセス許可

言語を削除するには、ALTER ANY EXTERNAL LANGUAGE の特権が必要です。 既定では、すべてのデータベース所有者またはオブジェクトの所有者も、外部言語を削除することができます。

> [!NOTE]
> 外部言語を削除する前に、その外部言語を参照している外部ライブラリを削除する必要があることに注意してください。

### <a name="return-values"></a>戻り値

ステートメントが成功した場合は、情報メッセージが返されます。

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="remarks"></a>解説

外部言語を削除するには、その前に、指定した言語に対するすべての外部ライブラリを削除する必要があります。

## <a name="examples"></a>例

外部言語 **Java** を作成します。

```sql
CREATE EXTERNAL LANGUAGE Java 
FROM (CONTENT = N'<path-to-zip>', FILE_NAME = 'javaextension.dll');
GO
```

外部言語を削除します。

```sql
DROP EXTERNAL LANGUAGE Java;
```

## <a name="see-also"></a>参照

[CREATE EXTERNAL LANGUAGE (Transact-SQL)](create-external-language-transact-sql.md)  
[ALTER EXTERNAL LANGUAGE (Transact-SQL)](alter-external-language-transact-sql.md)  
[sys.external_languages](../../relational-databases/system-catalog-views/sys-external-languages-transact-sql.md)  
[sys.external_language_files](../../relational-databases/system-catalog-views/sys-external-language-files-transact-sql.md)  
