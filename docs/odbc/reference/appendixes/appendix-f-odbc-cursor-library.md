---
description: '付録 F: ODBC カーソル ライブラリ'
title: '付録 F: ODBC カーソルライブラリ |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- cursor library [ODBC]
ms.assetid: a03084df-4e48-48ef-917d-4a3fae48a605
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 325c7cdc5d2fb185ef3dbd2500a20230d90193bf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411428"
---
# <a name="appendix-f-odbc-cursor-library"></a>付録 F: ODBC カーソル ライブラリ
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 ODBC カーソルライブラリ (Odbccr32.dll) は、レベル1の API 準拠レベルに準拠しているすべてのドライバーのスクロール可能なカーソルをブロックし、開発者がそのアプリケーションやドライバーを使用して再配布することができます。 カーソルライブラリでは、 **SELECT** ステートメントによって生成される結果セットの位置指定の update および delete ステートメントもサポートされています。 静的カーソルと順方向専用カーソルのみがサポートされていますが、カーソルライブラリは多くのアプリケーションのニーズを満たしています。 さらに、パフォーマンスを向上させることができます。特に、サイズの小さいサイズから中規模の結果セットの場合や、適切なカーソルサポートがないアプリケーションの場合に適しています。  
  
 カーソルライブラリは、ドライバーマネージャーとドライバーの間に存在するダイナミックリンクライブラリ (DLL) です。 アプリケーションが関数を呼び出すと、ドライバーマネージャーはカーソルライブラリ内の関数を呼び出します。この関数は、関数を実行するか、指定されたドライバーで関数を呼び出します。 特定の接続では、アプリケーションは、カーソルライブラリを常に使用するかどうかを指定します。これは、ドライバーがスクロール可能なカーソルをサポートしていない場合、または使用されない場合に使用されます。  
  
 カーソルライブラリはドライバーマネージャーにドライバーとして表示されます。 ドライバーマネージャーと ODBC 2.x*ドライバーの*間にカーソルライブラリが存在する場合、カーソルライブラリは odbc *2.x ドライバーと*して表示されます。 ドライバーマネージャーと ODBC 3.x*ドライバーの*間にカーソルライブラリが存在する場合、カーソルライブラリは odbc *2.x ドライバーと*して表示されます。 カーソルライブラリによって実行される動作は、使用しているドライバーのバージョンによって異なります。バインドオフセットは例外であり、ODBC *2.x と odbc* 3.x の両方 *のドライバーで* サポートされています。  
  
 **Sqlfetch**および**sqlfetchscroll**にブロックカーソルを実装するには、カーソルライブラリがドライバーで**sqlfetch**を繰り返し呼び出します。 スクロールを実装するために、メモリとディスクファイルに取得したデータをキャッシュします。 アプリケーションが新しい行セットを要求すると、カーソルライブラリはドライバーまたはキャッシュから必要に応じてその行セットを取得します。  
  
 位置指定の update ステートメントと delete ステートメントを実装するために、カーソルライブラリは、行の各バインド列のキャッシュされた値を指定する**WHERE**句を使用して**update**ステートメントまたは**delete**ステートメントを構築します。 位置指定の update ステートメントを実行すると、カーソルライブラリは、行セットバッファーの値からキャッシュを更新します。  
  
 ODBC カーソルライブラリの詳細については、この付録の次のセクションを参照してください。  
  
-   [ODBC カーソル ライブラリの使用](../../../odbc/reference/appendixes/using-the-odbc-cursor-library.md)  
  
-   [位置指定更新と Delete ステートメントの実行](../../../odbc/reference/appendixes/executing-positioned-update-and-delete-statements.md)  
  
-   [カーソル ライブラリのコード例](../../../odbc/reference/appendixes/cursor-library-code-example.md)  
  
-   [実装に関するメモ](../../../odbc/reference/appendixes/implementation-notes.md)  
  
-   [ODBC カーソル ライブラリのエラー コード](../../../odbc/reference/appendixes/odbc-cursor-library-error-codes.md)
