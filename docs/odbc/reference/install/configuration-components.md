---
description: 構成コンポーネント
title: 構成コンポーネント |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], configuring
ms.assetid: 0b68ff48-12e4-41aa-b9e2-b39ed5023ea7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a8a4b0f0b0a7a99409b5bb9caea53f23b62457e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487435"
---
# <a name="configuration-components"></a>構成コンポーネント
> [!NOTE]  
>  Windows XP および windows Server 2003 以降では、ODBC は Windows オペレーティングシステムに含まれています。 ODBC は、以前のバージョンの Windows にのみ明示的にインストールする必要があります。  
  
 データソースは、インストーラーの DLL によって構成されます。この DLL は、必要に応じてドライバーのセットアップ Dll と translator セットアップ Dll を呼び出します。 インストーラー DLL は、コントロールパネルから直接呼び出されるか、または *管理プログラム*と呼ばれる別のプログラムによって読み込まれて呼び出されます。 構成コンポーネント間の関係を次の図に示します。  
  
 ![構成コンポーネント間の関係](../../../odbc/reference/install/media/pr30.gif "pr30")  
  
 これらのコンポーネントの詳細については、このセクションの最後にある次のトピックを参照してください。  
  
-   [セットアップ プログラム](../../../odbc/reference/install/setup-program.md)  
  
-   [インストーラー DLL](../../../odbc/reference/install/installer-dll.md)  
  
-   [ドライバーのセットアップ DLL](../../../odbc/reference/install/driver-setup-dll.md)  
  
## <a name="see-also"></a>参照  
 [インストールコンポーネント](../../../odbc/reference/install/installation-components.md)
