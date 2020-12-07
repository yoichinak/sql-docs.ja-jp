---
description: テンポラル テーブルでのパーティション分割
title: テンポラル テーブルでのパーティション分割 | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 313714b8-4ad1-4c14-93a3-7f628a334a51
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0af4a041580d59cc77d5605dc1df72ca8b823f0c
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548853"
---
# <a name="partitioning-with-temporal-tables"></a>テンポラル テーブルでのパーティション分割


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]


パーティション分割は、現在のテーブルと履歴テーブルで個別に使用できます。 ただし、システム バージョン管理を行わずに、パーティション分割を使用してデータのコンテンツを変更することはできません。

> [!NOTE]
> パーティション分割は Service Pack 1 以前のバージョンの SQL Server 2016 では Enterprise Edition の機能です。 パーティション分割は、SQL Server 2016 Service Pack 1 以降のバージョンのすべてのエディションでサポートされます。

- **現在のテーブル:**

  - **SYSTEM_VERSIONING** が **ON** の場合、現在のテーブルへの **SWITCH IN**
  - **SYSTEM_VERSIONING** が **ON** の場合、現在のテーブルへの **SWITCH IN**

- **履歴テーブル:**

  - **SYSTEM_VERSIONING** が **ON** の場合、履歴テーブルからの **SWITCH OUT** を実行して、関連性がなくなった一部のデータを消去します。
  - **SYSTEM_VERSIONING** が **ON** の場合、 **SWITCH IN** は許可されません。これは、テンポラル データの整合性が無効になる場合があるためです。

## <a name="next-steps"></a>次のステップ

- [テンポラル テーブル](../../relational-databases/tables/temporal-tables.md)
- [システム バージョン管理されたテンポラル テーブルの概要](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [テンポラル テーブルのシステム一貫性のチェック](../../relational-databases/tables/temporal-table-system-consistency-checks.md)
- [テンポラル テーブルの考慮事項と制約](../../relational-databases/tables/temporal-table-considerations-and-limitations.md)
- [テンポラル テーブル セキュリティ](../../relational-databases/tables/temporal-table-security.md)
- [システム バージョン管理されたテンポラル テーブルの履歴データの保有期間管理](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [メモリ最適化テーブルでのシステム バージョン管理されたテンポラル テーブル](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [テンポラル テーブル メタデータのビューおよび関数](../../relational-databases/tables/temporal-table-metadata-views-and-functions.md)
