---
description: ODBC カーソル ライブラリのエラー コード
title: ODBC カーソルライブラリのエラーコード |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursor library [ODBC], error codes
- error codes [ODBC], cursor library
- ODBC cursor library [ODBC], error codes
ms.assetid: 9713480e-8744-4f37-a630-20871590d4a1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 414de02eb7145006af4faa543735888082a3d6ff
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88466137"
---
# <a name="odbc-cursor-library-error-codes"></a>ODBC カーソル ライブラリのエラー コード
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Microsoft Data Access コンポーネントでは削除される予定です。 新しい開発作業ではこの機能の使用を避け、現在この機能を使用しているアプリケーションの変更を検討してください。 代わりに、ドライバーおよびサーバーカーソルを使用します。  
  
 Odbc カーソルライブラリは、 [ODBC API リファレンス](../../../odbc/reference/syntax/odbc-api-reference.md)に記載されているものに加えて、次の sqlstates を返します。  
  
> [!NOTE]  
>  カーソルライブラリでは、状態レコードが順序付けされません。ドライバーマネージャーおよび ODBC 3.*x* ドライバーは、ステータスレコードの順序付けを行います。  
  
|SQLSTATE|説明|から返される可能性があります。|  
|--------------|-----------------|--------------------------|  
|01000|カーソルは更新できません。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|カーソルライブラリが使用されていません。 読み込みに失敗しました。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|カーソルライブラリが使用されていません。 ドライバーのサポートが不十分です。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|カーソルライブラリが使用されていません。 ドライバーマネージャーとバージョンが一致しません。|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|ドライバーが SQL_SUCCESS_WITH_INFO を返しました。 警告メッセージが失われました。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|一般的なエラー: ファイルバッファーを作成できません。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般的なエラー: ファイルバッファーから読み取ることができません。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般的なエラー: ファイルバッファーに書き込むことができません。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|一般的なエラー: ファイルバッファーを閉じたり、削除したりすることはできません。|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|検索可能な列がバインドされていないため、位置指定要求を実行できません。|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|結果セットが結合条件によって作成されたため、位置指定要求を実行できませんでした。|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|バインドされたバッファーがセグメントの最大サイズを超えています。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|**SELECT**ステートメントによって結果セットが生成されませんでした。|**SQLGetData**|  
|SL005|**Select** ステートメントに GROUP by 句が含まれています。|**SQLGetData**|  
|SL006|パラメーター配列は、位置指定要求ではサポートされていません。|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** は、順方向専用 (バッファリングされていない) カーソルでは許可されていません。|**SQLGetData**|  
|SL009|**Sqlfetch**または**sqlfetchscroll**を呼び出す前に、列がバインドされていませんでした。|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** は、内部バッファーにバインドしようとしたときに SQL_ERROR を返しました。|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|ステートメントオプションは、 **Sqlfetch** または **sqlfetchscroll**を呼び出した後にのみ有効です。|**SQLGetStmtAttr**|  
|SL012|カーソルが開いている間は、ステートメントのバインドを変更できません。|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|位置指定要求が発行されましたが、一部の列カウントフィールドがバッファーされませんでした。|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**Sqlfetch** と **sqlfetchscroll** を混在させることはできません。|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
