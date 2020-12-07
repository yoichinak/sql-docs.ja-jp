---
description: MySQL と SQL Server データ型のマッピング (MySQLToSQL)
title: MySQL と SQL Server のデータ型のマッピング (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping, customize data type mapping
- Mapping, Type mapping
ms.assetid: 14f98054-13b4-4231-a6b0-2452f3b9941d
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 0df267807ff824cebac580fb3454d63de8dfe31b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463385"
---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>MySQL と SQL Server データ型のマッピング (MySQLToSQL)
MySQL データベースの型 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、型または Azure SQL Database 型とは異なります。 MySQL データベースオブジェクトをまたは SQL Azure オブジェクトに変換する場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、mysql からまたは SQL Azure にデータ型をマップする方法を指定する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 次の手順に示すように、既定のデータ型マッピングをそのまま使用することも、マッピングをカスタマイズすることもできます。  
  
## <a name="default-mappings"></a>既定のマップ  
SSMA には、データ型マッピングの既定のセットがあります。 既定のマッピングの一覧については、「 [プロジェクトの設定 &#40;Type Mapping&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md)」を参照してください。  
  
## <a name="type-mapping-inheritance"></a>型マッピングの継承  
型マッピングは、プロジェクトレベル、オブジェクトカテゴリレベル (すべてのストアドプロシージャなど)、またはオブジェクトレベルでカスタマイズできます。 設定は、下位レベルでオーバーライドされない限り、上位レベルから継承されます。 たとえば、プロジェクトレベルで **smallint** を **int** にマップすると、オブジェクトまたはカテゴリレベルでマッピングをカスタマイズしない限り、プロジェクト内のすべてのオブジェクトはこのマッピングを使用します。  
  
SSMA の [ **型マッピング** ] タブを表示すると、背景は、継承される型マッピングを示すために色分けされます。 型マッピングの背景は、継承された型マッピングの場合は黄色、現在のレベルで指定されているマッピングの場合は白になります。  
  
## <a name="customizing-data-type-mappings"></a>データ型マッピングのカスタマイズ  
  
-   **データ型をマップするには:**  
  
    次の手順では、プロジェクト、データベース、またはデータベースオブジェクトレベルでデータ型をマップする方法について説明します。  
  
    1.  プロジェクト全体のデータ型マッピングをカスタマイズするには、[ **プロジェクトの設定** ] ダイアログボックスを開きます。 [ツール] メニューの [ **プロジェクトの設定**] をクリックします。  
  
        左側のウィンドウで、[ **型マッピング**] を選択します。 右ペインに型マッピンググラフとボタンが表示されます。  
  
    2.  データベースレベルまたはテーブルレベルでデータ型マッピングをカスタマイズするには、MySQL メタデータエクスプローラーでデータベースまたはテーブルを選択します。 MySQL メタデータエクスプローラーで、カスタマイズするフォルダーまたはオブジェクトを選択します。  
  
        右ペインで、[ **型マッピング**] をクリックします。  
  
-   **新しいマッピングを追加するには、次の手順を実行します。**  
  
    1.  [型マッピング] ペインで、[ **追加** ] をクリックします。  
  
    2.  [新しい型のマッピング] ダイアログボックスの [ **ソースの種類**] で、マップする MySQL データ型を選択します。  
  
    3.  型の長さが必要な場合は、[開始] および [ **開始** ] チェックボックスをオンにして値を入力 **する** ことにより、マッピングのデータの最小長と最大長を指定します。  
  
    4.  これにより、データマップをカスタマイズして、同じデータ型の小さい値と大きい値を指定できます。 [ **ターゲットの種類**] で、ターゲット SQL Server または SQL Azure データ型を選択します。  
  
        1.  一部の型では、対象のデータ型の長さが必要です。 必要に応じて、[置換後の **文字列** ] ボックスに新しいデータ長を入力し、[ **OK**] をクリックします。  
  
        2.  一部の型では、ターゲットデータ型の **有効桁数** と **小数点以下桁数**が必要です。 必要に応じて、[置換後の **文字列** ] ボックスに新しい有効桁数と小数点以下桁数を入力し、[ **OK**] をクリックします。  
  
-   **型マッピングを編集するには、次の手順を実行します。**  
  
    1.  [型マッピング] ペインで、[ **編集**] をクリックします。  
  
    2.  [型マッピングの一覧] ダイアログボックスの [ **ソースの種類**] で、マップする MySQL データ型を選択します。  
  
    3.  型の長さが必要な場合は、[開始] および [ **開始** ] チェックボックスをオンにして値を入力 **する** ことにより、マッピングのデータの最小長と最大長を指定します。  
  
    これにより、データマップをカスタマイズして、同じデータ型の小さい値と大きい値を指定できます。 [ **ターゲットの種類**] で、ターゲット SQL Server または SQL Azure データ型を選択します。  
  
    -  一部の型では、対象のデータ型の長さが必要です。 必要に応じて、[置換後の **文字列** ] ボックスに新しいデータ長を入力し、[ **OK**] をクリックします。  
  
    -  一部の型では、ターゲットデータ型の **有効桁数** と **小数点以下桁数**が必要です。 必要に応じて、[置換後の **文字列** ] ボックスに新しい有効桁数と小数点以下桁数を入力し、[ **OK**] をクリックします。  
  
-   **データ型マッピングを削除するには、次の手順を実行します。**  
  
    1.  [型マッピング] ペインで、削除するデータ型マッピングが含まれている [型マッピング] ボックスの一覧で行を選択します。  
  
    2.  **[削除]** をクリックします。  
  
## <a name="next-step"></a>次の手順  
移行プロセスの次の手順では、 [評価レポートを作成](assessing-mysql-databases-for-conversion-mysqltosql.md) するか、 [MySQL データベースオブジェクトを SQL Server または SQL Azure 構文に変換](converting-mysql-databases-mysqltosql.md)します。 レポートを作成する場合、MySQL オブジェクトは評価中に自動的に変換されます。  
  
## <a name="see-also"></a>参照  
[MySQL データベースを SQL Server Azure SQL Database &#40;MySQLToSql&#41;に移行する ](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
