---
title: master データベースと model データベースを合わせるようにユーザー定義データベースの照合順序を設定する
description: ユーザー定義データベースとシステム データベースが同じかどうかを確認するためのポリシーを有効にする方法について説明します。
ms.custom: seo-lt-2019
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 905accc62afdc12152110d44a18e61d4c8a9bcef
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/01/2020
ms.locfileid: "89285132"
---
# <a name="set-the-collation-of-user-defined-databases-to-match-master-and-model-databases"></a>master データベースと model データベースを合わせるようにユーザー定義データベースの照合順序を設定する
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  このルールでは、ユーザー定義データベースの定義に使用されたデータベース照合順序と master または model の照合順序が一致しているかどうかを確認します。
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスの推奨事項  
 ユーザー定義データベースの照合順序と master または model データベースの照合順序を一致させることをお勧めします。 照合順序が一致していない場合、照合順序の競合が発生してコードが実行されなくなる可能性があります。 たとえば、ストアド プロシージャによってあるテーブルを一時テーブルに結合すると、ユーザー定義のデータベースと model データベースの照合順序が異なる場合、SQL Server ではバッチが終了し、照合順序の競合エラーが返されることがあります。 この現象は、一時テーブルが tempdb に作成されることが原因で発生します。tempdb の照合順序は、model データベースの照合順序に基づいています。

  照合順序の競合エラーが発生した場合は、次のいずれかの解決策を検討してください。

  - データをユーザー データベースからエクスポートし、照合順序が master データベースおよび model データベースと同じ新しいテーブルにインポートします。

  - ユーザー データベースの照合順序と一致する照合順序を使用するようにシステム データベースを再構築します。 システム データベースを再構築する方法の詳細については、「[システム データベースの再構築](../databases/rebuild-system-databases.md)」を参照してください。

  - ユーザー テーブルを tempdb 内のテーブルに結合するストアド プロシージャを、ユーザー データベースの照合順序を使用して tempdb にテーブルを作成するように変更します。 これを行うには、次の例に示すように、一時テーブルの列定義に COLLATE database_default 句を追加します。
  
    ```
    CREATE TABLE #temp1 ( c1 int, c2 varchar(30) COLLATE database_default )
    ```

## <a name="see-also"></a>関連項目
  
 [サーバーの照合順序の設定または変更](../collations/set-or-change-the-server-collation.md)  

 [データベースの照合順序の設定または変更](../collations/set-or-change-the-database-collation.md)

 [列の照合順序の設定または変更](../collations/set-or-change-the-column-collation.md)
 
 [照合順序情報の表示](../collations/view-collation-information.md)    
  
  
