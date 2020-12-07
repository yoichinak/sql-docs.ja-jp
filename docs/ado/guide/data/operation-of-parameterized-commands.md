---
description: パラメーター化コマンドの操作
title: パラメーター化されたコマンドの操作 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
author: rothja
ms.author: jroth
ms.openlocfilehash: 91fe315304cc2be0ccfb8c638665ce699c75e248
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980173"
---
# <a name="operation-of-parameterized-commands"></a>パラメーター化コマンドの操作
大きな子 **レコードセット**で作業している場合は、特に親 **レコード**セットのサイズとは異なりますが、いくつかの子チャプターにのみアクセスする必要がある場合は、パラメーター化されたコマンドを使用する方が効率的です。  
  
 パラメーター化されてい *ないコマンド* は、親と子の両方の **レコードセット**を取得し、チャプター列を親に追加して、親の各行に関連する子のチャプターに参照を割り当てます。  
  
 *パラメーター化*されたコマンドは親**レコードセット**全体を取得しますが、チャプター列にアクセスしたときにはチャプター**レコードセット**のみを取得します。 このような取得方法の違いにより、パフォーマンスが大幅に向上する可能性があります。  
  
 たとえば、次のように指定できます。  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 親テーブルと子テーブルには、共通の列名、 *cust_id*があります。 この *子コマンド* には、"?" というプレースホルダーがあります。ここで、関連句は "...パラメーター 0 ")。  
  
> [!NOTE]
>  PARAMETER 句は、shape コマンドの構文にのみ関連します。 ADO [パラメーター](../../reference/ado-api/parameter-object.md) オブジェクトまたは [Parameters](../../reference/ado-api/parameters-collection-ado.md) コレクションに関連付けられていません。  
  
 パラメーター化された shape コマンドを実行すると、次の処理が行われます。  
  
1.  *親コマンド*が実行され、Customers テーブルから親**レコードセット**が返されます。  
  
2.  チャプター列が親 **レコードセット**に追加されます。  
  
3.  親行のチャプター列にアクセスした場合、 *子コマンド* は、パラメーターの値として cust_id を使用して実行されます。  
  
4.  手順3で作成したデータプロバイダー行セット内のすべての行を使用して、子 **レコードセット**を設定します。 この例では、Orders テーブルのすべての行で、cust_id が customer. cust_id の値と等しくなります。 既定では、親**レコードセット**へのすべての参照が解放されるまで、子**レコードセット**はクライアントにキャッシュされます。 この動作を変更するには、**レコードセット**の[動的プロパティ](../../reference/ado-api/ado-dynamic-property-index.md)**キャッシュの子行**を**False**に設定します。  
  
5.  取得した子行への参照 (つまり、子 **レコードセット**のチャプター) は、親 **レコードセット**の現在の行のチャプター列に配置されます。  
  
6.  別の行のチャプター列にアクセスすると、手順3-5 が繰り返されます。  
  
 既定では、" **子行のキャッシュ** " 動的プロパティは **True** に設定されています。 キャッシュの動作は、クエリのパラメーター値によって異なります。 1つのパラメーターを持つクエリでは、指定されたパラメーター値の子 **レコードセット** が、その値を持つ子の要求間でキャッシュされます。 その例を次のコードに示します。  
  
```  
SCmd = "SHAPE {select * from customer} " & _  
         "APPEND({select * from orders where cust_id = ?} " & _  
         "RELATE cust_id TO PARAMETER 0) AS chpCustOrder"  
Rst1.Open sCmd, Cnn1  
Set RstChild = Rst1("chpCustOrder").Value  
Rst1.MoveNext      ' Next cust_id passed to Param 0, & new rs fetched   
                   ' into RstChild.  
Rst1.MovePrevious  ' RstChild now holds cached rs, saving round trip.  
```  
  
 2つ以上のパラメーターを持つクエリでは、キャッシュされた子は、すべてのパラメーター値がキャッシュされた値と一致する場合にのみ使用されます。  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>パラメーター化されたコマンドと複合親子関係  
 パラメーター化コマンドを使用して等結合型階層のパフォーマンスを向上させるだけでなく、パラメーター化コマンドを使用して、より複雑な親子関係をサポートすることもできます。 たとえば、2つのテーブルを持つ簡単なリーグデータベースがあるとします。1つはチーム (team_id、team_name)、もう1つはゲーム (date、home_team、visiting_team) で構成されています。  
  
 パラメーター化されていない階層を使用する場合、各チームの子 **レコードセット** に完全なスケジュールが含まれるように、チームとゲームテーブルを関連付けることはできません。 ホームスケジュールまたは道路スケジュールを含むチャプターを作成できますが、両方を指定することはできません。 これは、関連付け句によって、フォーム (pc1 = cc1) と (pc2 = pc2) という形式の親子関係が制限されるためです。 このため、コマンドに "team_id を home_team に関連付ける"、team_id を visiting_team "にすると、チームが自身をプレイしていたゲームのみが表示されます。 必要なのは、"(team_id = home_team) または (team_id = visiting_team)" ですが、図形プロバイダーはまたは句をサポートしていません。  
  
 目的の結果を得るには、パラメーター化されたコマンドを使用します。 次に例を示します。  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 この例では、必要な結果を得るために、SQL の WHERE 句の柔軟性が向上しています。  
  
> [!NOTE]
>  WHERE 句を使用する場合、text、ntext、および image の SQL データ型をパラメーターで使用することはできません。また、次のようなエラーが発生 `Invalid operator for data type` します。  
  
## <a name="see-also"></a>参照  
 [データシェイプの例](./data-shaping-example.md)   
 [仮形の文法](./formal-shape-grammar.md)   
 [一般的な Shape コマンド](./shape-commands-in-general.md)