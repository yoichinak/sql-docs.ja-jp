---
title: Oracle と SQL Server のデータ型のマッピング (OracleToSQL) |Microsoft Docs
description: SSMA for Oracle データ型と SQL Server 間のマッピングをカスタマイズする方法、または既定値をそのまま使用する方法について説明します。
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Type Mapping Inheritance
ms.assetid: 05da1495-63b9-47b7-86e2-6746394a2d8a
author: nahk-ivanov
ms.author: alexiva
manager: alexiva
ms.openlocfilehash: 8058123020571ad43e3142fccb920aa22a4b5af5
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100080783"
---
# <a name="mapping-oracle-and-sql-server-data-types-oracletosql"></a>Oracle と SQL Server データ型のマッピング (OracleToSQL)
Oracle データベースの種類は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、データベースの種類とは異なります。 Oracle データベースオブジェクトをオブジェクトに変換する場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、データ型を oracle からにマップする方法を指定する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 既定のデータ型マッピングをそのまま使用することも、次のセクションに示すようにマッピングをカスタマイズすることもできます。  
  
## <a name="default-mappings"></a>既定のマップ  
SSMA には、データ型マッピングの既定のセットがあります。 既定のマッピングの一覧については、「 [プロジェクトの設定 &#40;Type Mapping&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md)」を参照してください。  
  
## <a name="type-mapping-inheritance"></a>型マッピングの継承  
型マッピングは、プロジェクトレベル、オブジェクトカテゴリレベル (すべてのストアドプロシージャなど)、またはオブジェクトレベルでカスタマイズできます。 設定は、下位レベルでオーバーライドされない限り、上位レベルから継承されます。 たとえば、プロジェクトレベルで **smallmoney** を **money** にマップすると、オブジェクトまたはカテゴリレベルでマッピングをカスタマイズしない限り、プロジェクト内のすべてのオブジェクトでこのマッピングが使用されます。  
  
SSMA の [ **型マッピング** ] タブを表示すると、背景は、継承される型マッピングを示すために色分けされます。 型マッピングの背景は、継承された型マッピングの場合は黄色、現在のレベルで指定されているマッピングの場合は白になります。  
  
## <a name="customizing-data-type-mappings"></a>データ型マッピングのカスタマイズ  
次の手順では、データ型をプロジェクト、データベース、またはオブジェクトレベルでマップする方法について説明します。  
  
**データ型をマップするには**  
  
1.  プロジェクト全体のデータ型マッピングをカスタマイズするには、[ **プロジェクトの設定** ] ダイアログボックスを開きます。  
  
    1.  [ **ツール** ] メニューの [ **プロジェクトの設定**] をクリックします。  
  
    2.  左側のウィンドウで、[ **型マッピング**] を選択します。  
  
        右ペインに型マッピンググラフとボタンが表示されます。  
  
    または、データベース、テーブル、ビュー、またはストアドプロシージャレベルでのデータ型マッピングをカスタマイズするには、Oracle メタデータエクスプローラーでデータベース、オブジェクトカテゴリ、またはオブジェクトを選択します。  
  
    1.  Oracle メタデータエクスプローラーで、カスタマイズするフォルダーまたはオブジェクトを選択します。  
  
    2.  右ペインで、[ **型マッピング** ] タブをクリックします。  
  
2.  新しいマッピングを追加するには、次の手順を実行します。  
  
    1.  **[追加]** をクリックします。  
  
    2.  [ **ソースの種類**] で、マップする Oracle データ型を選択します。  
  
    3.  型の長さが必要な場合は、[ **開始** ] ボックスにマッピングの最小データ長を指定し、[変換後 **] ボックスに** データの最大長を指定します。  
  
        これにより、データマップをカスタマイズして、同じデータ型の小さい値と大きい値を指定できます。  
  
    4.  [ **対象の型**] で、対象のデータ型を選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
        一部の型では、対象のデータ型の長さが必要です。 必要に応じて、[ **置換後の文字列** ] ボックスに新しいデータ長を入力します。  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  データ型のマッピングを変更するには、次の手順を実行します。  
  
    1.  **[編集]** をクリックします。  
  
    2.  [ **ソースの種類**] で、マップする Oracle データ型を選択します。  
  
    3.  型の長さが必要な場合は、[ **開始** ] ボックスにマッピングの最小データ長を指定し、[変換後 **] ボックスに** データの最大長を指定します。  
  
        これにより、データマップをカスタマイズして、同じデータ型の小さい値と大きい値を指定できます。  
  
    4.  [ **対象の型**] で、対象のデータ型を選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
        一部の型では、対象のデータ型の長さが必要です。 必要に応じて、[置換後の **文字列** ] ボックスに新しいデータ長を入力し、 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  カスタムデータ型マッピングを削除するには、次の手順を実行します。  
  
    1.  [型マッピング] ボックスの一覧で、削除するデータ型マッピングが含まれている行を選択します。  
  
    2.  **[削除]** をクリックします。  
  
        継承されたマッピングを削除することはできません。 ただし、継承されたマッピングは、特定のオブジェクトまたはオブジェクトカテゴリのカスタムマッピングによって上書きされます。  
  
## <a name="next-steps"></a>次の手順  
移行プロセスの次の手順では、 [評価レポートを作成](assessing-oracle-schemas-for-conversion-oracletosql.md) するか、 [Oracle データベースオブジェクトを SQL Server 構文に変換](converting-oracle-schemas-oracletosql.md)します。 評価レポートを作成する場合は、評価中に Oracle オブジェクトが自動的に変換されます。  
  
## <a name="see-also"></a>参照  
[Oracle データベースの SQL Server &#40;OracleToSQL&#41;への移行 ](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
