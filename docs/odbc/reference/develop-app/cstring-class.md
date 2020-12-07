---
description: CString クラス
title: CString クラス |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CString class [ODBC]
ms.assetid: 18630642-76fa-43c4-a154-3f0969ec9b50
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cfe8809fed17e4e787c9965f175c4b97238868bf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499935"
---
# <a name="cstring-class"></a>CString クラス
Microsoft® Visual C++®の **cstring** クラスのオブジェクトは署名されており、odbc 関数の文字列引数は符号なしであるため、キャストせずに **CSTRING** オブジェクトを odbc 関数に渡すアプリケーションは、コンパイラの警告を受け取ります。
