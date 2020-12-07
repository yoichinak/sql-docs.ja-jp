---
description: DDL トリガーの実装
title: DDL トリガーの実装 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- DDL triggers, implementing
ms.assetid: f44e5340-1d18-40e9-828e-0ffcca091ae3
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b6ad03a2ca062ecc93d8027d544ca37ef142cb74
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472984"
---
# <a name="implement-ddl-triggers"></a>DDL トリガーの実装
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  ここでは、DDL トリガーの作成、DDL トリガーの変更、および DDL トリガーの無効化または削除に役立つ情報を提供します。  
  
## <a name="creating-ddl-triggers"></a>DDL トリガーの作成  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TRIGGER ステートメントを使用することにより、DDL トリガーが作成されます。  
  
 **DDL トリガーを作成するには**  
  
-   [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
> [!IMPORTANT]  
>  今後のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、トリガーを使用して結果セットを返す機能が削除される予定です。 結果セットを返すトリガーは、それと連動するように設計されていないアプリケーションでは予期しない動作を起こすことがあります。 新しい開発作業では、トリガーを使用して結果セットを返すことを避け、現在この方法を使用しているアプリケーションについては変更を検討してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でトリガーを使用して結果セットを返さないようにするには、 [disallow results from triggers](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md) オプションを 1 に設定します。 今後のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、このオプションの既定の設定は 1 になります。  
  
## <a name="modifying-ddl-triggers"></a>DDL トリガーの変更  
 DDL トリガーの定義を変更する必要がある場合は、トリガーを削除してから作成し直すか、または既存のトリガーの再定義を行います。  
  
 DDL トリガーで参照されるオブジェクトの名前を変更する際には、新しい名前が反映されるようにトリガーを変更する必要があります。 したがって、オブジェクトの名前を変更する前に、まずオブジェクトの依存関係を表示して、オブジェクト名の変更により影響を受けるトリガーがあるかどうかを確認してください。  
  
 トリガーは、定義が暗号化されるように変更することもできます。  
  
 **トリガーを変更するには**  
  
-   [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
 **トリガーの依存関係を表示するには**  
  
-   [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
-   [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)  
  
-   [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
## <a name="disabling-and-dropping-ddl-triggers"></a>DDL トリガーの無効化と削除  
 DDL トリガーが不要になった場合は、そのトリガーを無効にするかまたは削除できます。  
  
 DDL トリガーを無効にしても削除はされません。 オブジェクトとして現在のデータベースに残りますが、 トリガーがプログラムされた [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントを実行しても、トリガーは起動しません。 無効になった DDL トリガーは、再度有効にできます。 トリガーを有効にすると、最初に作成したときと同じ方法でトリガーが起動されます。 DDL トリガーが作成されると、既定で有効になります。  
  
 DDL トリガーを削除すると、現在のデータベースから削除されます。 DDL トリガーのスコープが設定されているオブジェクトやデータには影響しません。  
  
 **DDL トリガーを無効にするには**  
  
-   [DISABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/disable-trigger-transact-sql.md)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
 **DDL トリガーを有効にするには**  
  
-   [ENABLE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/enable-trigger-transact-sql.md)  
  
-   [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
 **DDL トリガーを削除するには**  
  
-   [DROP TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-trigger-transact-sql.md)  
  
  
