---
description: SQLDriverConnect (Excel ドライバー)
title: SQLDriverConnect (Excel ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLDriverConnect
- SQLDriverConnect function [ODBC], Excel Driver
ms.assetid: 285cb1ea-f461-4596-97f2-fc57af05dede
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6320033d83e9b46c3567b3bf0b845144dbe9250e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449194"
---
# <a name="sqldriverconnect-excel-driver"></a>SQLDriverConnect (Excel ドライバー)
> [!NOTE]  
>  このトピックでは、Excel ドライバー固有の情報について説明します。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
 **SQLDriverConnect** を使用すると、データソース (DSN) を作成せずにドライバーに接続できます。  
  
 すべてのドライバーの接続文字列では、 **DSN**、 **dbq**、および **FIL**の各キーワードがサポートされています。  
  
 次の表は、各ドライバーに接続するために必要な最低限のキーワードと、 **SQLDriverConnect**で使用されるキーワードと値のペアの例を示しています。 DRIVERID 値の完全な一覧については、「 [Sqlconfigdatasource](../../odbc/microsoft/odbc-jet-sqlconfigdatasource-excel-driver.md)」を参照してください。  
  
> [!NOTE]  
>  Microsoft Excel 3.0 または4.0 ドライバーに DBQ または DefaultDir が指定されていない場合、ドライバーは現在のディレクトリに接続します。  
  
|ドライバー|キーワードが必要です|例|  
|------------|-----------------------|--------------|  
|Microsoft Excel 3.0 または4.0|ドライバー、DriverID|Driver = {Microsoft Excel Driver (* .xls)};DBQ = c:\temp;DriverID = 278|  
|Microsoft Excel 5.0/7.0|ドライバー、DriverID、DBQ|Driver = {Microsoft Excel Driver (* .xls)};DBQ =c:\temp\sample.xls;DriverID = 22|  
|Microsoft Excel 97 以降|ドライバー、DriverID、DBQ|Driver = {Microsoft Excel Driver (* .xls)};DBQ =c:\temp\sample.xls;DriverID = 790|
