---
description: 変更の種類
title: 変更の種類 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], types of changes
- backward compatibility [ODBC], types of changes
ms.assetid: 6a7db81a-20aa-4915-aed8-429711a36f49
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46866c49a36711a8072895deb816a9d9110f5035
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476306"
---
# <a name="types-of-changes"></a>変更の種類
ODBC *3.x (および* odbc のすべてのバージョン) では、3種類の変更が行われます。 これらはそれぞれ下位互換性に影響し、異なる方法で処理されます。 これらの変更については、次の表で説明します。  
  
|変更の種類|説明|  
|--------------------|-----------------|  
|新機能|これらは、アウトオブラインバインドや記述子 *など、ODBC*3.x の新機能です。 これらは、アプリケーションとドライバー、およびドライバーマネージャーのバージョンが2.x である場合にのみ実装されます。したがっ *て、これら*の下位互換性を確保することはできません。|  
|重複する機能|これらは、ODBC 2.x および ODBC 3.x に存在する機能*です**が、それぞれ*に異なる方法で実装されています。 関数 **SQLAllocHandle** と **sqlallocstmt** は一例です。 これらの機能およびその他の重複する機能の旧バージョンとの互換性の問題は、ほとんどの場合、ドライバーマネージャーでのマッピングによって処理されます。|  
|動作の変更|これらの機能*は、odbc 2.x および odbc* 3.x では異なる方法で処理され*ます。* Datetime **#define** は一例です。 これらの機能は、環境属性の設定に基づいて ODBC 3.x ドライバーによって処理さ*れます。* (詳細については、「 [動作の変更](../../../odbc/reference/develop-app/behavioral-changes.md) 」を参照してください。)|
