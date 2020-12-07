---
description: 列データの長さ
title: 列データの長さ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96194272d6b291da53986330199d9c7972cef8f1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429664"
---
# <a name="length-of-column-data"></a>列データの長さ
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 カーソルライブラリは、 **SQLBindCol**を使用して結果セットにバインドされた各長さ/インジケーターバッファーのバッファーをキャッシュに作成します。 位置指定の update または delete ステートメントをエミュレートするときに、これらのバッファー内の値を使用して **where** 句を構築します。 データソースからデータをフェッチするときと、位置指定の update ステートメントを実行するときに、これらのバッファーを行セットバッファーから更新します。  
  
 データバッファーの C 型が SQL_C_CHAR または SQL_C_BINARY で、長さ/インジケーターの値が SQL_NTS 場合、データの文字列の長さは長さ/インジケーターバッファーに格納されます。  
  
> [!NOTE]  
>  対応する行セットバッファー内の **StrLen_or_IndPtr* が SQL_DATA_AT_EXEC または SQL_LEN_DATA_AT_EXEC マクロの結果である場合、カーソルライブラリは列のキャッシュを更新しません。
