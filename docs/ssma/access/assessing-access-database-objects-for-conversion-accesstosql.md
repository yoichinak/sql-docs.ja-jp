---
description: 変換のためのアクセスデータベースオブジェクトの評価 (アクセス許可 Sql)
title: 変換のためのアクセスデータベースオブジェクトを評価する (アクセス可能な Sql) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- assessing SQL
- assessing syntax
- assessment reports
- creating assessment reports
- estimating migration effort
- reports
- SQL, assessing
- syntax, assessing
ms.assetid: 8b9e23d6-da62-437a-8c05-8ad2628b9441
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 6bf9144249bc8707bce9c812da19a07bacc43c68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418608"
---
# <a name="assessing-access-database-objects-for-conversion-accesstosql"></a>変換のためのアクセスデータベースオブジェクトの評価 (アクセス許可 Sql)
オブジェクトを読み込み、データをまたは SQL Azure に移行する前に、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 移行が成功する量と、変換にかかる時間を決定する必要があります。 SSMA では、評価レポートを作成して、正常に変換されたオブジェクトの割合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または移行を実行するための構文と時間の推定 SQL Azure を示すことができます。 SSMA では、変換エラーの原因となった特定の問題を確認することもできます。  
  
## <a name="creating-assessment-reports"></a>評価レポートの作成  
評価レポートを作成すると、SSMA は、選択した Access データベースオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] または SQL Azure 構文に変換し、結果を表示します。  
  
**評価レポートを作成するには**  
  
1.  [Access Metadata Explorer] で、評価するデータベースを選択します。  
  
2.  個々のオブジェクトを省略するには、評価しないオブジェクトの横にあるチェックボックスをオフにします。  
  
3.  [ **データベース**] を右クリックし、[ **レポートの作成**] を選択します。  
  
    オブジェクトを右クリックし、[ **レポートの作成**] を選択して、個々のオブジェクトを分析することもできます。  
  
    SSMA は、ウィンドウの下部にあるステータスバーに進行状況を表示します。 出力ウィンドウが表示されている場合は、[出力] ウィンドウにメッセージも表示されます。  
  
評価が完了すると、[ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] アクセスの Migration Assistant: 評価レポート] ウィンドウが表示されます。  
  
## <a name="using-assessment-reports"></a>評価レポートの使用  
[評価レポート] ウィンドウには、エクスプローラー、詳細ウィンドウ、およびメッセージウィンドウの3つのペインがあります。  
  
-   [エクスプローラー] ペインでは、評価されたオブジェクトを参照できます。 このペインの項目をクリックすると、個々のテーブル、インデックス、およびキーにドリルダウンできます。  
  
-   詳細ペインには、選択したオブジェクトの変換統計が表示されます。  
  
-   メッセージペインには、変換のエラー、警告、および情報メッセージと、移行と個々のエラー修正の手順を実行するための時間の見積もりが表示されます。  
  
エラーを修正してから、評価レポートを再実行するか、スキーマを変換する必要があります。 エラーを見つけるには、[メッセージ] ウィンドウの [ **エラー** ] ボタンをクリックし、各エラーを展開して、エラーが発生したオブジェクトの一覧を表示します。 [メッセージ] ウィンドウでオブジェクトをクリックすると、そのオブジェクトのすべてのエラーと警告が詳細ウィンドウに表示されます。  
  
## <a name="next-step"></a>次の手順  
[Access データベース オブジェクトの変換](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>参照  
[Access データベースの SQL Server への移行](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
