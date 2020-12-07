---
title: SSMA:Linux 上の SQL Server への移行を自動化する
description: SQL Server Migration Assistant (SSMA) を使用し、Microsoft Access、DB2、MySQL、Oracle、Sybase から Linux 上の SQL Server へのデータベースの移行を自動化します。
ms.custom: seo-lt-2019
author: VanMSFT
ms.author: vanto
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 251bc3af-ebce-4d97-adec-afc0e7fab6cc
ms.openlocfilehash: 661fbd184750fbb912ef44d28c7d6cdf2d68c917
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115828"
---
# <a name="automate-database-migration-to-linux-with-the-sql-server-migration-assistant-ssma"></a>SQL Server Migration Assistant (SSMA) を使用して Linux へのデータベースの移行を自動化する

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

この記事では、Microsoft Access、DB2、MySQL、Oracle、Sybase から SQL Server on Linux にデータベースを簡単に移行できる [SQL Server Migration Assistant (SSMA)](../ssma/sql-server-migration-assistant.md) を紹介します。 SSMA は Windows アプリケーションです。Linux 上のリモート SQL Server インスタンスに接続できる Windows マシンがある場合は SSMA を使用してください。 

SSMA は、Oracle、MySQL、Sybase、DB2、Microsoft Access などのさまざまなソース データベースの SQL Server on Linux への移行をサポートし、次のような移行タスクを自動化するために役立ちます。

- ソース データベースを評価する
- ソース データベース スキーマを Microsoft SQL Server スキーマに変換する
- スキーマを移行する
- データを移行する
- 移行をテストする

まず、次の一覧からソース データベースに適した SQL Server Migration Assistant (SSMA) をダウンロードします。
- [SSMA for Access](https://aka.ms/ssmaforaccess)
- [SSMA for DB2](https://aka.ms/ssmafordb2)
- [SSMA for MySql](https://aka.ms/ssmaformysql) 
- [SSMA for Oracle](https://aka.ms/ssmafororacle)
- [SSMA for Sybase ASE](https://aka.ms/ssmaforsybase) 

次に、[SQL Server Migration Assistant (SSMA)](../ssma/sql-server-migration-assistant.md) に従って、ソース データベースを SQL Server on Linux に移行します。

## <a name="see-also"></a>関連項目
- [Microsoft Data Migration ブログ](https://blogs.msdn.microsoft.com/datamigration)
- [SQL Server Migration Assistant (SSMA) ブログ](/archive/blogs/ssma/)