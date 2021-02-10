---
description: カーソルとロックの特性
title: カーソルとロックの特性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
author: rothja
ms.author: jroth
ms.openlocfilehash: cecbdd12fd98e6f58d07cfe30c6c0b8a044ed15e
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100037689"
---
# <a name="cursor-and-lock-characteristics"></a>カーソルとロックの特性
カーソルの特性はプロバイダーの機能によって異なりますが、一般的に、次のような長所と短所がさまざまな種類のカーソルやロックに適用されます。  
  
|カーソルまたはロックの種類|長所|短所|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-リソース要件が不足しています|-後方にスクロールできません<br />-データの同時実行がありません|  
|**adOpenStatic**|-スクロール可能|-データの同時実行がありません|  
|**adOpenKeyset**|-データの同時実行<br />-スクロール可能|-より高いリソース要件<br />-切断されたシナリオでは使用できません|  
|**adOpenDynamic**|-高データ同時実行<br />-スクロール可能|-最大リソース要件<br />-切断されたシナリオでは使用できません|  
|**adLockReadOnly**|-リソース要件が不足しています<br />-拡張性が高い|-カーソルを使用して更新できないデータ|  
|**adLockBatchOptimistic**|-バッチ更新<br />-切断されたシナリオを許可します<br />-他のユーザーがデータにアクセスできる|-複数のユーザーが同時にデータを変更できます。|  
|**adLockPessimistic**|-ロック中に他のユーザーがデータを変更することはできません|-ロック中に他のユーザーがデータにアクセスできないようにします|  
|**adLockOptimistic**|-他のユーザーがデータにアクセスできる|-複数のユーザーが同時にデータを変更できます。|
