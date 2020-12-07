---
title: ブレークポイントの位置の編集
description: Transact-SQL スクリプト ファイル内のブレークポイントをスクリプト内の別の場所または別のスクリプトに移動する方法について説明します。
titleSuffix: T-SQL debugger
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint location
ms.assetid: 5c28e411-0377-4210-a7ce-2a5c13dcdf74
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 22e94d5bd53287600458504834321106fa22a1ce
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036462"
---
# <a name="edit-a-breakpoint-location"></a>ブレークポイントの位置の編集

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

ブレークポイントの位置では、ブレークポイントを設定する [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト ファイル内の行や文字を指定します。 ブレークポイントの位置を編集して、ブレークポイントを別の位置や別のスクリプトに移動できます。

## <a name="editing-a-location"></a>位置の編集

ブレークポイントの位置を編集すると、ブレークポイントはヒット カウント、条件などの既存のすべてのプロパティと共に新しい位置に移動します。  

#### <a name="to-edit-a-breakpoint-location"></a>ブレークポイントの位置を編集するには

1. エディター ウィンドウで、ブレークポイント グリフを右クリックし、ショートカット メニューの **[場所]** をクリックします。  
  
     または  
  
     **[ブレークポイント]** ウィンドウで、ブレークポイント グリフを右クリックし、ショートカット メニューの **[場所]** をクリックします。  
  
2. **[ファイルのブレークポイント]** ダイアログ ボックスで、新しいファイルを指定するには **[ファイル]** 、新しい行を指定するには **[行]** 、行内の新しい場所を指定するには **[文字]** の各項目を編集します。 指定した新しいファイルがクエリ エディター ウィンドウで既に開いている場合は、ブレークポイントがそのエディター ウィンドウに移動します。 ファイルが開いていない場合は、新しいクエリ エディター ウィンドウが開き、そのファイルが読み込まれ、ブレークポイントが新しい位置に移動します。  
  
     **をデバッグする場合、** [元のバージョンと異なるソース コードを許可する] [!INCLUDE[tsql](../../includes/tsql-md.md)]オプションは無効です。  
  
## <a name="see-also"></a>参照

- [ヒット カウントの指定](./specify-a-hit-count.md)
- [ブレークポイント アクションの指定](./specify-a-breakpoint-action.md)
- [ブレークポイント条件の指定](./specify-a-breakpoint-condition.md)
- [ブレークポイント フィルターの指定](./specify-a-breakpoint-filter.md)