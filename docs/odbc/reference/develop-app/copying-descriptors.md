---
description: 記述子のコピー
title: 記述子のコピー |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90f3acb5ccb479ba5c1d1eb4c405a486f7032f3f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465870"
---
# <a name="copying-descriptors"></a>記述子のコピー
1つの記述子のフィールドを別の記述子にコピーするには、 **Sqlcopydesc** 関数を呼び出します。 フィールドはアプリケーション記述子または IPD にのみコピーできますが、IRD にはコピーできません。 フィールドは、任意の種類の記述子からコピーできます。 コピー元とコピー先の両方の記述子に対して定義されているフィールドのみがコピーされます。 記述子の割り当ての種類は変更できないため、 **Sqlcopydesc**では SQL_DESC_ALLOC_TYPE フィールドはコピーされません。 コピーされたフィールドは既存のフィールドを上書きします。  
  
 1つのステートメントハンドルを使用すると、別のステートメントハンドルで APD として機能することができます。 これにより、アプリケーションは、アプリケーションレベルでデータをコピーせずに、テーブル間で行をコピーできます。 これを行うには、テーブルのフェッチされた行を記述する行記述子を、INSERT ステートメントのパラメーターのパラメーター記述子として再利用します。 この操作を成功させるには、SQL_MAX_CONCURRENT_ACTIVITIES 情報の種類が1より大きい必要があります。
