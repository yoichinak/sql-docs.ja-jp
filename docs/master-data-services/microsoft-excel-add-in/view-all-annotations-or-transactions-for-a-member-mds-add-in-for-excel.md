---
description: メンバーのすべての注釈またはトランザクションの表示 (Excel 用 MDS アドイン)
title: 注釈またはトランザクションの表示
ms.custom: microsoft-excel-add-in, seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: de90c81c-9e7f-4997-bf96-e22b97b2862c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 2dba27ae76c411f4ac095b9e8c38fa4987e32749
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100340377"
---
# <a name="view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel"></a>メンバーのすべての注釈またはトランザクションの表示 (Excel 用 MDS アドイン)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)]では、データの更新履歴を確認する必要があるときにデータ行 (メンバー) の注釈 (コメント) およびトランザクションを表示できます。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 この手順を実行するには  
  
-   MDS によって管理されるデータが含まれているアクティブなワークシートが必要です。  
  
-   エンティティ " **Transaction Log Type** " は、 **メンバー** または **属性** である必要があります。  
  
### <a name="to-view-annotations-or-transactions"></a>注釈またはトランザクションを表示するには  
  
1.  表示するトランザクションを含む行のセルをクリックします。  
  
2.  右クリックして表示されるメニューで、[ **トランザクションの表示** ] または [ **履歴の表示**] をクリックします。  
  
3.  **[トランザクションの表示]** ダイアログ ボックスにトランザクションの一覧が表示されます。 トランザクションに関連付けられたすべての注釈を表示するには、グリッド内の行をクリックします。  
  
## <a name="see-also"></a>参照  
 [概要: Excel からのデータのインポート (Excel 用 MDS アドイン)](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
