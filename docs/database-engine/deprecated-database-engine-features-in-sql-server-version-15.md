---
description: '[!INCLUDE[sssql19-md](../includes/sssql19-md.md)] のデータベース エンジンの非推奨機能'
title: SQL Server 2019 データベース エンジンの非推奨の機能 | Microsoft Docs
titleSuffix: SQL Server 2019
ms.custom: seo-lt-2019
ms.date: 02/12/2021
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- deprecated changes 2019 [SQL Server]
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: 4e322ff478e9ccdc031882e7c3b5b18fd8506e42
ms.sourcegitcommit: ca81fc9e45fccb26934580f6d299feb0b8ec44b7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102186470"
---
# <a name="deprecated-database-engine-features-in-sql-server-2019-15x"></a>SQL Server 2019 (15.x) データベース エンジンの非推奨の機能

[!INCLUDE[sqlserver2019](../includes/applies-to-version/sqlserver2019.md)]

[!INCLUDE [sssql19-md](../includes/sssql19-md.md)] では、以前のリリースで非推奨となったもの以外の機能は非推奨にされません。

- [[!INCLUDE [sssql17-md](../includes/sssql17-md.md)]](deprecated-database-engine-features-in-sql-server-2017.md)
- [[!INCLUDE [sssql16-md](../includes/sssql16-md.md)]](deprecated-database-engine-features-in-sql-server-2016.md)

## <a name="deprecation-guidelines"></a>非推奨のガイドライン

機能に非推奨の印が付いている場合、それは次のことを意味します。

- その機能は保守管理状態にあり、それ以外では利用されていません。 新機能との相互運用性への対応に関連するものを含め、新しい変更は行われません。
- Microsoft は、アップグレードを容易にする目的で、今後のリリースから非推奨機能を外さないように努めます。 ただし、その機能によって将来の技術革新が制限されてしまう場合に、永久的にそれを中止、つまり、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] から外すことを選択することがまれにあります。
- 新規の開発作業では、非推奨の機能を使用しないでください。 既存のアプリケーションについては、これらの機能を現在使用しているアプリケーションをできるだけ早く修正するように計画してください。     

非推奨の機能の使用は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Deprecated Features オブジェクトのパフォーマンス カウンター、または`deprecation_announcement` と `deprecation_final_support` の拡張イベントを使用して監視できます。 詳細については、「 [SQL Server オブジェクトの使用](../relational-databases/performance-monitor/use-sql-server-objects.md)」を参照してください。  

## <a name="query-deprecated-features"></a>非推奨の機能のクエリ

これらのカウンターの値は、次のステートメントを実行して入手することもできます。  

```sql
SELECT * FROM sys.dm_os_performance_counters
WHERE object_name = 'SQLServer:Deprecated Features';
```

### <a name="see-also"></a>関連項目

- [SQL Server 2019 におけるデータベース エンジン機能の重大な変更](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-version-15.md)
- [SQL Server で廃止されたデータベース エンジンの機能](../database-engine/discontinued-database-engine-functionality-in-sql-server.md)
- [SQL Server データベース エンジンの旧バージョンとの互換性](./discontinued-database-engine-functionality-in-sql-server.md)
