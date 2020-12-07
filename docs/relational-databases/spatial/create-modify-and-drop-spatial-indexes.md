---
description: 空間インデックスの作成、変更、および削除
title: 空間インデックスの作成、変更、および削除 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- indexes [SQL Server], creating
- spatial indexes [SQL Server], dropping
- spatial indexes [SQL Server], creating
- indexes [SQL Server], dropping
- indexes [SQL Server], modifying
- spatial indexes [SQL Server], modifying
ms.assetid: 00c1b927-8ec5-44cf-87c2-c8de59745735
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bb02f98fbfad4dbad81983afd09daf04ed1e0176
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006360"
---
# <a name="create-modify-and-drop-spatial-indexes"></a>空間インデックスの作成、変更、および削除
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]
  空間インデックスは、 **geometry** データ型や **geography** データ型の列 ( *空間列*) に対する一部の操作をより効率的に実行できます。 1 つの空間列に対して複数の空間インデックスを指定できます。 たとえば、1 つの列の異なるテセレーション パラメーターのインデックスを作成する場合などに便利です。  
  
 空間インデックスの作成にはいくつかの制限があります。 詳細については、このトピックの「 [空間インデックスに関する制限](#restrictions) 」を参照してください。  
  
> [!NOTE]  
>  空間インデックスとパーティションやファイル グループとの関係については、「 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)」の「解説」をご覧ください。  
  
##  <a name="creating-modifying-and-dropping-spatial-indexes"></a><a name="creating"></a> 空間インデックスの作成、変更、および削除  
  
###  <a name="to-create-a-spatial-index"></a><a name="create"></a> 空間インデックスを作成するには  
 **Transact-SQL を使用して空間インデックスを作成するには**  
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)  
  
 **Management Studio の [新しいインデックス] ダイアログ ボックスを使用して空間インデックスを作成するには**  
 ##### <a name="to-create-a-spatial-index-in-management-studio"></a>Management Studio で空間インデックスを作成するには  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、指定されたインデックスを含むテーブルが格納されたデータベースを展開して、 **[テーブル]** を展開します。  
  
3.  インデックスを作成するテーブルを展開します。  
  
4.  **[インデックス]** を右クリックして **[新しいインデックス]** をクリックします。  
  
5.  **[インデックス名]** フィールドにインデックスの名前を入力します。  
  
6.  **[インデックスの種類]** ボックスの一覧の **[空間]** をクリックします。  
  
7.  インデックスを作成する空間列を指定するには、 **[追加]** をクリックします。  
  
8.  [ *\<table name>* **から列を選択**] ダイアログ ボックスで、対応するチェック ボックスをオンにして、**geometry** または **geography** 型の列を選択します。 その他の空間列は編集できなくなります。 別の空間列を選択するには、先に現在選択されている列の選択を解除する必要があります。 完了したら、 **[OK]** をクリックします。  
  
9. **[インデックス キー列]** グリッドで、選択した列を確認します。  
  
10. **[インデックスのプロパティ]** ダイアログ ボックスの **[ページの選択]** ペインで、 **[空間]** をクリックします。  
  
11. **[空間]** ページで、インデックスの空間プロパティに対して使用する値を指定します。  
  
     **geometry** 型の列にインデックスを作成する場合は、境界ボックスの座標 **(** _X-min_ **,** _Y-min_ **)** および **(** _X-max_ **,** _Y-max_ **)** を指定する必要があります。 **geography** 型の列のインデックスの場合は、 **[地理グリッド]** テセレーション スキームを指定すると境界ボックスのフィールドが読み取り専用になります。地理グリッド テセレーションでは境界ボックスは使用されません。  
  
     また、 **[オブジェクトごとのセル数]** フィールドに既定以外の値を指定したり、テセレーション スキームの任意のレベルのグリッド密度を指定したりすることもできます。 オブジェクトごとのセル数の既定値は、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] では 16、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降では 8 で、 **のグリッド密度の既定値は** [中] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]です。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、テセレーション スキームに GEOMETRY_AUTO_GRID または GEOGRAPHY_AUTO_GRID を選択することができます。 GEOMETRY_AUTO_GRID または GEOGRAPHY_AUTO_GRID を選択すると、レベル 1、レベル 2、レベル 3、およびレベル 4 のグリッド密度のオプションが無効になります。  
  
     これらのプロパティの詳細については、「 [[インデックスのプロパティ] の F1 ヘルプ](../../relational-databases/indexes/index-properties-f1-help.md)」をご覧ください。  
  
12. **[OK]** をクリックします。  
  
