---
description: データ移行の設定 (DB2ToSQL)
title: データ移行の設定 (DB2ToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 573e673e-a194-4cb2-9aba-aaac6e1a225c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 0646fc033f73134a4dfcba62e574ba08e378b9cc
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91984878"
---
# <a name="data-migration-settings-db2tosql"></a>データ移行の設定 (DB2ToSQL)
  
## <a name="data-migration-settings"></a>データの移行設定  
**データ移行設定** を使用すると、ユーザーはデータ移行のためのカスタムクエリを作成できます。  
  
-   このタブは、[プロジェクトの設定] で [**非表示**] に設定した場合に、[**拡張データ移行オプション**] が [**表示**] に設定され、非表示になるときに使用できます。 プロジェクトの移行設定の詳細については、「 [プロジェクトの設定 (移行)](./project-settings-migration-db2tosql.md) 」を参照してください。  
  
-   カスタム SQL ステートメントの解析は、テーブルノードの [ **データ移行の設定** ] タブで実装されます。  
  
-   **データ移行設定**可視化で使用できる2つのチェックボックスを次に示します。  
  
    1.  SQL Server テーブルの切り捨て  
  
    2.  カスタム選択の使用  
  
1.  **SQL Server テーブルの切り捨て:**  
     このオプションを使用すると、移行されたデータを対象のデータベースに明確に表示できます。  
  
    -   既定では、このテキストボックスはオンになっています。  
  
    -   このテキストボックスがオフの場合、移行されるデータは、ターゲットデータベースの既存のデータに追加されます。  
  
2.  **カスタム選択を使用する:**  
     このオプションを使用すると、ユーザーは現在の **select** ステートメントを変更できます (**select** ステートメントを使用すると、ターゲットデータベースに表示するデータをユーザーが選択できます)。  
  
    1.  既定では、このテキストボックスはオフになっています。  
  
    2.  このテキストボックスがオンになっている場合は、ユーザーが現在の **select** ステートメントを変更できます。  
  
可視化には、次の2つのボタンが表示されます。  
  
-   **適用:** [ **適用** ] をクリックして、変更された設定を適用します。  
  
-   **取り消し:** 変更が行われる前に設定を復元するには、[ **キャンセル** ] をクリックします。  
  
## <a name="see-also"></a>参照  
[DB2 データの SQL Server への移行](./migrating-db2-data-into-sql-server-db2tosql.md)  
