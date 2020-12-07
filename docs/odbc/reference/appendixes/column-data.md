---
description: 列のデータ
title: 列のデータ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 0425818c-9469-493f-9e3c-fc03d9411c5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5f4ea57de9dfefd21b6d71bb3b248d5aed5dd50d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449004"
---
# <a name="column-data"></a>列のデータ
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 カーソルライブラリは、 **SQLBindCol**を使用して結果セットにバインドされたデータバッファーごとに、バッファーをキャッシュに作成します。 位置指定の update または delete ステートメントをエミュレートするときに、これらのバッファー内の値を使用して **where** 句を作成します。 データソースからデータをフェッチするときと、位置指定の update ステートメントを実行するときに、これらのバッファーを行セットバッファーから更新します。  
  
 カーソルライブラリは、行セットバッファーからキャッシュを更新すると、 **SQLBindCol**で指定された C データ型に従ってデータを転送します。 たとえば、行セットバッファーの C データ型が SQL_C_SLONG 場合、カーソルライブラリは4バイトのデータを転送します。この値が SQL_C_CHAR で、 *bufferlength* が10の場合、カーソルライブラリは10バイトのデータを転送します。 カーソルライブラリでは、転送されるデータに対して型チェックや変換は実行されません。  
  
> [!NOTE]  
>  対応する行セットバッファー内の **StrLen_or_IndPtr* が SQL_DATA_AT_EXEC または SQL_LEN_DATA_AT_EXEC マクロの結果である場合、カーソルライブラリは列のキャッシュを更新しません。  
  
 列を更新すると、データソースは固定長の文字データを埋め込み、必要に応じて固定長のバイナリデータをゼロ埋め込みます。 たとえば、データソースは、"smith" を CHAR (10) 列に "Smith" として格納します。 カーソルライブラリでは、配置された update ステートメントの実行後に、このデータをキャッシュにコピーするときに、行セットバッファー内のデータが空白になることはありません。 そのため、アプリケーションで、カーソルライブラリのキャッシュ内の値が空白またはゼロで埋め込まれている必要がある場合は、位置指定の update ステートメントを実行する前に、行セットバッファー内の値を空白またはゼロで埋め込む必要があります。
