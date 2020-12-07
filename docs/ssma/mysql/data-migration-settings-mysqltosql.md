---
description: データ移行の設定 (MySQLToSQL)
title: データ移行の設定 (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9c396df4-5676-4f32-9c57-70d4f15f9b7a
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 3bc5427d17a8678e81ee148d247d743bda9d53ff
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/13/2020
ms.locfileid: "91988718"
---
# <a name="data-migration-settings-mysqltosql"></a>データ移行の設定 (MySQLToSQL)
  
## <a name="data-migration-settings"></a>データの移行設定  
**データ移行設定** を使用すると、ユーザーはデータ移行のためのカスタムクエリを作成できます。  
  
-   このタブは、[プロジェクトの設定] で [**非表示**] に設定した場合に、[**拡張データ移行オプション**] が [**表示**] に設定され、非表示になるときに使用できます。 プロジェクトの移行設定の詳細については、「 [プロジェクトの設定 (移行)](./project-settings-migration-mysqltosql.md) 」を参照してください。  
  
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
[MySQL データの SQL Server/SQL Azure への移行](./migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
