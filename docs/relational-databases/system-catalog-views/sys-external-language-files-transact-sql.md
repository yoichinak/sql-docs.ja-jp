---
description: external_language_files (Transact-sql)-SQL Server
title: external_language_files (Transact-sql)-SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- external_languages
- external_languages_TSQL
- sys.external_languages
- sys.external_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_languages catalog view
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fe6da94cc085e14667ee0518452fc6043eed60e9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88401068"
---
# <a name="sysexternal_language_files-transact-sql"></a>external_language_files (Transact-sql)
[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

このカタログビューには、データベース内の外部言語拡張ファイルの一覧が表示されます。 **R** と **Python** は予約済みの名前であり、それらの特定の名前で外部言語を作成することはできません。

File_spec から外部言語が作成されると、拡張機能自体とそのプロパティがこのビューに表示されます。 このビューには、OS ごとに1つのエントリが含まれます。

## <a name="sysexternal_languages"></a>sys.external_languages

カタログビューの external_language_files には、データベース内の外部言語拡張機能ごとに1行のデータが表示されます。 パラメーター

|列名 |データ型 | 説明|
|------|------|------|
|external_language_id |INT | 外部言語の ID|
|コンテンツ|varbinary(max) |外部言語拡張ファイルの内容|
|file_name|nvarchar (266)|言語拡張ファイルの名前|
|platform|tinyint|SQL Server がインストールされているホストプラットフォームの ID|
|platform_desc |nvarchar(60)|ホストプラットフォームの名前。 有効な値は ' WINDOWS '、' LINUX ' です。|
|parameters|nvarchar(4000)|外部言語 prameters|
|environment_variables |nvarchar(4000)|外部言語環境変数|

## <a name="see-also"></a>関連項目  

+ [sys.external_languages](sys-external-languages-transact-sql.md)  
+ [外部言語の作成](../../t-sql/statements/create-external-language-transact-sql.md)  
