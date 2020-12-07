---
description: トランスレーター セットアップ DLL
title: トランスレーターセットアップ Dll |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2fe4d514f098773024392666d8f528592d362da4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487395"
---
# <a name="translator-setup-dlls"></a>トランスレーター セットアップ DLL
> [!NOTE]  
>  Windows XP および windows Server 2003 以降では、ODBC は Windows オペレーティングシステムに含まれています。 ODBC は、以前のバージョンの Windows にのみ明示的にインストールする必要があります。  
  
 Translator セットアップ DLL には、変換プログラムの既定のオプションを返す **configtranslator** 関数が含まれています。 必要に応じて、ユーザーにこの情報の入力を求めます。 この関数の詳細については、「 [SETUP DLL API Reference](../../../odbc/reference/syntax/setup-dll-api-reference.md)」を参照してください。  
  
 Translator セットアップ DLL は、translator 開発者によって作成されています。 トランスレーター DLL または別の DLL の一部にすることができます。
