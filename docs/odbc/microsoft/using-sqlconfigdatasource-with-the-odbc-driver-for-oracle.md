---
description: ODBC Driver for Oracle を使用した SQLConfigDatasource の使用
title: SQLConfigDatasource と ODBC Driver for Oracle | の使用Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], ODBC driver for Oracle
ms.assetid: e535d1ef-aff9-4ae7-a3ed-ef4ca2584289
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 98f7ef460097a7ca4b814769290cdcda81eb6205
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471314"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>ODBC Driver for Oracle を使用した SQLConfigDatasource の使用
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 次の表に、Microsoft ODBC Driver for Oracle、version 1.0 (Msorcl10.dll)、および Microsoft ODBC Driver for Oracle、version 2.0 (Msorcl32.dll) の有効な **Sqlconfigdatasource** 設定を示します。  
  
> [!NOTE]  
>  Msorcl10.dll ドライバー (バージョン 1.0) では、 **Server**以外のすべての設定がサポートされています。 Msorcl32.dll ドライバー (バージョン2.0 以降) では、すべての設定がサポートされています。  
  
 一部の設定はドライバーによって無視されますが、 **Sqlconfigdatasource**によって受け付けられます。 これらの設定を ODBC 接続文字列に含めることは、実行時にのみ許可されます。 **Sqlconfigdatasource**によってデータソースが作成されるときに、無視される設定はレジストリに格納されません。  
  
 次の表で *は、/N は* 、許容される最大長までの有効な英数字文字列を意味します。 最大*Len* (最大長) は、文字列終端文字を含む、設定で許容される最大文字列長です。  
  
|設定|最大長|既定値|有効な値|説明|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65,535|1000|最小フェッチバッファーサイズは65535バイトまで|  
|CatalogCap|2|1|0 または 1|1の場合、引用符で囲まれていない識別子は、カタログ関数では大文字に変換されます。|  
|ConnectString|128|""|A/N|接続文字列: Msorcl10.dll ドライバーを使用してサーバー名を指定するために必要なメソッドです。|  
|説明|256|""|A/N|説明|  
|DSN (DSN)|33|""|A/N|データソース名。|  
|GuessTheColDef|4|0|A/N|Oracle で定義された小数点以下桁数がない列に対して0以外の値を返します。|  
|数値 float|2|""|0 または 1|0の場合、FLOAT 型の列は SQL_FLOAT として扱われます。 1の場合、FLOAT 型の列は SQL_DOUBLE として扱われます。|  
|PWD|30|""|A/N|パスワード。|  
|RDOSupport|2|""|0 または 1|RDO が Oracle プロシージャを呼び出すことができるようにします。|  
|解説|2|0|0 または 1|カタログ関数に注釈を含めます。|  
|RowLimit|4|""|0 ~ 99|SELECT ステートメントによって返される行の最大数。 長さが0の文字列は、制限が適用されていないことを示します。|  
|サーバー|128|""|A/N|Oracle サーバー名。|  
|SynonymColumns|2|1|0 または 1|SQLColumns にシノニムを含めます。|  
|SystemTable|2|""|0 または 1|0の場合、システムテーブルは表示されません。 1の場合、システムテーブルが表示されます。|  
|TranslationDLL|33|""|A/N|変換 .dll 名。|  
|TranslationName|33|""|A/N|翻訳名。|  
|TranslationOption|33|""|A/N|Translation オプション。|  
|TxnCap|2|""|A/N|トランザクション対応。 0の場合、ドライバーはトランザクションをサポートしていないことを報告します。 1の場合、ドライバーはトランザクションを実行できることを報告します。|  
|UID|30|""|A/N|ユーザー名。|
