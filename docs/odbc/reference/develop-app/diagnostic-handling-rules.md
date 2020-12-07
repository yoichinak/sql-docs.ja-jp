---
description: 診断の処理規則
title: 診断処理ルール |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], diagnostic handling rules
- SQLGetDiagRec function [ODBC], diagnostic handling rules
- diagnostic information [ODBC], SqlGetDiagRec
ms.assetid: 74387c3a-d6b3-4c35-b209-b9612602b20a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3112f6db31a4369ec880e31a7bb8be6e15071bed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424664"
---
# <a name="diagnostic-handling-rules"></a>診断の処理規則
次の規則は、 **SQLGetDiagRec** と **SQLGetDiagField**での診断処理を制御します。  
  
 すべての ODBC コンポーネント:  
  
-   別の ODBC コンポーネントから受信したエラーや警告を置換、変更、またはマスクしないでください。  
  
-   別の ODBC コンポーネントから診断メッセージを受信するときに、追加のステータスレコードを追加することができます。 追加されたレコードは、実際の情報値を元のメッセージに追加する必要があります。  
  
 データソースを直接インターフェイスする ODBC コンポーネントの場合は、次のようになります。  
  
-   は、ベンダー識別子、コンポーネント識別子、およびデータソースの識別子のプレフィックスを、データソースから受信する診断メッセージに付ける必要があります。  
  
-   データソースのネイティブエラーコードを保持する必要があります。  
  
-   データソースの診断メッセージを保持する必要があります。  
  
 データソースに依存しないエラーまたは警告を生成する ODBC コンポーネントの場合:  
  
-   は、エラーまたは警告の正しい SQLSTATE を指定する必要があります。  
  
-   診断メッセージのテキストを生成する必要があります。  
  
-   は、ベンダー識別子とそのコンポーネント識別子のプレフィックスを診断メッセージに付ける必要があります。  
  
-   使用可能で意味がある場合は、ネイティブエラーコードを返す必要があります。  
  
 ドライバーマネージャーとのインターフェイスを持つ ODBC コンポーネントの場合:  
  
-   **SQLGetDiagRec**と**SQLGetDiagField**の出力引数を初期化する必要があります。  
  
-   は、その関数が呼び出されたときに、 **SQLGetDiagRec** および **SQLGetDiagField** の出力引数として診断情報を書式指定して返す必要があります。  
  
 ドライバーマネージャー以外の1つの ODBC コンポーネントの場合:  
  
-   は、ネイティブエラーに基づいて SQLSTATE を設定する必要があります。 ゲートウェイを使用しないファイルベースのドライバーおよび DBMS ベースのドライバーの場合、ドライバーは SQLSTATE を設定する必要があります。 ゲートウェイを使用する DBMS ベースのドライバーでは、ODBC をサポートするドライバーまたはゲートウェイが SQLSTATE を設定できます。
