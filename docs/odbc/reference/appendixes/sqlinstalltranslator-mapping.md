---
description: SQLInstallTranslator のマッピング
title: SQLInstallTranslator マッピング |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLInstallTranslator function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLInstallTranslator
ms.assetid: bcd9ba4f-7834-4bc4-876e-c7478998e524
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fc571e305070e4afba6dc7c647d18a6790c011f0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448971"
---
# <a name="sqlinstalltranslator-mapping"></a>SQLInstallTranslator のマッピング
ODBC *2.x アプリケーションが odbc* *3. x*ドライバーを使用して**sqlinstalltranslator**を呼び出すと、ドライバーマネージャーが呼び出しを**SQLInstallTranslatorEx**にマップします。アプリケーションでは、 *Lpszinffile*引数が NULL 以外の値に設定されている ODBC *3.x ドライバーマネージャー*で**sqlinstalltranslator**を呼び出すことはできません。 ODBC です。Odbc 2.x で使用される INF *ファイルは、* 旧バージョンとの互換性のため *に odbc 3.x*ではサポートされなくなりました。
