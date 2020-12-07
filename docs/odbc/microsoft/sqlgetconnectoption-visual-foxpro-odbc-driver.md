---
description: SQLGetConnectOption (Visual FoxPro ODBC ドライバー)
title: SQLGetConnectOption (Visual FoxPro ODBC ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetConnectOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5703eb39-f3b2-4f3a-8676-a5625ae29a41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd22ec3862ff2f0f3c4f7b5aa9dbeff53a5d8cfe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411788"
---
# <a name="sqlgetconnectoption-visual-foxpro-odbc-driver"></a>SQLGetConnectOption (Visual FoxPro ODBC ドライバー)
> [!NOTE]  
>  このトピックには、Visual FoxPro ODBC ドライバー固有の情報が含まれています。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 サポート: 部分的  
  
 ODBC API の準拠: レベル1  
  
 接続オプションの現在の設定を返します。 この関数は部分的にサポートされています。ドライバーは*foption*引数のすべての値をサポートしていますが、 *foption*引数 SQL_TXN_ISOLATION の*vparam*値の一部をサポートしていません。  
  
 次の表では、 **SQLGetConnectOption**の VISUAL FoxPro ODBC ドライバーの実装に固有の動作を持つ引数のみについて説明します。  
  
|*fOption*|解説|  
|---------------|-------------|  
|SQL_AUTOCOMMIT|SQL_AUTOCOMMIT_OFF を選択した場合、アプリケーションは [Sqltransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md)を使用してトランザクションを明示的にコミットまたはロールバックする必要があります。Visual FoxPro ODBC ドライバーは、完了時に不可能ステートメントを自動的にコミットしません。 ステートメントが不可能の場合、ドライバーはトランザクションを開始します。|  
|SQL_CURRENT_QUALIFIER|には、完全修飾データベース (dbc ファイル) 名を指定することも、0個以上のテーブル (.dbf ファイル) を含むディレクトリへの完全修飾パスを指定することもできます。|  
|SQL_LOGINTIMEOUT|"ドライバーがサポートされていません" エラーを返します。|  
|SQL_CURSORS|"ドライバーがサポートされていません" エラーを返します。|  
|SQL_PACKET_SIZE|"ドライバーがサポートされていません" エラーを返します。|  
|SQL_TXN_ISOLATION|ドライバーは SQL_TXN_READ_COMMITTED のみを許可します。<br /><br /> 次の *Vparam*はサポートされていません。<br /><br /> SQL_TXN_READ_UNCOMMITTED<br /><br /> SQL_TXN_REAPEATABLE_READ<br /><br /> SQL_TXN_SERIALIZABLE|  
  
 詳細については、 *ODBC プログラマーリファレンス*の「 [SQLGetConnectOption](../../odbc/reference/syntax/sqlgetconnectoption-function.md) 」を参照してください。
