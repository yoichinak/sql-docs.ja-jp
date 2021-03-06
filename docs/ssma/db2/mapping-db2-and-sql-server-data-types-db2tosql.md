---
description: DB2 と SQL Server のデータ型のマッピング (DB2ToSQL)
title: DB2 と SQL Server のデータ型のマッピング (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e7e939a8-5e76-4509-beaf-5acd1cab505e
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 32cf19b192fe67802ae44eaf9ce6e4ca891d02ae
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100072366"
---
# <a name="mapping-db2-and-sql-server-data-types-db2tosql"></a>DB2 と SQL Server のデータ型のマッピング (DB2ToSQL)
DB2 データベースの種類は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、データベースの種類とは異なります。 DB2 データベースオブジェクトをオブジェクトに変換する場合は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、db2 のデータ型をにマップする方法を指定する必要があり [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。 既定のデータ型マッピングをそのまま使用することも、次のセクションに示すようにマッピングをカスタマイズすることもできます。  
  
## <a name="default-mappings"></a>既定のマップ  
SSMA には、データ型マッピングの既定のセットがあります。 既定のマッピングの一覧については、「 [プロジェクトの設定 &#40;Type Mapping&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md)」を参照してください。  
  
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
  
    または、データベース、テーブル、ビュー、またはストアドプロシージャレベルでのデータ型マッピングをカスタマイズするには、DB2 メタデータエクスプローラーでデータベース、オブジェクトカテゴリ、またはオブジェクトを選択します。  
  
    1.  DB2 メタデータエクスプローラーで、カスタマイズするフォルダーまたはオブジェクトを選択します。  
  
    2.  右ペインで、[ **型マッピング** ] タブをクリックします。  
  
2.  新しいマッピングを追加するには、次の手順を実行します。  
  
    1.  **[追加]** をクリックします。  
  
    2.  [ **ソースの種類**] で、マップする DB2 データ型を選択します。  
  
    3.  型の長さが必要な場合は、[ **開始** ] ボックスにマッピングの最小データ長を指定し、[変換後 **] ボックスに** データの最大長を指定します。  
  
        これにより、データマップをカスタマイズして、同じデータ型の小さい値と大きい値を指定できます。  
  
    4.  [ **対象の型**] で、対象のデータ型を選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
        一部の型では、対象のデータ型の長さが必要です。 必要に応じて、[ **置換後の文字列** ] ボックスに新しいデータ長を入力します。  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  データ型のマッピングを変更するには、次の手順を実行します。  
  
    1.  **[編集]** をクリックします。  
  
    2.  [ **ソースの種類**] で、マップする DB2 データ型を選択します。  
  
    3.  型の長さが必要な場合は、[ **開始** ] ボックスにマッピングの最小データ長を指定し、[変換後 **] ボックスに** データの最大長を指定します。  
  
        これにより、データマップをカスタマイズして、同じデータ型の小さい値と大きい値を指定できます。  
  
    4.  [ **対象の型**] で、対象のデータ型を選択し [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ます。  
  
        一部の型では、対象のデータ型の長さが必要です。 必要に応じて、[置換後の **文字列** ] ボックスに新しいデータ長を入力し、 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  カスタムデータ型マッピングを削除するには、次の手順を実行します。  
  
    1.  [型マッピング] ボックスの一覧で、削除するデータ型マッピングが含まれている行を選択します。  
  
    2.  **[削除]** をクリックします。  
  
        継承されたマッピングを削除することはできません。 ただし、継承されたマッピングは、特定のオブジェクトまたはオブジェクトカテゴリのカスタムマッピングによって上書きされます。  
  
## <a name="next-steps"></a>次の手順  
移行プロセスの次の手順では、 [評価レポート &#40;DB2ToSQL&#41;](../../ssma/db2/assessment-report-db2tosql.md) 、または [DB2 スキーマ &#40;DB2ToSQL&#41;に変換 ](../../ssma/db2/converting-db2-schemas-db2tosql.md)します。 評価レポートを作成する場合、DB2 オブジェクトは評価中に自動的に変換されます。  
  
## <a name="see-also"></a>参照  
[DB2 データベースを SQL Server &#40;DB2ToSQL&#41;に移行する ](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
