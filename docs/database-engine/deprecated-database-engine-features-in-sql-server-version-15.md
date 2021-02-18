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
ms.openlocfilehash: b6a8b2edf94d74720836e02589ec8e1270f38dac
ms.sourcegitcommit: c83c17e44b5e1e3e2a3b5933c2a1c4afb98eb772
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/15/2021
ms.locfileid: "100525169"
---
# <a name="deprecated-database-engine-features-in-sql-server-2019-15x"></a>SQL Server 2019 (15.x) データベース エンジンの非推奨の機能

[!INCLUDE[sqlserver2019](../includes/applies-to-version/sqlserver2019.md)]

[!INCLUDE [sssql19-md](../includes/sssql19-md.md)] では、以前のリリースで非推奨となったもの以外の機能は非推奨にされません。

- [[!INCLUDE [sssql17-md](../includes/sssql17-md.md)]](deprecated-database-engine-features-in-sql-server-2017.md)
- [[!INCLUDE [sssql16-md](../includes/sssql16-md.md)]](deprecated-database-engine-features-in-sql-server-2016.md)

## <a name="deprecation-guidelines"></a>非推奨のガイドライン

機能に非推奨の印が付いている場合、それは次のことを意味します。

- その機能は保守管理状態にあり、それ以外では利用されていません。 新しい変更は行われません。新しい機能との相互運用性に関する変更もありません。
- Microsoft は、アップグレードを容易にする目的で、今後のリリースから非推奨機能を外さないように努めます。 ただし、非推奨機能が将来の技術革新を制限してしまう場合、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] からそれを永久的に外すことをまれに選択することがあります。
- 新しい開発作業に非推奨機能を使用することはお勧めしません。      

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