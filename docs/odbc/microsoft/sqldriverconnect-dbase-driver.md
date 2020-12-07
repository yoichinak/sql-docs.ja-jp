---
description: SQLDriverConnect (dBASE ドライバー)
title: SQLDriverConnect (dBASE ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], dBASE Driver
ms.assetid: c837aa31-068e-4fa3-bc00-aae09bec21de
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e15925b52c096acb1a1021c1a2f968c0863eacf0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449204"
---
# <a name="sqldriverconnect-dbase-driver"></a>SQLDriverConnect (dBASE ドライバー)
> [!NOTE]  
>  このトピックでは、dBASE ドライバー固有の情報について説明します。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 **SQLDriverConnect** を使用すると、データソース (DSN) を作成せずにドライバーに接続できます。  
  
 すべてのドライバーの接続文字列では、 **DSN**、 **dbq**、および **FIL**の各キーワードがサポートされています。  
  
 Paradox ドライバーを使用すると、ユーザーがパスワードで保護されたファイルを開いた後、他のユーザーは同じファイルを開くことができなくなります。  
  
 次の表は、各ドライバーに接続するために必要な最低限のキーワードと、 **SQLDriverConnect**で使用されるキーワードと値のペアの例を示しています。 DRIVERID 値の完全な一覧については、「 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-dbase-driver.md)」を参照してください。  
  
> [!NOTE]  
>  DBASEdriver に DBQ または DefaultDir が指定されていない場合、ドライバーは現在のディレクトリに接続します。  
  
|ドライバー|キーワードが必要です|例|  
|------------|-----------------------|--------------|  
|dBASE|ドライバー、DriverID|Driver = {Microsoft dBASE Driver (* .dbf)};DBQ = c:\temp;DriverID = 277|
