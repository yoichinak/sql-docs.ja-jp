---
description: 行の状態の配列
title: 行の状態の配列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8067aaf8724a6634d165d53743cbd0ef2015f6bd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465635"
---
# <a name="row-status-array"></a>行の状態の配列
データに加えて、 **Sqlfetch** および **sqlfetchscroll** は、行セットの各行の状態を示す配列を返すことができます。 この配列は、SQL_ATTR_ROW_STATUS_PTR statement 属性を使用して指定します。 この配列は、アプリケーションによって割り当てられ、SQL_ATTR_ROW_ARRAY_SIZE statement 属性で指定された数の要素を持つ必要があります。 配列内の値は、 **Sqlbulkoperations**、 **sqlfetch**、 **Sqlbulkoperations**、および SQLSetPos によって設定され **ます。** 値は、行の状態と、その状態が最後にフェッチされてから変更されたかどうかを示します。  
  
|行の状態の配列値|説明|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|行は正常にフェッチされましたが、最後にフェッチされてから変更されていません。|  
|SQL_ROW_SUCCESS_WITH_INFO|行は正常にフェッチされましたが、最後にフェッチされてから変更されていません。 ただし、行に関する警告が返されました。|  
|SQL_ROW_ERROR|行のフェッチ中にエラーが発生しました。|  
|SQL_ROW_UPDATED|行は正常にフェッチされ、最後にフェッチされてから更新されました。 行が再度フェッチされるか、 **SQLSetPos**によって更新されると、その状態が新しい状態に変わります。<br /><br /> 一部のドライバーでは、データへの変更を検出できないため、この値を返すことができません。 ドライバーが refetched 行の更新を検出できるかどうかを判断するために、アプリケーションは SQL_ROW_UPDATES オプションを使用して **SQLGetInfo** を呼び出します。|  
|SQL_ROW_DELETED|行は最後にフェッチされてから削除されています。|  
|SQL_ROW_ADDED|行は **Sqlbulkoperations**によって挿入されました。 行が再度フェッチされた場合、または **SQLSetPos**によって更新された場合、その状態は SQL_ROW_SUCCESS になります。<br /><br /> この値は、 **sqlfetch** または **sqlfetchscroll**では設定されません。|  
|SQL_ROW_NOROW|行セットには、結果セットの末尾が重なっています。行の状態配列のこの要素にこれする行は返されませんでした。|
