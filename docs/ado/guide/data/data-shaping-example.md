---
description: データ シェイプの例
title: データシェイプの例 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], about data shaping
ms.assetid: 1bfdcad4-52e1-45bc-ad21-783657ef0a44
author: rothja
ms.author: jroth
ms.openlocfilehash: b6d6310e27db65576aac3ed79e699200dfa31c18
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991443"
---
# <a name="data-shaping-example"></a>データ シェイプの例
次のデータシェイプコマンドは、Northwind データベースの**Customers**テーブルと**Orders**テーブルから階層**レコードセット**を作成する方法を示しています。  
  
```  
SHAPE {SELECT CustomerID, ContactName FROM Customers}   
APPEND ({SELECT OrderID, OrderDate, CustomerID FROM Orders} AS chapOrders   
RELATE customerID TO customerID)   
```  
  
 このコマンドを使用して**レコードセット**オブジェクトを開くと ( [Visual Basic データシェイプの例](./visual-basic-example-of-data-shaping.md)を参照)、 **Customers**テーブルから返されたレコードごとにチャプター (**chapOrders**) が作成されます。 この章は、 **Orders**テーブルから返された**レコードセット**のサブセットで構成されています。 **ChapOrders**章には、特定の顧客によって行われた注文に関するすべての要求された情報が含まれています。 この例では、" **OrderID**"、" **OrderDate**"、および **"CustomerID"** という3つの列で構成されています。  
  
 結果の整形された **レコードセット** の最初の2つのエントリは次のとおりです。  
  
|CustomerID|[ContactName]|OrderID|OrderDate|CustomerID|  
|----------------|-----------------|-------------|---------------|----------------|  
|ALFKI|マリア Ander|10643<br /><br /> 10692<br /><br /> 10702<br /><br /> 10835<br /><br /> 10952<br /><br /> 11011|1997-08-25<br /><br /> 1997-10-03<br /><br /> 1997-10-13<br /><br /> 1998-01-15<br /><br /> 1998-03-16<br /><br /> 1998-04-09|ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI<br /><br /> ALFKI|  
|ANATR|Ana Trujillo|10308<br /><br /> 10625<br /><br /> 10759<br /><br /> 10926|1996-09-18<br /><br /> 1997-08-08<br /><br /> 1997-11-28<br /><br /> 1998-03-04|ANATR<br /><br /> ANATR<br /><br /> ANATR<br /><br /> ANATR|  
  
 SHAPE コマンドで、APPEND を使用して、親**レコードセット**に関連する子**レコードセット**を作成します (前に説明した SHAPE キーワードの直後にある、プロバイダー固有のコマンドから返されます)、関連句。 親と子には、通常、少なくとも1つの共通の列があります。親の行の列の値は、子のすべての行の列の値と同じです。  
  
 図形コマンドを使用するもう1つの方法として、子**レコードセット**から親**レコードセット**を生成する方法があります。 子 **レコードセット** 内のレコードは、通常、by 句を使用してグループ化され、子の結果の各グループの親 **レコードセット** に1行が追加されます。 BY 句を省略した場合、子 **レコードセット** は1つのグループを形成し、親 **レコードセット** には1つの行だけが含まれます。 これは、子 **レコードセット**全体に対する "総計" 集計を計算する場合に便利です。  
  
 SHAPE command コンストラクトを使用すると、プログラミングによって整形された **レコードセット**を作成することもできます。 その後、プログラムによって、または適切なビジュアルコントロールを使用して、 **レコードセット** のコンポーネントにアクセスできます。 Shape コマンドは、他の ADO コマンドテキストと同様に発行されます。 詳細については、「 [Shape コマンド全般](./shape-commands-in-general.md)」を参照してください。  
  
 親 **レコードセット** がどのように形成されているかにかかわらず **、子レコードセットに**関連付けられたチャプター列が含まれます。 必要に応じて、親 **レコードセット** には、子行に対する集計 (SUM、MIN、MAX など) を含む列を含めることもできます。 親と子の両方の **レコードセット** は、 **レコードセット**内の行に式を含む列と、新しい列と最初に空になる列を持つことができます。  
  
 このセクションでは、次のトピックについて説明します。  
  
-   [Visual Basic のデータ シェイプの例](./visual-basic-example-of-data-shaping.md)