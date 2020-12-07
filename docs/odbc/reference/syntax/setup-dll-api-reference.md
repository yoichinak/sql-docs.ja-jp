---
description: セットアップ DLL API リファレンス
title: DLL API リファレンスのセットアップ |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: f9d03f17-1c0d-4e7c-9c04-8c316e07ef25
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5cb3e20a1c25d206a1dd27367bbe4a128af0818f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487335"
---
# <a name="setup-dll-api-reference"></a>セットアップ DLL API リファレンス
このセクションでは、2つの関数 (**configdriver** と **configdriver**) で構成される driver setup DLL API の構文について説明します。 **Configdriver** と **configdriver** は、ドライバー dll または別のセットアップ DLL のいずれかにすることができます。  
  
 また、このセクションでは、1つの関数 (**Configtranslator**) で構成される TRANSLATOR SETUP DLL API の構文についても説明します。 **Configtranslator** は、translator dll または別のセットアップ dll のいずれかにすることができます。  
  
 各関数には、その関数が導入された ODBC のバージョンが示されています。  
  
 このセクションでは、次のトピックを扱います。  
  
-   [ConfigDriver 関数](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [ConfigDSN 関数](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [ConfigTranslator 関数](../../../odbc/reference/syntax/configtranslator-function.md)
