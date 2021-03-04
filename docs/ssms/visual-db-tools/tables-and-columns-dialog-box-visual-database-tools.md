---
description: '[テーブルと列] ダイアログ ボックス (Visual Database Tools)'
title: '[テーブルと列] ダイアログ ボックス'
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.tablesandcolumns
ms.assetid: 8cf27be1-e66d-4735-a428-9ab4b33af4f5
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: ce49303d14dc92811b383349c7fa8d74202ab8ea
ms.sourcegitcommit: 9413ddd8071da8861715c721b923e52669a921d8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2021
ms.locfileid: "101836939"
---
# <a name="tables-and-columns-dialog-box-visual-database-tools"></a>[テーブルと列] ダイアログ ボックス (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
このダイアログ ボックスを使用すると、あるテーブルの主キーを別のテーブルの外部キーに割り当てることができます。 このダイアログ ボックスにアクセスするには、 **[テーブル デザイナー]** メニューの **[リレーションシップ]** をクリックします。 **[外部キーのリレーションシップ]** ダイアログ ボックスの **[テーブルと列の指定]** フィールドをクリックして、プロパティの右側にある省略記号 ( **[...]** ) をクリックします。  
  
> [!NOTE]  
> テーブルをレプリケーションのためにパブリッシュする場合は、Transact-SQL ステートメントの [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) または SQL Server 管理オブジェクト (SMO) を使用してスキーマを変更する必要があります。 テーブル デザイナーまたはデータベース ダイアグラム デザイナーを使用してスキーマを変更するとき、テーブルはいったん削除されてから再作成されます。 パブリッシュされたオブジェクトは削除できないので、スキーマの変更は失敗します。  
  
## <a name="options"></a>オプション  
**[リレーションシップ名]**  
リレーションシップの名前を表示します。  
  
**[主キー テーブル]**  
データベース内のテーブルの一覧を表示します。 リレーションシップの主キー側になるテーブルを選択します。  
  
**[外部キーのテーブル]**  
リレーションシップの外部キー側のテーブルを表示します。 これは、テーブル デザイナーで現在選択されているテーブルです。  
  
**[主キー テーブル] の下のグリッド**  
**[主キー テーブル]** ボックスで選択されているテーブルの列を一覧表示します。 そのテーブルの主キーになる列を入力します。  
  
**[外部キーのテーブル] の下のグリッド**  
**[外部キーのテーブル]** ボックスで選択されているテーブルの列を一覧表示します。 主キー列に対応する外部キーのテーブルの外部キー列を入力します。  
  
> [!NOTE]  
> 外部キーに選択した列は、対応する主キー列と同じデータ型である必要があります。 各キーには同じ数の列が必要です。 たとえば、リレーションシップの主キー側になるテーブルの主キーが 2 列で構成されている場合、この各列がリレーションシップの外部キー側になるテーブルの列と一致する必要があります。  
  
## <a name="see-also"></a>参照  
[方法: テーブル間のリレーションシップを作成する](../../relational-databases/tables/create-foreign-key-relationships.md)  
