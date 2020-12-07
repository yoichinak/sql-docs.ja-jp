---
description: パラメーター バインディングのオフセット
title: パラメーターバインドのオフセット |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets of parameters [ODBC]
- binding offsets of parameters [ODBC]
ms.assetid: 309339e9-9ccd-4a58-8aa4-b6dc88f4eb7c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 71b4958e77d01c613e33386ec1b2b21ed91f0a67
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476544"
---
# <a name="parameter-binding-offsets"></a>パラメーター バインディングのオフセット
アプリケーションでは、バインドされたパラメーターバッファーアドレスにオフセットが追加されるように指定できます。また、 **SQLExecDirect** または **sqlexecute** が呼び出されたときに、対応する長さ/インジケーターバッファーアドレスが使用されます。 これらの追加の結果によって、これらの操作で使用されるアドレスが決まります。  
  
 バインドオフセットを使用すると、アプリケーションは、以前にバインドされたパラメーターに対して **SQLBindParameter** を呼び出さずにバインドを変更できます。 パラメーターを再バインドする **SQLBindParameter** を呼び出すと、バッファーアドレスと長さ/インジケーターポインターが変更されます。 一方、オフセットを使用して再バインドする場合は、既存のバインドされたパラメーターバッファーアドレスと長さ/インジケーターバッファーアドレスにオフセットを追加するだけです。 オフセットが使用されている場合、バインドはアプリケーションバッファーのレイアウト方法の "テンプレート" であり、アプリケーションはオフセットを変更することによって、この "テンプレート" をメモリの別の領域に移動できます。 新しいオフセットはいつでも指定でき、常に元のバインドされた値に追加されます。  
  
 バインドオフセットを指定するために、アプリケーションは、SQL_ATTR_PARAM_BIND_OFFSET_PTR statement 属性を SQLINTEGER バッファーのアドレスに設定します。 アプリケーションは、バインドを使用する関数を呼び出す前に、このバッファーにバイト単位のオフセットを配置します。ただし、パラメーターのバッファーアドレスも長さ/インジケーターバッファーのアドレスも0でなく、バインドされたパラメーターが SQL ステートメント内にある場合に限ります。 アドレスとオフセットの合計は、有効なアドレスである必要があります。 (つまり、オフセットとオフセットが追加されるアドレスの両方または両方が、有効なアドレスである限り無効になることがあります)。  
  
> [!NOTE]  
>  バインドオフセットは ODBC 2 ではサポートされていません。*x* ドライバー。
