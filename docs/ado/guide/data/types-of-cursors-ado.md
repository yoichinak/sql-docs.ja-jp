---
description: カーソルの種類 (ADO)
title: カーソルの種類 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
author: rothja
ms.author: jroth
ms.openlocfilehash: adeaef5251ef5e9ebbc1e6b792f2647d3fcea250
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979313"
---
# <a name="types-of-cursors-ado"></a>カーソルの種類 (ADO)
一般的な規則として、アプリケーションでは、必要なデータアクセスを提供する最も単純なカーソルを使用する必要があります。 基本を超える各カーソル特性 (順方向専用、読み取り専用、静的、スクロール、バッファーなし) には、クライアントメモリ、ネットワーク負荷、またはパフォーマンスの価格があります。 多くの場合、既定のカーソルオプションでは、アプリケーションで実際に必要とされるよりも複雑なカーソルが生成されます。  
  
 カーソルの種類の選択は、アプリケーションでの結果セットの使用方法や、結果セットのサイズ、使用される可能性が高いデータの割合、データの変更に対する感度、アプリケーションのパフォーマンス要件など、いくつかの設計上の考慮事項によって異なります。  
  
 最も基本的なカーソルの選択は、データを変更する必要があるか、単にデータを表示する必要があるかによって異なります。  
  
-   結果のセットをスクロールするだけで、変更データをスクロールする必要がない場合は、 [順方向専用](../../../ado/guide/data/forward-only-cursors.md) カーソルまたは [静的](../../../ado/guide/data/static-cursors.md) カーソルを使用します。  
  
-   大きな結果セットがあり、少数の行だけを選択する必要がある場合は、 [キーセット](../../../ado/guide/data/keyset-cursors.md) カーソルを使用します。  
  
-   すべての同時実行ユーザーが最近追加、変更、および削除した結果セットを同期する場合は、 [動的](../../../ado/guide/data/dynamic-cursors.md) カーソルを使用します。  
  
 各カーソルの種類は個別であるように見えますが、これらのカーソルの種類は、重複する特性やオプションの結果とはあまり異なる性質を持つという点に注意してください。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [順方向専用カーソル](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [静的カーソル](../../../ado/guide/data/static-cursors.md)  
  
-   [Keyset カーソル](../../../ado/guide/data/keyset-cursors.md)  
  
-   [動的カーソル](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>参照  
 [順方向専用カーソル](../../../ado/guide/data/forward-only-cursors.md)   
 [静的カーソル](../../../ado/guide/data/static-cursors.md)   
 [キーセットカーソル](../../../ado/guide/data/keyset-cursors.md)   
 [動的カーソル](../../../ado/guide/data/dynamic-cursors.md)
