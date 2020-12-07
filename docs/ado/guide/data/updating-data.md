---
description: データの更新
title: データの更新 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], about data updates
- updating data [ADO], about updating data
ms.assetid: 6508e4e9-e33a-4dad-b340-5d632fd78a91
author: rothja
ms.author: jroth
ms.openlocfilehash: 417d03c66209a44110aff8d0c8e71845119049f1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979183"
---
# <a name="updating-data"></a>データの更新
更新の動作と機能は、更新モード (ロックの種類)、カーソルの種類、およびカーソルの場所に大きく依存します。  
  
 **AddNew**メソッドを呼び出した後、または既存のレコードのフィールド値を変更した後に、**レコードセット**オブジェクトの現在のレコードに加えた変更を保存するには、 **Update**メソッドを使用します。 **レコードセット**オブジェクトは更新をサポートしている必要があります。  
  
 **レコードセット**オブジェクトでバッチ更新がサポートされている場合は、 **UpdateBatch**メソッドを呼び出すまで、1つ以上のレコードに対して複数の変更をローカルにキャッシュできます。 現在のレコードを編集している場合、または **UpdateBatch** メソッドを呼び出したときに新しいレコードを追加している場合、ADO は **Update** メソッドを自動的に呼び出して、保留中の変更を現在のレコードに保存してから、バッチされた変更をプロバイダーに送信します。  
  
 **Update**メソッドまたは**UpdateBatch**メソッドを呼び出した後、現在のレコードは最新のままです。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [イミディエイト モード](../../../ado/guide/data/immediate-mode.md)  
  
-   [バッチ モード](../../../ado/guide/data/batch-mode.md)  
  
-   [トランザクション処理](../../../ado/guide/data/transaction-processing.md)
