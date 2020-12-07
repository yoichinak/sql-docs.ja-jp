---
description: SQLInstallTranslator 関数
title: SQLInstallTranslator 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslator
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslator
helpviewer_keywords:
- SQLInstallTranslator function [ODBC]
ms.assetid: 453b21ff-3c2b-4069-8ff7-5c727f062d89
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0be53f18682290c976af73c214d9f87b01b84704
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421156"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 関数
**互換性**  
 導入されたバージョン: ODBC 2.5、非推奨  
  
 **まとめ**  
 ODBC 3.0 では、 **Sqlinstalltranslator** は [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)に置き換えられました。 **Sqlinstalltranslator**への呼び出しは、 **SQLInstallTranslatorEx**にマップされます。 詳細については、「 **SQLInstallTranslatorEx**」を参照してください。  
  
 アプリケーションで、 *Lpszinffile*引数が NULL 以外の値に設定されている場合、 **SQLINSTALLTRANSLATOR**は FALSE を返し*ます。* Odbc 2.x で使用される Odbc .inf ファイル*は、旧*バージョンとの互換性のために odbc 3.x*ではサポート*されなくなりました。
