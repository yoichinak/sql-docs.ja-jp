---
description: 記述子フィールドの適合性
title: 記述子フィールドの準拠 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptor field conformance levels [ODBC]
- conformance levels [ODBC], descriptor field
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 6c29d93b-696c-4960-bff3-4d6bc41bc513
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36687cf456f4fcbbaa3f4b029e51098815dec3f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476744"
---
# <a name="descriptor-field-conformance"></a>記述子フィールドの適合性
次の表は、各 ODBC 記述子ヘッダーフィールドの準拠レベルを示しています。これは適切に定義されています。  
  
|機能|一致レベル|  
|--------------|-----------------------|  
|SQL_DESC_ALLOC_TYPE|コア|  
|SQL_DESC_ARRAY_SIZE|コア|  
|SQL_DESC_ARRAY_STATUS_PTR|コア (APD、IPR、および IRD の場合)。レベル 1 (この場合は)|  
|SQL_DESC_BIND_OFFSET_PTR|コア|  
|SQL_DESC_BIND_TYPE|コア|  
|SQL_DESC_COUNT|コア|  
|SQL_DESC_ROWS_PROCESSED_PTR|コア|  
  
 次の表は、各 ODBC 記述子レコードフィールドの準拠レベルを示しています。これは適切に定義されています。  
  
|機能|一致レベル|  
|--------------|-----------------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|[レベル 2]|  
|SQL_DESC_BASE_COLUMN_NAME|コア|  
|SQL_DESC_BASE_TABLE_NAME|[レベル 1]|  
|SQL_DESC_CASE_SENSITIVE|コア|  
|SQL_DESC_CATALOG_NAME|[レベル 2]|  
|SQL_DESC_CONCISE_TYPE|コア|  
|SQL_DESC_DATA_PTR|コア|  
|SQL_DESC_DATETIME_INTERVAL_ コード|コア [1]|  
|SQL_DESC_DATETIME_INTERVAL_ の精度|コア [1]|  
|SQL_DESC_DISPLAY_SIZE|コア|  
|SQL_DESC_FIXED_PREC_SCALE|コア|  
|SQL_DESC_INDICATOR_PTR|コア|  
|SQL_DESC_LABEL|[レベル 2]|  
|SQL_DESC_LENGTH|コア|  
|SQL_DESC_LITERAL_PREFIX|コア|  
|SQL_DESC_LITERAL_SUFFIX|コア|  
|SQL_DESC_LOCAL_TYPE_NAME|コア|  
|SQL_DESC_NAME|コア|  
|SQL_DESC_NULLABLE|コア|  
|SQL_DESC_OCTET_LENGTH|コア|  
|SQL_DESC_OCTET_LENGTH_PTR|コア|  
|SQL_DESC_PARAMETER_TYPE|コア/レベル 2 [2]|  
|SQL_DESC_PRECISION|コア|  
|SQL_DESC_ROWVER|[レベル 1]|  
|SQL_DESC_SCALE|コア|  
|SQL_DESC_SCHEMA_NAME|[レベル 1]|  
|SQL_DESC_SEARCHABLE|コア|  
|SQL_DESC_TABLE_NAME|[レベル 1]|  
|SQL_DESC_TYPE|コア|  
|SQL_DESC_TYPE_NAME|コア|  
|SQL_DESC_UNNAMED|コア|  
|SQL_DESC_UNSIGNED|コア|  
|SQL_DESC_UPDATABLE|コア|  
  
 [1] これらのレコードフィールドのサポートは、ドライバーが適用可能なデータ型をサポートしている場合にのみ必要です。  
  
 [2] コアレベルの準拠のために、ドライバーは SQL_PARAM_INPUT をサポートする必要があります。 レベル2のインターフェイス準拠の場合、ドライバーは SQL_PARAM_INPUT_OUTPUT と SQL_PARAM_OUTPUT もサポートする必要があります。
