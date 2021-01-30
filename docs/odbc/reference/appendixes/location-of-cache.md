---
description: キャッシュの場所
title: キャッシュの場所 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 240d6162-4da6-4b1f-96c7-f379f4ecb16f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b500aa9b7955c91c6ca39b3f7f830b2022dc4a57
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99184366"
---
# <a name="location-of-cache"></a>キャッシュの場所
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 Microsoft では、ドライバーのカーソル機能を使用することをお勧めします。  
  
 カーソルライブラリは、メモリおよび Windows®の一時ファイルにデータをキャッシュします。 これにより、カーソルライブラリが使用可能なディスク領域によってのみ処理できる結果セットのサイズが制限されます。 一時ファイルは、キャッシュするデータがカーソルライブラリキャッシュの末尾に挿入された場合にセグメント境界を越える場合に使用されます。 キャッシュに格納されるデータは、キャッシュ内の最後に保存されたデータブロックの代わりに追加されます。 最後に保存されたデータブロックは一時ファイルに保存されます。 電源障害などによってカーソルライブラリが異常終了した場合は、Windows の一時ファイルをディスクに残しておくことができます。 これらの名前は ~ CTT *nnnn*.tmp で、現在のディレクトリに作成されます。  
  
> [!NOTE]  
>  Microsoft®® WindowsNT のカーソルライブラリが、読み取り専用共有またはコンパクトディスク (Microsoft Foundation Class ライブラリサンプルなど) からアプリケーションを実行しているときに、現在のディレクトリの一時ファイルにデータをキャッシュしようとすると、SQLSTATE HY000 (ファイルバッファーを作成するための一般的な Error-Unable) が返されます。
