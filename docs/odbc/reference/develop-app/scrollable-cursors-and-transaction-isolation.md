---
description: スクロール可能なカーソルとトランザクション分離
title: スクロール可能なカーソルとトランザクション分離 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- scrollable cursors [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: f0216f4a-46e3-48ae-be0a-e2625e8403a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 790b2d0c4d80c821645c3a4360d1295cc55a8a4e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476504"
---
# <a name="scrollable-cursors-and-transaction-isolation"></a>スクロール可能なカーソルとトランザクション分離
次の表に、変更の可視性を制御する要因を示します。  
  
|変更者:|可視性は次に依存します。|  
|----------------------|----------------------------|  
|カーソル|カーソルの種類、カーソルの実装|  
|同じトランザクション内の他のステートメント|カーソルの種類|  
|他のトランザクション内のステートメント|カーソルの種類、トランザクション分離レベル|  
  
 これらの要因を次の図に示します。  
  
 ![変化の見え方を規定する要因](../../../odbc/reference/develop-app/media/pr23.gif "pr23")  
  
 次の表は、それぞれのカーソルの種類が、それ自体、他のトランザクション内の他の操作、および他のトランザクションによって行われた変更を検出する機能をまとめたものです。 後者の変更の可視性は、カーソルの種類と、カーソルを含むトランザクションの分離レベルによって異なります。  
  
|カーソルのタイプ \ アクション|セルフ|独自<br /><br /> Txn|他<br /><br /> Txn<br /><br /> (RU [a])|他<br /><br /> Txn<br /><br /> (RC [a])|他<br /><br /> Txn<br /><br /> (RR [a])|他<br /><br /> Txn<br /><br /> (S [a])|  
|-------------------------|----------|-----------------|----------------------------------|----------------------------------|----------------------------------|---------------------------------|  
|静的|||||||  
|挿入|おそらく [b]|いいえ|いいえ|いいえ|いいえ|いいえ|  
|更新|おそらく [b]|いいえ|いいえ|いいえ|いいえ|いいえ|  
|削除|おそらく [b]|いいえ|いいえ|いいえ|いいえ|いいえ|  
|キーセット ドリブン|||||||  
|挿入|おそらく [b]|いいえ|いいえ|いいえ|いいえ|いいえ|  
|更新|はい|はい|はい|はい|いいえ|いいえ|  
|削除|おそらく [b]|はい|はい|はい|いいえ|いいえ|  
|動的|||||||  
|挿入|はい|はい|はい|はい|はい|いいえ|  
|更新|はい|はい|はい|はい|いいえ|いいえ|  
|削除|はい|はい|はい|はい|いいえ|いいえ|  
  
 [a] かっこ内の文字は、カーソルを含むトランザクションの分離レベルを示します。(変更が加えられた) 他のトランザクションの分離レベルは無関係です。  
  
 RU: コミットされていない読み取り  
  
 RC: Read committed  
  
 RR: Repeatable read  
  
 S: Serializable  
  
 [b] は、カーソルがどのように実装されているかによって異なります。 このような変更をカーソルが検出できるかどうかは、 **SQLGetInfo**の SQL_STATIC_SENSITIVITY オプションを使用して報告されます。
