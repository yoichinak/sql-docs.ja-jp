---
description: エラー メッセージ (Visual FoxPro ODBC ドライバー)
title: エラーメッセージ (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- error messages [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], error messages
- SQLSTATE [ODBC]
- FoxPro ODBC driver [ODBC], error messages
ms.assetid: 58ea9734-4edf-44da-ba80-938aa7b340e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1b76ec8703ebee8aa597849b23a5a22323caa350
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483605"
---
# <a name="error-messages-visual-foxpro-odbc-driver"></a>エラー メッセージ (Visual FoxPro ODBC ドライバー)
エラーが発生すると、Visual FoxPro ドライバーは次の情報を返します。  
  
-   ネイティブエラー番号とエラーメッセージのテキスト  
  
-   SQLSTATE (ODBC エラーコード) とエラーメッセージテキスト  
  
 このエラー情報にアクセスするには、 [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)を呼び出します。  
  
## <a name="native-errors"></a>ネイティブエラー  
 データソースで発生したエラーの場合、Visual FoxPro ドライバーはネイティブのエラー番号とエラーメッセージのテキストを返します。 ネイティブエラー番号の一覧については、「 [Visual FOXPRO ODBC ドライバーのネイティブエラーメッセージ](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md)」を参照してください。  
  
## <a name="sqlstate-odbc-error-codes"></a>SQLSTATE (ODBC エラー コード)  
 Visual FoxPro ドライバーによって検出されて返されるエラーの場合、ドライバーは返されたネイティブエラー番号を適切な SQLSTATE にマップします。 ネイティブエラー番号にマップする ODBC エラーコードがない場合、Visual FoxPro ドライバーは SQLSTATE S1000 (一般的なエラー) を返します。  
  
 Visual foxpro ODBC ドライバーによって生成される、対応する Visual FoxPro エラーの SQLSTATE 値の一覧については、「 [Odbc エラーコード](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
 エラーメッセージの形式は次のとおりです。  
  
 **[** *vendor* **] [** *ODBC_component* **]** *error_message*  
  
 次の表で定義されているように、角かっこ ([]) で囲まれたプレフィックスによってエラーの原因が特定されます。  
  
|データ ソースの|Prefix|値|  
|-----------------|------------|-----------|  
|ドライバー マネージャー|業者<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC ドライバーマネージャー]<br />該当なし|  
|Visual FoxPro ドライバー|業者<br />[ODBC_component]<br />[data_source]|[Microsoft]<br />[ODBC Visual FoxPro ドライバー]<br />該当なし|  
  
 たとえば、Visual FoxPro ODBC ドライバーがファイルの .dbf を見つけられなかった場合、次のエラーメッセージが返されることがあります。  
  
 "[*Microsoft*] [*ODBC Visual FoxPro Driver*] ファイル ' employee .dbf ' は存在しません"
