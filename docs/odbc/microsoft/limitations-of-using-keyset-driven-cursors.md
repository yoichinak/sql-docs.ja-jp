---
description: キーセット ドリブン カーソルの使用に関する制限
title: キーセットドリブンカーソルの使用に関する制限事項 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], cursors
- keyset-driven cursors [ODBC]
ms.assetid: 59d86fed-387c-4719-9550-36343e74da44
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 611bc032c51760742e5dce4dfbd8e1fa4fe33d0f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483475"
---
# <a name="limitations-of-using-keyset-driven-cursors"></a>キーセット ドリブン カーソルの使用に関する制限
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 クエリ対象のテーブルに対して1つの ROWID 列を取得できる必要があります。 キーセットドリブンカーソルは、DISTINCT、GROUP BY、UNION、INTERSECT、またはマイナス句を含む結合、クエリ、またはステートメントでは使用できません。  
  
 また、アプリケーションでテーブルの別名が使用されている場合、キーセットドリブンカーソルは機能しません。順方向専用または静的カーソルの種類が必要です。 テーブルの別名を持つ keyset カーソルの種類を使用すると、次のエラーが発生します。 "[Microsoft] [ODBC driver for Oracle] では、join ではキーセットドリブンカーソルを使用できません。 union、intersect、またはマイナスまたは読み取り専用の結果セットを使用することはできません。  
  
> [!NOTE]  
>  Oracle は、Oracle サーバーに送信される SQL ステートメントをドライバーが処理する方法によって、内部的に次のエラーメッセージを返します。 "ORA-00964: テーブル名がリストから取得されていません。"
