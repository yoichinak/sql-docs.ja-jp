---
description: SQLFetch (カーソル ライブラリ)
title: SQLFetch (カーソルライブラリ) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ce9da3c0c5b95be4336c58896b17b6ba5daf6443
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466004"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (カーソル ライブラリ)
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 このトピックでは、カーソルライブラリでの **Sqlfetch** 関数の使用について説明します。 **Sqlfetch**に関する一般的な情報については、「 [sqlfetch 関数](../../../odbc/reference/syntax/sqlfetch-function.md)」を参照してください。  
  
 カーソルライブラリを使用する場合、 **Sqlfetch** の呼び出しと **sqlfetchscroll** または **SQLExtendedFetch**の呼び出しを混在させることはできません。  
  
 **Sqlfetch**が呼び出され SQL_ATTR_ROW_ARRAY_SIZE が1より大きい値に設定されている場合、カーソルライブラリはその呼び出しをドライバーに渡します。 ドライバーが ODBC 2 の場合。*x* ドライバーでは、行セットのサイズは無視され、 **sqlfetch** を呼び出すと1行のデータが返されます。  
  
 カーソルライブラリが ODBC 2 で使用される場合はです。*x* ドライバーは、 **sqlfetch** が呼び出されるときに、バインドオフセット (SQL_ATTR_ROW_BIND_OFFSET_PTR statement 属性で定義されている) は使用されません。  
  
 カーソルライブラリが読み込まれると、アプリケーションは **Sqlfetch** を呼び出してブックマーク列をフェッチすることはできません。 カーソルライブラリは **Sqlfetch** の呼び出しをドライバーに渡しますが、ブックマークを有効にするための関数呼び出しとブックマーク列のバインドはカーソルライブラリによってインターセプトされます。
