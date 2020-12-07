---
description: Sybase ASE と SQL Server データ型とのマッピング (SybaseToSQL)
title: Sybase ASE と SQL Server のデータ型のマッピング (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping Sybase ASE Schemas to SQL Server Schemas
- Type Mapping Settings
ms.assetid: 784365d3-df4e-47ab-8ee0-d8392b52f510
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 5a7e1ba17822d339e5ae40e6e6b5828191ce84ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463174"
---
# <a name="mapping-sybase-ase-and-sql-server-data-types-sybasetosql"></a>Sybase ASE と SQL Server データ型とのマッピング (SybaseToSQL)
Sybase Adaptive Server Enterprise (ASE) データベースの種類 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、または Azure SQL Database の種類とは異なります。 ASE データベースオブジェクトをまたは SQL Azure オブジェクトに変換する場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、データ型を ase からまたは SQL Azure にマップする方法を指定する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 既定のデータ型マッピングをそのまま使用することも、次のセクションに示すようにマッピングをカスタマイズすることもできます。  
  
## <a name="default-mappings"></a>既定のマップ  
SSMA には、データ型マッピングの既定のセットがあります。 既定のマッピングの一覧については、「 [プロジェクトの設定 &#40;Type Mapping&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md)」を参照してください。  
  
## <a name="type-mapping-inheritance"></a>型マッピングの継承  
型マッピングは、プロジェクトレベル、オブジェクトカテゴリレベル (すべてのストアドプロシージャなど)、またはオブジェクトレベルでカスタマイズできます。 低いレベルでオーバーライドしない限り、設定は上位レベルから継承されます。 たとえば、プロジェクトレベルで **smallmoney** を **money** にマップした場合、オブジェクトカテゴリレベルまたはオブジェクトレベルでマッピングをカスタマイズしない限り、プロジェクト内のすべてのオブジェクトはこのマッピングを使用します。  
  
SSMA の [ **型マッピング** ] タブを表示すると、背景は、継承される型マッピングを示すために色分けされます。 型マッピングの背景は、継承された型マッピングの場合は黄色、現在のレベルで指定されているマッピングの場合は白になります。  
  
## <a name="customizing-data-type-mappings"></a>データ型マッピングのカスタマイズ  
次の手順では、データ型をプロジェクト、データベース、またはオブジェクトレベルでマップする方法について説明します。  
  
**データ型をマップするには**  
  
1.  プロジェクト全体のデータ型マッピングをカスタマイズするには、[ **プロジェクトの設定** ] ダイアログボックスを開きます。  
  
    1.  [ **ツール** ] メニューの [ **プロジェクトの設定**] をクリックします。  
  
    2.  左側のウィンドウで、[ **型マッピング**] を選択します。  
  
        右ペインに型マッピンググラフとボタンが表示されます。  
  
    または、データベース、テーブル、ビュー、またはストアドプロシージャレベルでのデータ型マッピングをカスタマイズするには、Sybase メタデータエクスプローラーでデータベース、オブジェクトカテゴリ、またはオブジェクトを選択します。  
  
    1.  Sybase メタデータエクスプローラーで、カスタマイズするフォルダーまたはオブジェクトを選択します。  
  
    2.  右ペインで、[ **型マッピング** ] タブをクリックします。  
  
2.  新しいマッピングを追加するには、次の手順を実行します。  
  
    1.  **[追加]** をクリックします。  
  
    2.  [ **ソースの種類**] で、マップする ASE データ型を選択します。  
  
    3.  型の長さが必要な場合は、[ **開始** ] ボックスでマッピングの最小データ長を指定し、[ **対象** ] ボックスでマッピングの最大データ長を指定します。  
  
        これにより、データマップをカスタマイズして、同じデータ型の小さい値と大きい値を指定できます。  
  
    4.  [ **ターゲットの種類**] で、ターゲット [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure データ型を選択します。  
  
        一部の型では、対象のデータ型の長さが必要です。 必要に応じて、[ **置換後の文字列** ] ボックスに新しいデータ長を入力します。  
  
    5.  **[OK]** をクリックします。  
  
3.  データ型のマッピングを編集するには、次の手順を実行します。  
  
    1.  **[編集]** をクリックします。  
  
    2.  [ **ソースの種類**] で、マップする ASE データ型を選択します。  
  
    3.  型の長さが必要な場合は、[ **開始** ] ボックスでマッピングの最小データ長を指定し、[ **対象** ] ボックスでマッピングの最大データ長を指定します。  
  
        これにより、データマップをカスタマイズして、同じデータ型の小さい値と大きい値を指定できます。  
  
    4.  [ **ターゲットの種類**] で、ターゲット [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure データ型を選択します。  
  
        一部の型では、対象のデータ型の長さが必要です。 必要に応じて、[置換後の **文字列** ] ボックスに新しいデータ長を入力し、[ **OK**] をクリックします。  
  
4.  カスタムデータ型マッピングを削除するには、次の手順を実行します。  
  
    1.  [型マッピング] ボックスの一覧で、削除するデータ型マッピングが含まれている行を選択します。  
  
    2.  **[削除]** をクリックします。  
  
        継承されたマッピングを削除することはできません。 ただし、継承されたマッピングは、特定のオブジェクトまたはオブジェクトカテゴリのカスタムマッピングによって上書きされます。  
  
## <a name="next-steps"></a>次の手順  
移行プロセスの次の手順では、 [評価レポートを作成](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) するか、 [Sybase ASE データベースオブジェクトを SQL Server または SQL Azure 構文に変換](converting-sybase-ase-database-objects-sybasetosql.md)します。 評価レポートを作成する場合、Sybase ASE オブジェクトは評価中に自動的に変換されます。  
  
## <a name="see-also"></a>参照  
[Sybase ASE データベースを SQL Server Azure SQL Database &#40;SybaseToSQL&#41;に移行する ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
