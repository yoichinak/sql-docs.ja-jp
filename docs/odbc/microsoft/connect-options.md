---
description: 接続のオプション
title: 接続オプション |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection options [ODBC]
- ODBC driver for Oracle [ODBC], connection options
- custom connection options [ODBC]
ms.assetid: abfdc133-cb33-435f-a467-fbe15444f687
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 22326ca650f575c6a4f0503093306d8b68581475
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483685"
---
# <a name="connect-options"></a>接続のオプション
> [!IMPORTANT]  
>  この機能は、今後のバージョンの Windows では削除される予定です。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 代わりに、Oracle によって提供される ODBC ドライバーを使用してください。  
  
 これらのオプションを使用すると、アプリケーション内のデータベース接続をカスタマイズできます。  
  
|Connect オプション|ノート|  
|--------------------|-----------|  
|SQL_AUTOCOMMIT|SQL_AUTOCOMMIT_OFF を選択した場合、アプリケーションは [Sqltransact](../../odbc/microsoft/core-level-api-functions-odbc-driver-for-oracle.md)を使用してトランザクションを明示的にコミットまたはロールバックする必要があります。|  
|SQL_ODBC_CURSORS|この接続属性は、ドライバーマネージャーに実装されます。|  
|SQL_OPT_TRACE|この接続属性は、ドライバーマネージャーに実装されます。|  
|SQL_OPT_TRACEFILE|この接続属性は、ドライバーマネージャーに実装されます。|  
|SQL_TRANSLATE_DLL|"ドライバーに対応していません" というエラーが返されます。|  
|SQL_TRANSLATE_OPTION|変換 .dll に渡される32ビット値。|  
|SQL_TXN_ISOLATION|ドライバーは SQL_TXN_READ_COMMITTED のみを許可します。<br /><br /> 次の vParams はサポートされていません。<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
|SQL_ATTR_ENLIST_IN_DTC|この ODBC 3.0 接続属性を使用すると、Microsoft コンポーネントサービス (または Windows NT を使用している場合は MTS) によって調整された分散トランザクションで、ODBC Driver for Oracle を使用できます。 このメソッドは、 *Vparam*引数としてトランザクションに*pITransaction*インターフェイスポインターを提供します。|  
|SQL_ATTR_CONNECTION_DEAD|この読み取り専用 ODBC 3.5 接続属性を使用すると、Oracle サーバーへの接続に失敗したかどうかを判断できます。 Get のみ。を設定できません。|
