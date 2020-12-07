---
description: SQLColumns (Excel ドライバー)
title: SQLColumns (Excel ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColumns function [ODBC], Excel Driver
- Excel driver [ODBC], SQLColumns
ms.assetid: 4bae3fcd-0287-4f79-ad7c-8f7ab2f6f940
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b44c3ee23eead3f2798c2389e66f82d77f48cc1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412058"
---
# <a name="sqlcolumns-excel-driver"></a>SQLColumns (Excel ドライバー)
> [!NOTE]  
>  このトピックでは、Excel ドライバー固有の情報について説明します。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
|列|コメント|  
|------------|--------------|  
|TABLE_QUALIFIER|ディレクトリへのパスが返されます。|  
|TABLE_OWNER|所有者名がサポートされていないため、この列には NULL が返されます。|  
|NULLABLE|主キーまたは一意のインデックスに含まれる列に対して SQL_NO_NULLS が返されます。|
