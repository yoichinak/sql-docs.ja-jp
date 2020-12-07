---
description: SQLColumns (テキスト ファイル ドライバー)
title: SQLColumns (テキストファイルドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLColumns
- SQLColumns function [ODBC], Text File Driver
ms.assetid: c99e5f8d-4e43-48f8-9e0e-086707b411f5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fed898b4b4c821571423eba1b99ef093bf38b844
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412028"
---
# <a name="sqlcolumns-text-file-driver"></a>SQLColumns (テキスト ファイル ドライバー)
> [!NOTE]  
>  このトピックでは、テキストファイルドライバー固有の情報について説明します。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
|列|コメント|  
|------------|--------------|  
|TABLE_QUALIFIER|ディレクトリへのパスが返されます。|  
|TABLE_OWNER|所有者名がサポートされていないため、この列には NULL が返されます。|  
|NULLABLE|主キーまたは一意のインデックスに含まれる列に対して SQL_NO_NULLS が返されます。|
