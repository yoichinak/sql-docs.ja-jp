---
description: SQLInstallTranslator 関数
title: SQLInstallTranslator 関数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
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
ms.openlocfilehash: 40f4c4a5df497c64d081a8d03d1765a4fe5e060a
ms.sourcegitcommit: 33f0f190f962059826e002be165a2bef4f9e350c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/30/2021
ms.locfileid: "99189653"
---
# <a name="sqlinstalltranslator-function"></a>SQLInstallTranslator 関数
**互換性**  
 導入されたバージョン: ODBC 2.5、非推奨  
  
 **要約**  
 ODBC 3.0 では、 **Sqlinstalltranslator** は [SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)に置き換えられました。 **Sqlinstalltranslator** への呼び出しは、 **SQLInstallTranslatorEx** にマップされます。 詳細については、「 **SQLInstallTranslatorEx**」を参照してください。  
  
 アプリケーションで、 *Lpszinffile* 引数が NULL 以外の値に設定されている場合、 **SQLINSTALLTRANSLATOR** は FALSE を返し *ます。* Odbc 2.x で使用される Odbc .inf ファイル *は、旧* バージョンとの互換性のために odbc 3.x *ではサポート* されなくなりました。
