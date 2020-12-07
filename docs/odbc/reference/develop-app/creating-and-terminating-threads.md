---
description: スレッドの作成と終了
title: スレッドを作成して終了する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- terminating threads [ODBC]
- threads [ODBC]
- multithreaded applications [ODBC]
ms.assetid: a2cf98ef-1c71-4742-8ee2-b53fd8e04333
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c0100b85bc596149d809dee7e6c4cb3547dbd081
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465854"
---
# <a name="creating-and-terminating-threads"></a>スレッドの作成と終了
ODBC を使用するマルチスレッドアプリケーションでは、Microsoft® Visual C++®ランタイムライブラリ関数 **_beginthread** および **_endthread** (または **_beginthreadex** と **_Endthreadex**) を呼び出して、odbc ドライバーマネージャーを呼び出すスレッドを作成および終了する必要があります。 アプリケーションが Microsoft Windows NT® functions **CreateThread** と **EndThread** を呼び出すと、ドライバーマネージャーと一部の ODBC ドライバーが **CreateThread**を呼び出すことによって作成されたスレッドで動作しない C ランタイム関数を呼び出すため、メモリリークが発生します。 詳細については、Microsoft Windows®のドキュメントを参照してください。
