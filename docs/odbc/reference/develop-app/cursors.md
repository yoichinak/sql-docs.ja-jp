---
description: カーソル (ODBC)
title: カーソル (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- forward-only cursors [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], about cursors
- cursors [ODBC]
- fetches [ODBC], cursors
- result sets [ODBC], fetching
- block cursors [ODBC]
ms.assetid: 0b114352-3c63-4d33-9220-182ede90e4aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10dbd2517c29bcd02d1d39abe0b2caec1bf03312
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429404"
---
# <a name="odbc-cursors"></a>ODBC カーソル
アプリケーションは *カーソル*を使用してデータをフェッチします。 カーソルは、結果セットとは異なります。結果セットは、特定の検索条件に一致する行のセットです。一方、カーソルは、それらの行をアプリケーションに返すソフトウェアです。 データベースに適用される名前 *カーソル* 。これは、コンピューターターミナルの点滅カーソルから発生することがあります。 カーソルが画面上の現在位置を示し、型指定された単語が次に表示されるのと同様に、結果セットのカーソルは結果セット内の現在の位置と、次に返される行を示します。  
  
 ODBC のカーソルモデルは、embedded SQL のカーソルモデルに基づいています。 これらのモデルの注目すべき点の1つは、カーソルを開く方法です。 Embedded SQL では、カーソルを使用する前に、明示的に宣言して開いておく必要があります。 ODBC では、結果セットを作成するステートメントが実行されると、カーソルが暗黙的に開かれます。 カーソルが開かれると、結果セットの最初の行の前に配置されます。 Embedded SQL と ODBC の両方で、アプリケーションの使用が終了したら、カーソルを閉じる必要があります。  
  
 カーソルの特性は異なります。 *前方参照専用カーソル*と呼ばれる最も一般的な種類のカーソルは、結果セットの前方にのみ移動できます。 前の行に戻るには、アプリケーションがカーソルを閉じてから再度開き、必要な行に到達するまで結果セットの先頭から行を読み取る必要があります。 順方向専用カーソルは、結果セットを通過するための高速なメカニズムを提供します。  
  
 前方参照専用カーソルは、画面ベースのアプリケーションではあまり役に立ちませんが、ユーザーはデータを前後にスクロールします。 このようなアプリケーションでは、結果セットを1回読み取り、データをローカルにキャッシュし、スクロール自体を実行することで、順方向専用カーソルを使用できます。 ただし、これは少量のデータでのみ機能します。 より良い解決策は、スクロール可能なカーソルを使用することです。これにより *、* 結果セットへのランダムアクセスが提供されます。 このようなアプリケーションでは、*ブロックカーソル*と呼ばれるものを使用して、一度に複数行のデータをフェッチすることでパフォーマンスを向上させることもできます。 ブロックカーソルの詳細については、「 [ブロックカーソルの使用](../../../odbc/reference/develop-app/using-block-cursors.md)」を参照してください。  
  
 順方向専用カーソルは ODBC の既定のカーソルの種類です。次のセクションで説明します。 ブロックカーソルとスクロール可能なカーソルの詳細については、「 [ブロックカーソル](../../../odbc/reference/develop-app/block-cursors.md) と [スクロール](../../../odbc/reference/develop-app/scrollable-cursors.md)可能なカーソル」を参照してください。  
  
> [!IMPORTANT]  
>  **SQLEndTran**を明示的に呼び出すか、自動コミットモードで動作することにより、トランザクションをコミットまたはロールバックすると、一部のデータソースによって、接続上のすべてのステートメントのすべてのカーソルが閉じられます。 詳細については、「 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 関数の説明」の SQL_CURSOR_COMMIT_BEHAVIOR と SQL_CURSOR_ROLLBACK_BEHAVIOR の属性を参照してください。
