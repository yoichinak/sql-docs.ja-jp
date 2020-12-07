---
description: バインドされた記述子レコード
title: バインドされた記述子レコード |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcf88374967b5a9d8426d16c9e92c06e4eef32cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476804"
---
# <a name="bound-descriptor-records"></a>バインドされた記述子レコード
アプリケーションが記述子レコードの SQL_DESC_DATA_PTR フィールドを設定して、そのレコードに null 値が含まれないようにすると、レコードは " *バインド*" と呼ばれます。  
  
 記述子が APD の場合、バインドされた各レコードはバインドされたパラメーターを構成します。 入力パラメーターの場合、アプリケーションは、ステートメントを実行する前に、SQL ステートメントの動的パラメーターマーカーごとにパラメーターをバインドする必要があります。 出力パラメーターの場合、アプリケーションでパラメーターをバインドする必要はありません。  
  
 記述子が、データベースデータの行を記述する場合は、バインドされた各レコードがバインド列を構成します。
