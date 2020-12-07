---
description: ODBC カーソル ライブラリ
title: ODBC カーソルライブラリ |Microsoft Docs
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
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e5e3a01633a19c4ae82596ba1e180c64bcce06c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487515"
---
# <a name="the-odbc-cursor-library"></a>ODBC カーソル ライブラリ
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 ブロックカーソルとスクロール可能なカーソルは、多くのアプリケーションに非常に便利です。 ただし、すべてのドライバーがブロックカーソルおよびスクロール可能なカーソルをサポートするわけではありません。 位置指定の update および delete ステートメントや **SQLSetPos**にも当てはまります。これについては、「データの更新」で説明されています。 このため、以前は Microsoft Data Access Components (MDAC) SDK に含まれていた Windows SDK の ODBC コンポーネントには、カーソルライブラリが含まれています。 カーソルライブラリは、Open Group Standard CLI 準拠レベルを満たすすべてのドライバーに対して、ブロック、静的カーソル、位置指定更新、および削除の各ステートメントと **SQLSetPos** を実装します。 カーソルライブラリは ODBC アプリケーションと共に再配布できます。詳細については、SDK のライセンス契約を参照してください。  
  
 カーソルライブラリを使用するには、アプリケーションがデータソースに接続する前に、SQL_ATTR_ODBC_CURSORS 接続属性を設定します。 カーソルライブラリの詳細については、「 [付録 F: ODBC カーソルライブラリ](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)」を参照してください。
