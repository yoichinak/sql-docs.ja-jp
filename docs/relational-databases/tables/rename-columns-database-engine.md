---
description: 列名の変更 (データベース エンジン)
title: 列名の変更 (データベース エンジン) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], names
- renaming columns
- column names [SQL Server]
ms.assetid: 7c71ec9f-0180-4398-b32a-4bfb7592e75d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 18ed629f6a9d02c0068a20fc1da3e8d5c4375dc2
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645801"
---
# <a name="rename-columns-database-engine"></a>列名の変更 (データベース エンジン)


[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] では、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または [!INCLUDE[tsql](../../includes/tsql-md.md)]を使用してテーブル列の名前を変更することができます。

**このトピックの内容**

- **作業を開始する準備:**

   [制限事項と制約事項](#Restrictions)

   [Security](#Security)

- **列名を変更する方法:**

   [SQL Server Management Studio](#SSMSProcedure)

   [Transact-SQL](#TsqlProcedure)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> はじめに

### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 制限事項と制約事項

列名を変更しても、その列に対する参照の名前は自動的には変更されません。 名前を変更した列を参照しているオブジェクトに対しては、手動で変更を加える必要があります。 たとえば、テーブルの列の名前を変更するとき、その列がトリガーで参照されている場合は、新しい列名が反映されるようにトリガーに変更を加える必要があります。 オブジェクトの名前を変更する前には、 [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) を使ってオブジェクトの従属関係を一覧表示できます。

### <a name="security"></a><a name="Security"></a> セキュリティ

#### <a name="permissions"></a><a name="Permissions"></a> Permissions

オブジェクトに対する ALTER 権限が必要です。

## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio の使用

### <a name="to-rename-a-column-using-object-explorer"></a>オブジェクト エクスプ ローラーを使用して列の名前を変更するには

1. **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに接続します。
2. **オブジェクト エクスプローラー**で、列の名前を変更するテーブルを右クリックし、 **[名前の変更]** をクリックします。
3. 新しい列の名前を入力します。

### <a name="to-rename-a-column-using-table-designer"></a>テーブル デザイナーを使用して列の名前を変更するには

1. **オブジェクト エクスプローラー**で、列の名前を変更するテーブルを右クリックし、 **[デザイン]** をクリックします。
2. **[列名]** の下の変更する名前を選択して、新しい名前を入力します。
3. **[ファイル]** メニューの **[** _<テーブル名>_ を保存] をクリックします。

> [!NOTE]
> **[列のプロパティ]** タブで列の名前を変更することもできます。名前を変更する列を選択して、 **[名前]** に新しい値を入力します。

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL の使用

**列名を変更するには**

### <a name="to-rename-a-column"></a>列名を変更するには

次の例では、AdventureWorks データベース内で `Sales.SalesTerritory` テーブルの `TerritoryID` 列の名前を `TerrID` に変更します。

```sql
EXEC sp_rename 'Sales.SalesTerritory.TerritoryID', 'TerrID', 'COLUMN';
```

詳細については、「[sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)」を参照してください。
