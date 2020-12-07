---
description: ドライバー
title: Drivers |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC]
- drivers [ODBC], about drivers
ms.assetid: d6795d92-877e-44e1-b7d5-2ff2fd3989bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 81e8989fc178728e687baa13b37e6055692d9413
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494595"
---
# <a name="drivers"></a>ドライバー
*ドライバー* は、ODBC API の関数を実装するライブラリです。 各は特定の DBMS に固有です。たとえば、Oracle のドライバーは、Informix DBMS のデータに直接アクセスすることはできません。 ドライバーは、基になる Dbms の機能を公開します。DBMS でサポートされていない機能を実装する必要はありません。 たとえば、基になる DBMS が外部結合をサポートしていない場合、どちらの場合もドライバーは必要ありません。 唯一の重要な例外は、Xbase などのスタンドアロンデータベースエンジンを搭載していない Dbms のドライバーは、少なくとも最小量の SQL をサポートするデータベースエンジンを実装する必要があることです。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ドライバーでの処理](../../odbc/reference/driver-tasks.md)  
  
-   [ドライバーのアーキテクチャ](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>参照  
 [Microsoft 提供の ODBC ドライバー](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
