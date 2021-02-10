---
description: データの取得
title: データの取得 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, getting data
ms.assetid: 3931e7ec-f66b-4d5d-aad3-c4bf12e8b154
author: rothja
ms.author: jroth
ms.openlocfilehash: 9f53092d1677afd0c6eec25c2bdcde6f75b47657
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100037422"
---
# <a name="getting-data"></a>データの取得
[Ado の基礎](./ado-fundamentals.md)、および特に [HelloData](./hellodata-a-simple-ado-application.md) の例では、ado アプリケーションの作成に関連する4つの主要な操作 (データの取得、データの検査、データの編集、データの更新) が導入されました。 ここでは、データの取得について詳しく説明します。  
  
 基本レベルでは、いくつかの ADO オブジェクトがデータ取得操作に寄与します。 まず、ADO **Connection** オブジェクトを使用してデータソースに接続する必要があります。 次に、ADO **コマンド** オブジェクトを使用して、データソースに命令を渡します。 最後に、ほとんどの場合、ADO **レコードセット** オブジェクトのデータを受け取ります。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [データ ソースへの接続](./connecting-to-data-sources.md)  
  
-   [準備とコマンドの実行](./preparing-and-executing-commands.md)  
  
-   [結果の受信](./receiving-results.md)