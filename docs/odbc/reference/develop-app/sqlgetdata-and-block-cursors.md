---
description: SQLGetData およびブロック カーソル
title: SQLGetData カーソルとブロックカーソル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- SQLGetData function [ODBC], block cursors
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 12599cdc-7725-4faf-bcae-e163ea0f5851
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f53358b2d4d8dfef1a5a820ed3943f07a584a595
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424494"
---
# <a name="sqlgetdata-and-block-cursors"></a>SQLGetData およびブロック カーソル
**SQLGetData** は1つの行の1つの列に対して動作し、複数の行のデータを含む配列をフェッチすることはできません。 これは、 **SQLGetData** の主な用途は、長いデータを部分的にフェッチすることであり、一度に複数の行に対してこれを行う理由はほとんどありません。  
  
 ブロックカーソルで **SQLGetData** を使用するには、アプリケーションはまず **SQLSetPos** を呼び出して、カーソルを1行に配置します。 次に、その行の列に対して **SQLGetData** を呼び出します。 ただし、この動作は省略可能です。 ドライバーがブロックカーソルで **SQLGetData** の使用をサポートしているかどうかを判断するために、アプリケーションは SQL_GETDATA_EXTENSIONS オプションを指定して **SQLGetInfo** を呼び出します。
