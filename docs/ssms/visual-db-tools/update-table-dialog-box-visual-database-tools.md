---
description: '[テーブルの更新] ダイアログ ボックス (Visual Database Tools)'
title: '[テーブルの更新] ダイアログ ボックス'
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.updatetable
- vdtsql.chm:69643
ms.assetid: 174c7275-5b15-42a9-b172-5ff30de575a1
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.openlocfilehash: 93c0ed1368325ec27ff9ebb640f48ee45f7de8ea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88369178"
---
# <a name="update-table-dialog-box-visual-database-tools"></a>[テーブルの更新] ダイアログ ボックス (Visual Database Tools)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

このダイアログ ボックスを使用すると、更新するテーブルを指定できます。

クエリの種類を UPDATE クエリに変更するときに、ダイアグラム ペインに複数のテーブルが表示される場合、このダイアログ ボックスが表示されます。  

更新するテーブルを選択し、**[OK]** をクリックします。

> [!NOTE]
> テーブルをレプリケーションのためにパブリッシュする場合は、Transact-SQL ステートメントの [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) または SQL Server 管理オブジェクト (SMO) を使用してスキーマを変更する必要があります。 テーブル デザイナーまたはデータベース ダイアグラム デザイナーを使用してスキーマを変更するとき、テーブルはいったん削除されてから再作成されます。 パブリッシュされたオブジェクトは削除できないので、スキーマの変更は失敗します。

## <a name="see-also"></a>参照

[更新クエリの作成](../../ssms/visual-db-tools/create-update-queries-visual-database-tools.md)
