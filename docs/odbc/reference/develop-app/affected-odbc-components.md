---
description: 影響を受ける ODBC コンポーネント
title: 影響を受ける ODBC コンポーネント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4874a22d441ec856c25e08dc20cf04e0f0be89cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424864"
---
# <a name="affected-odbc-components"></a>影響を受ける ODBC コンポーネント
旧バージョンとの互換性については、新しいバージョンのドライバーマネージャーの導入によって、アプリケーション、ドライバーマネージャー、およびドライバーがどのように影響を受けるかについて説明します。 これは、アプリケーションとドライバーのいずれかまたは両方が古いバージョンのままである場合に影響します。 したがって、次の表に示すように、3種類の下位互換性が考慮されます。  
  
|Type|DM のバージョン|アプリケーションのバージョン|ドライバーのバージョン|  
|----------|-------------------|----------------------------|-----------------------|  
|ドライバーマネージャーの旧バージョンとの互換性|*3.x*|*2.x*|*2.x*|  
|ドライバー [1] の旧バージョンとの互換性|*3.x*|*2.x*|*3.x*|  
|アプリケーションの旧バージョンとの互換性|*3.x*|*3.x*|*2.x*|  
  
 [1] ドライバーの旧バージョンとの互換性については、主に「付録 G: 旧バージョンとの互換性のためのドライバーガイドライン」で説明されています。  
  
> [!NOTE]
>  標準に準拠したアプリケーション (オープングループまたは ISO CLI 標準に従って作成されたアプリケーションなど) は、ODBC 3.x ドライバーマネージャーを介して *odbc 3.x* *ドライバーで* 動作することが保証されます。 アプリケーションが使用している機能がドライバーで使用可能であることを前提としています。 また、標準に準拠しているアプリケーションが ODBC *3. x* ヘッダーファイルを使用してコンパイルされていることも前提としています。