> [!NOTE]  
>  同じ空間列または異なる空間列に別の空間インデックスを作成するには、上の手順を繰り返します。  
  
  
 **Management Studio のテーブル デザイナーを使用して空間インデックスを作成するには**  
 ##### <a name="to-create-a-spatial-index-in-table-designer"></a>テーブル デザイナーで空間インデックスを作成するには  
  
1.  オブジェクト エクスプローラーで、空間インデックスを作成するテーブルを右クリックし、 **[デザイン]** をクリックします。  
  
     テーブル デザイナーにテーブルが表示されます。  
  
2.  インデックスを作成する **geometry** 列または **geography** 列を選択します。  
  
3.  **[テーブル デザイナー]** メニューの **[空間インデックス]** をクリックします。  
  
4.  **[空間インデックス]** ダイアログ ボックスの **[追加]** をクリックします。  
  
5.  **[選択された空間インデックス]** ボックスの一覧で新しいインデックスを選択し、右側のグリッドで空間インデックスのプロパティを設定します。 プロパティの詳細については、「[[空間インデックス] ダイアログ ボックス &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/spatial-indexes-dialog-box-visual-database-tools.md)」をご覧ください。  
  
  
###  <a name="to-alter-a-spatial-index"></a><a name="alter"></a> 空間インデックスを変更するには  
  
-   [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
    > [!IMPORTANT]  
    >  BOUNDING_BOX や GRID など、空間インデックス固有のオプションを変更するには、DROP_EXISTING = ON を指定する CREATE SPATIAL INDEX ステートメントを使用するか、空間インデックスを削除して新しく作成します。 例については、「 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)」の「解説」をご覧ください。  
  
-   [インデックスの変更](../../relational-databases/indexes/modify-an-index.md)  
  
-   [既存のインデックスの別のファイル グループへの移動](../../relational-databases/indexes/move-an-existing-index-to-a-different-filegroup.md)  
  
  
###  <a name="to-drop-a-spatial-index"></a><a name="drop"></a> 空間インデックスを削除するには  
 **Transact-SQL を使用して空間インデックスを削除するには**  
 [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
 **Management Studio を使用してインデックスを削除するには**  
 [インデックスの削除](../../relational-databases/indexes/delete-an-index.md)  
  
 **Management Studio のテーブル デザイナーを使用して空間インデックスを削除するには**  
 ##### <a name="to-drop-a-spatial-index-in-table-designer"></a>テーブル デザイナーで空間インデックスを削除するには  
  
1.  オブジェクト エクスプローラーで、削除する空間インデックスが含まれているテーブルを右クリックし、 **[デザイン]** をクリックします。  
  
     テーブル デザイナーにテーブルが表示されます。  
  
2.  **[テーブル デザイナー]** メニューの **[空間インデックス]** をクリックします。  
  
     **[空間インデックス]** ダイアログ ボックスが表示されます。  
  
3.  **[選択された空間インデックス]** 列で削除するインデックスをクリックします。  
  
4.  **[削除]** をクリックします。  
  
  
##  <a name="restrictions-on-spatial-indexes"></a><a name="restrictions"></a> 空間インデックスに関する制限  
 空間インデックスは、 **geometry** 型または **geography**型の列にのみ作成できます。  
  
### <a name="table-and-view-restrictions"></a>テーブルおよびビューの制限  
 空間インデックスは、主キーがあるテーブルでしか定義できません。 テーブルの主キー列の最大数は 15 です。  
  
 インデックス キー レコードの最大サイズは 895 バイトです。 このサイズを超えるとエラーが発生します。  
  
> [!NOTE]  
>  主キーのメタデータは、テーブルに空間インデックスが定義されていると変更できません。  
  
 インデックス付きビューに対して空間インデックスを指定することはできません。  
  
### <a name="multiple-spatial-index-restrictions"></a>複数の空間インデックスに関する制限  
 空間インデックスは、サポートされているテーブルの任意の空間列に 249 個まで作成できます。 同じ空間列に複数の空間インデックスを作成すると、1 つの列の異なるテセレーション パラメーターのインデックスを作成する場合などに便利です。  
  
 一度に作成できる空間インデックスは 1 つだけです。  
  
### <a name="spatial-indexes-and-process-parallelism"></a>空間インデックスとプロセスの並列処理  
 インデックスの構築では、プロセスの並列処理を使用できます。  
  
### <a name="version-restrictions"></a>バージョンの制限事項  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] で導入された空間テセレーションは、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]にレプリケートできません。 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] のデータベースとの下位互換性が必要条件である場合は、空間インデックスで [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 空間テセレーションを使用する必要があります。  
  
  
## <a name="see-also"></a>参照  
 [空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)  
  
