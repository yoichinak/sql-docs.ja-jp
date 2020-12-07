---
description: '[データ ビューアー]'
title: '[データ ビューアー] | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.dataviewer.f1
helpviewer_keywords:
- Data Viewer dialog box
ms.assetid: 6351309a-688f-4e82-9697-1712130f10a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8e3f659ec65cece6dd36f4fc0bc09ecae70a46c3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430944"
---
# <a name="data-viewer"></a>[データ ビューアー]

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  パスがデータ ビューアーを使用するように構成されている場合、データ ビューアーはデータが 2 つのデータ フロー コンポーネントを移動するときに、バッファーによるデータ バッファーを表示します。  
  
## <a name="options"></a>オプション  
 **緑色の矢印**  
 クリックすると、次のバッファーのデータが表示されます。 データが 1 つのバッファーに移動される場合、このオプションは使用できません。  
  
 **[デタッチ]**  
 データ ビューアーをデタッチします。  
  
 **注** &#xA0;&#xA0;&#xA0;データ ビューアーをデタッチしてもデータ ビューアーは削除されません。 データ ビューアーがデタッチされた場合、データはパスを流れますが、ビューアー内のデータを各バッファーのデータに一致させる更新は行われません。  
  
 **[アタッチ]**  
 データ ビューアーをアタッチします。  
  
 **注** &#xA0;&#xA0;&#xA0;アタッチされたデータ ビューアーは、データ フロー内の各バッファーからの情報を表示してから、一時停止します。 緑色の矢印を使用して次のバッファーに進むことができます。  
  
 **[データのコピー]**  
 現在のバッファーのデータをクリップボードにコピーします。  
  
## <a name="see-also"></a>関連項目  
 [データ フローのデバッグ](../../integration-services/troubleshooting/debugging-data-flow.md)  
  
  
