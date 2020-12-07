---
description: SQLSetConnectOption (Access ドライバー)
title: SQLSetConnectOption (Access Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], Access Driver
ms.assetid: 58399bc4-d0b1-4eaa-a474-c92b2d5855ea
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a007693a59c190a29bf9895446e916d5c232bb9f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483315"
---
# <a name="sqlsetconnectoption-access-driver"></a>SQLSetConnectOption (Access ドライバー)
> [!NOTE]  
>  このトピックでは、ドライバー固有の情報にアクセスします。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
|fOption|解説|  
|-------------|-------------|  
|SQL_ACCESS_MODE|SQL_ACCESS_MODE fOption は、SQL_MODE_READ_ONLY または SQL_MODE_READ_WRITE のいずれかに設定できます。 ただし、SQL_ACCESS_MODE が SQL_MODE_READ_ONLY に設定されている場合、ドライバーは更新を妨げることはありません。|  
|SQL_AUTOCOMMIT|Microsoft access ドライバーではトランザクション [1] がサポートされているため、Microsoft Access ドライバーを使用する場合は、SQL_AUTOCOMMIT オプションを SQL_AUTOCOMMIT_ON または SQL_AUTOCOMMIT_OFF に設定できます。|  
|SQL_CURRENT_QUALIFIER|サポートされています。|  
|SQL_LOGIN_TIMEOUT|サポートされていません。|  
|SQL_OPT_TRACE|サポートされています。|  
|SQL_OPT_TRACEFILE|サポートされています。|  
|SQL_PACKET_SIZE|サポートされていません。|  
|SQL_QUIET_MODE|サポートされていません。|  
|SQL_TRANSLATE_DLL|サポートされていません。|  
|SQL_TRANSLATION_OPTION|サポートされていません。|  
|SQL_TXN_ISOLATION|SQL_TXN_ISOLATION は常に SQL_TXN_READ_COMMITTED です。|  
  
 [1] アトミックトランザクションは、Microsoft Access ドライバーではサポートされていません。 Microsoft Access ドライバーを使用してトランザクションをコミットする場合、トランザクションがコミットされてから、値がディスクに書き込まれるまでには、有限の遅延が発生します。 この遅延は、Microsoft Jet エンジンに固有の遅延によって決定されます。 PageTimeout オプションがその値より下に設定されている場合でも、ページタイムアウトは最小値より小さくなりません。 その結果、コミットされたデータが安定していることは保証されません。これは、遅延中に変更が行われる可能性があるためです。
