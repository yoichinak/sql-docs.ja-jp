---
description: Microsoft コンポーネント サービスの使用
title: Microsoft コンポーネントサービスを使用する |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], component services
- component services [ODBC]
ms.assetid: 06450562-d8f3-4987-b7bd-4a70223ff937
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8214b706394c9fe8e2b8a6fd2491156292475fa9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471344"
---
# <a name="using-microsoft-component-services"></a>Microsoft コンポーネント サービスの使用
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 Microsoft Windows NT/Windows 2000 および Microsoft Windows 95/98 で、Oracle データベースがトランザクションコンポーネントサービス (Windows NT を使用している場合は MTS) で動作できるようにすることができます。 トランザクションをサポートするコンポーネントサービスで Oracle データベースを使用できるようにするには、システム管理者が V $ XATRANS $ という名前のビューを作成する必要があります。 このスクリプトを作成するには、Oracle によって提供されるスクリプトを実行する必要があります。 詳細については、コンポーネントサービスのヘルプまたは Oracle のドキュメントを参照してください。
