---
description: 位置指定の UPDATE および DELETE ステートメントのシミュレート
title: 位置指定更新と Delete ステートメントをシミュレートする |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- row identifiers [ODBC]
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: b24ed59f-f25b-4646-a135-5f3596abc1a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 06f6faad1b5b6cb83616575ea8732cac98b88ed0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499815"
---
# <a name="simulating-positioned-update-and-delete-statements"></a>位置指定の UPDATE および DELETE ステートメントのシミュレート
データソースが位置指定の update および delete ステートメントをサポートしていない場合、ドライバーはこれらをシミュレートできます。 たとえば、ODBC カーソルライブラリは、位置指定の update および delete ステートメントをシミュレートします。 位置指定の update ステートメントと delete ステートメントをシミュレートするための一般的な方法は、配置されたステートメントを検索対象に変換することです。 この操作を行うには、 **WHERE current OF** 句を、現在の行を識別する検索対象の **where** 句に置き換えます。  
  
 たとえば、CustID 列は Customers テーブルの各行を一意に識別します。これは、位置指定 delete ステートメントです。  
  
```  
DELETE FROM Customers WHERE CURRENT OF CustCursor  
```  
  
 がに変換される可能性があります。  
  
```  
DELETE FROM Customers WHERE (CustID = ?)  
```  
  
 ドライバーは、 **WHERE**句で次のいずれかの*行識別子*を使用できます。  
  
-   テーブル内のすべての行を一意に識別する値を持つ列。 たとえば、SQL_BEST_ROWID を指定して **Sqlべき列** を呼び出すと、この目的を果たす最適な列または列のセットが返されます。  
  
-   すべての行を一意に識別するために、一部のデータソースによって提供される疑似列。 これらは、 **Sqlの列**を呼び出すことによって取得することもできます。  
  
-   一意のインデックス (使用可能な場合)。  
  
-   結果セット内のすべての列。  
  
 ドライバーが構築する **WHERE** 句でドライバーが使用する必要がある列は、ドライバーによって異なります。 データソースによっては、行識別子を特定するとコストがかかることがあります。 ただし、実行すると、シミュレートされたステートメントによって1行だけが更新または削除されるようになります。 基になる DBMS の機能によっては、行識別子を使用すると、設定に負荷がかかることがあります。 ただし、実行すると、シミュレートされたステートメントによって1行だけが更新または削除されるようになります。 通常、結果セット内のすべての列を使用するオプションは、より簡単に設定できます。 ただし、実行に時間がかかり、列で行が一意に識別されない場合、特に結果セットの選択リストに基になるテーブルに存在するすべての列が含まれていない場合は、行が誤って更新または削除される可能性があります。  
  
 ドライバーでサポートされている上記の戦略に応じて、アプリケーションでは、ドライバーが SQL_ATTR_SIMULATE_CURSOR statement 属性で使用する方法を選択できます。 アプリケーションでは、意図せずに行を更新または削除する危険性がありますが、結果セット内の列が結果セット内の各行を一意に識別できるようにすることで、このリスクを解消できます。 これにより、ドライバーはこれを行うための手間を省くことができます。  
  
 ドライバーは、行識別子を使用するように選択すると、結果セットを作成する **SELECT FOR UPDATE** ステートメントをインターセプトします。 選択リスト内の列が行を効果的に識別しない場合、ドライバーは選択リストの末尾に必要な列を追加します。 一部のデータソースには、Oracle の ROWID 列など、常に行を一意に識別する1つの列があります。このような列が使用可能な場合、ドライバーはこれを使用します。 それ以外の場合、ドライバーは**from**句内の各テーブルに対して**Sql独特な列**を呼び出して、各行を一意に識別する列の一覧を取得します。 この手法の結果として発生する一般的な制限は、 **from** 句に複数のテーブルがある場合にカーソルシミュレーションが失敗することです。  
  
 ドライバーが行を識別する方法に関係なく、通常は**SELECT FOR update**ステートメントから**for update**句を除去してから、データソースに送信します。 **FOR UPDATE OF**句は、位置指定の update および delete ステートメントでのみ使用されます。 配置された update ステートメントおよび delete ステートメントをサポートしていないデータソースは、通常はサポートしていません。  
  
 配置された update ステートメントまたは delete ステートメントを実行するためにアプリケーションが送信すると、ドライバーは **WHERE CURRENT OF** 句を行識別子を含む **where** 句に置き換えます。 これらの列の値は、 **WHERE** 句で使用する各列のドライバーによって保持されているキャッシュから取得されます。 ドライバーは、 **where** 句を置き換えると、ステートメントをデータソースに送信して実行します。  
  
 たとえば、アプリケーションが次のステートメントを送信して結果セットを作成するとします。  
  
```  
SELECT Name, Address, Phone FROM Customers FOR UPDATE OF Phone, Address  
```  
  
 アプリケーションで一意性の保証を要求するように SQL_ATTR_SIMULATE_CURSOR を設定している場合、行を一意に識別する擬似列をデータソースが提供していない場合、ドライバーは Customers テーブルに対して **SqlCustID 列** を呼び出し、select リストに追加して、 **for UPDATE of** 句を取り除きます。  
  
```  
SELECT Name, Address, Phone, CustID FROM Customers  
```  
  
 アプリケーションで一意性の保証が要求されていない場合、ドライバーは **FOR UPDATE of** 句のみを除去します。  
  
```  
SELECT Name, Address, Phone FROM Customers  
```  
  
 たとえば、アプリケーションが結果セットをスクロールして次の位置指定更新ステートメントを実行するとします。ここで、Cust は結果セットのカーソルの名前です。  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust  
```  
  
 アプリケーションで一意性の保証が要求されていない場合は、ドライバーによって **where** 句が置き換えられ、CustID パラメーターがキャッシュ内の変数にバインドされます。  
  
```  
UPDATE Customers SET Address = ?, Phone = ? WHERE (CustID = ?)  
```  
  
 アプリケーションで一意性の保証が要求されていない場合は、ドライバーによって **where** 句が置き換えられ、この句の Name、Address、および Phone パラメーターがキャッシュ内の変数にバインドされます。  
  
```  
UPDATE Customers SET Address = ?, Phone = ?  
   WHERE (Name = ?) AND (Address = ?) AND (Phone = ?)  
```
