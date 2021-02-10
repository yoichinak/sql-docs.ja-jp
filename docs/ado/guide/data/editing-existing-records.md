---
description: 既存のレコードの編集
title: 既存のレコードの編集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
author: rothja
ms.author: jroth
ms.openlocfilehash: 031d819e2c8eed63b9b8ff42aa58fb8e998a4273
ms.sourcegitcommit: 917df4ffd22e4a229af7dc481dcce3ebba0aa4d7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/10/2021
ms.locfileid: "100037502"
---
# <a name="editing-existing-records"></a>既存のレコードの編集
既存のレコードを編集するには、編集する行に移動し、変更するフィールドの [ **値** ] プロパティを変更します。 **フィールド** オブジェクトの **値** プロパティの詳細については、「[データの検査](./examining-data.md)」を参照してください。 カーソルの種類によっては、 **Update** または **UpdateBatch** を使用して、変更をデータソースに送り返すことができます。 詳細については、「 [データの更新と永続](./updating-and-persisting-data.md)化」を参照してください。  
  
 通常、ストアドプロシージャではカーソルを作成する必要がないので、コマンドオブジェクトを使用してストアドプロシージャを使用し、更新を実行したり、他の操作を実行したりする方が効率的です。 カーソルの詳細については、「 [カーソルとロック](./understanding-cursors-and-locks.md)について」を参照してください。