---
description: ブロック カーソル
title: ブロックカーソル |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5dece0e3ecfc5ef4f3116361a202cfa2d10863ed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476824"
---
# <a name="block-cursors"></a>ブロック カーソル
多くのアプリケーションでは、ネットワーク経由でデータを取り込むために膨大な時間を費やしています。 この時間の一部は、実際にネットワーク経由でデータを取り込むために費やされています。また、データの行を要求するためにドライバーによって行われる呼び出しなど、ネットワークのオーバーヘッドにも費やされます。 アプリケーションで1つ以上の行を返すことができる *ブロック* または *fat* *カーソルを* 効率的に使用する場合は、後者の時間を短縮できます。  
  
 アプリケーションには、常にブロックカーソルを使用するオプションがあります。 一度に1行しかフェッチできないデータソースでは、ドライバーでブロックカーソルをシミュレートする必要があります。 これを行うには、複数の単一行フェッチを実行します。 これによってパフォーマンスが向上する可能性はほとんどありませんが、アプリケーションの営業案件が開かれます。 そのようなアプリケーションでは、Dbms によってブロックカーソルがネイティブで実装され、それらの Dbms に関連付けられているドライバーがそれらを公開するため、パフォーマンスが向上します。  
  
 ブロックカーソルを含む単一のフェッチで返される行は、 *行セット*と呼ばれます。 行セットと結果セットを混同しないようにすることが重要です。 結果セットはデータソースで保持され、行セットはアプリケーションバッファーに保持されます。 結果セットは固定されていますが、行セットは、新しい行セットがフェッチされるたびに位置と内容を変更します。 従来の SQL 順方向専用カーソルなどの単一行カーソルが現在の行を指している場合と同様に、ブロックカーソルは *現在の行*と考えることができる行セットを指します。  
  
 複数の行がフェッチされたときに1つの行に対して操作を実行するには、まず現在の行である行をアプリケーションで指定する必要があります。 現在の行は、 **SQLGetData** および位置指定の update および delete ステートメントの呼び出しに必要です。 ブロックカーソルが最初に行セットを返すと、現在の行が行セットの最初の行になります。 現在の行を変更するには、アプリケーションは **SQLSetPos** または **sqlbulkoperations** (ブックマークによって更新) を呼び出します。 次の図は、結果セット、行セット、現在の行、行セットカーソル、およびブロックカーソルの関係を示しています。 詳細については、このセクションで後述 [する「ブロックカーソルの使用](../../../odbc/reference/develop-app/using-block-cursors.md)」および「 [更新と Delete ステートメントの配置](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md) 」および「 [SQLSetPos によるデータの更新](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)」を参照してください。  
  
 ![次、前、最初、および最後の行セットのフェッチ](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 カーソルがブロックカーソルであるかどうかは、スクロール可能かどうかに関係ありません。 たとえば、レポートアプリケーションでの作業のほとんどは、行の取得と印刷に費やされます。 このため、順方向専用のブロックカーソルを使用して、最速で動作します。 この例では、順方向専用カーソルを使用して、スクロール可能なカーソルの費用を回避し、ブロックカーソルを使用してネットワークトラフィックを削減します。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ブロック カーソルで使用するためのバインディング列](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [ブロック カーソルの使用](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [行の状態の配列](../../../odbc/reference/develop-app/row-status-array.md)
