---
description: SQLColAttributes (Access ドライバー)
title: SQLColAttributes (Access Driver) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], Access Driver
- Access driver [ODBC], SQLColAttributes
ms.assetid: adb6f81d-e8c7-4748-9b1d-f7a053788bbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d9758bb5c473971d3ed9acea52559da0a4aac67d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412278"
---
# <a name="sqlcolattributes-access-driver"></a>SQLColAttributes (Access ドライバー)
> [!NOTE]  
>  このトピックでは、ドライバー固有の情報にアクセスします。 この関数の一般的な情報については、「 [ODBC API リファレンス](../../odbc/reference/syntax/odbc-api-reference.md)」の該当するトピックを参照してください。  
  
|属性|コメント|  
|---------------|--------------|  
|SQL_COLUMN_DISPLAY_SIZE|LONGVARBINARY データの場合、SQL_COLUMN_DISPLAY_SIZE は列の最大長であり、列の最大長では2ではありません。|  
|SQL_OWNER_NAME|この列には、所有者名がサポートされていないため、空の文字列 ("") が返されます。|  
|SQL_QUALIFIER_NAME|データベースファイルへのパスが返されます。|  
|SQL_COLUMN_SEARCHABLE|LONGVARBINARY および LONGVARBINARY 列は SQL_UNSEARCHABLE として報告されます。<br /><br /> 固定長と可変長のバイナリおよび文字データ型は、LONGVARBINARY と LONGVARBINARY がない場合でも検索できます。|  
  
> [!NOTE]  
>  上記は、 **Sqlcolattributes**によって返される属性の完全な一覧ではありません。
