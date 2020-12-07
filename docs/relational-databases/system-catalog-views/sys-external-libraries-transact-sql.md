---
description: sys.external_libraries (Transact-SQL)
title: external_libraries (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/25/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- external_libraries
- external_libraries_TSQL
- sys.external_libraries
- sys.external_libraries_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_libraries catalog view
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 6dcc1b8f7cddc785203dc2430c2f1a4dce4b4d39
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88377578"
---
# <a name="sysexternal_libraries-transact-sql"></a>sys.external_libraries (Transact-SQL)  
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

では、R、Python、Java などの外部ランタイムに関連するパッケージライブラリの管理がサポートされています。

> [!NOTE]
> SQL Server 2017 では、R 言語と Windows プラットフォームがサポートされています。 Windows および Linux プラットフォームの R、Python、Java は SQL Server 2019 以降でサポートされています。 Azure SQL Managed Instance では、R と Python がサポートされています。

## <a name="sysexternal_libraries"></a>sys.external_libraries

カタログビューの external_libraries には、データベースにアップロードされた各外部ライブラリの行が一覧表示されます。

|列名 |データ型 | 説明|
|------|------|------|
|external_library_id |INT | 外部ライブラリオブジェクトの ID。 |
|name |sysname |外部ライブラリの名前。 所有者ごとにデータベース内で一意です。|
|principal_id |INT |この外部ライブラリを所有するプリンシパルの ID。 |
|language | sysname | 外部ライブラリをサポートする言語またはランタイムの名前。 有効な値は、' R '、' Python '、および ' Java ' です。 今後、追加のランタイムが追加される可能性があります。|
|scope |INT |パブリックスコープの場合は0。プライベートスコープの場合は1 |  
|scope_desc |varchar (7) |パッケージがパブリックであるかプライベートであるかを示します|

## <a name="see-also"></a>関連項目  

+ [sys.external_library_files](sys-external-library-files-transact-sql.md)  
+ [外部ライブラリの作成](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [新しい R パッケージのインストール](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md)  
+ [新しい Python パッケージのインストール](../../machine-learning/package-management/install-additional-python-packages-on-sql-server.md)  
