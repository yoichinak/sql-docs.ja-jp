---
description: SQLDriverConnect (Access ドライバー)
title: SQLDriverConnect (Access Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Access Driver
ms.assetid: 9d133e9b-7545-464d-aa3c-677fa7e2a41d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 52bbcbfa379be53ea24c150d2522242e85e61fea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449214"
---
# <a name="sqldriverconnect-access-driver"></a>SQLDriverConnect (Access ドライバー)
> [!NOTE]  
>  このトピックでは、ドライバー固有の情報にアクセスします。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 **SQLDriverConnect** を使用すると、データソース (DSN) を作成せずにドライバーに接続できます。  
  
 すべてのドライバーの接続文字列では、 **DSN**、 **dbq**、および **FIL**の各キーワードがサポートされています。  
  
 **UID**キーワードと**PWD**キーワードもサポートされています。  
  
 PWD キーワードには、特殊文字を含めることはできません (「 **SQLGetInfo** が返す値の SQL_SPECIAL_CHARACTERS」を参照してください)。  
  
 次の表は、各ドライバーに接続するために必要な最低限のキーワードと、 **SQLDriverConnect**で使用されるキーワードと値のペアの例を示しています。 DRIVERID 値の完全な一覧については、「 [Sqlconfigdatasource](../../odbc/microsoft/sqlconfigdatasource-access-driver.md)」を参照してください。  
  
|ドライバー|キーワードが必要です|例|  
|------------|-----------------------|--------------|  
|Microsoft Access|ドライバー、DBQ|Driver = {Microsoft Access Driver (* .mdb)};DBQ = c: \\ \temp、 \\ mdb|
